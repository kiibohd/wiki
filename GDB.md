# Debugging Faults

## Compiler Flags

In your `<keyboard.bash>` add the following defines `-DCMAKE_BUILD_TYPE=Debug -DJLINK=1` to `CMakeExtraArgs`

Compile and load the firmware

## GDB Server

A gdb server can be launched with `./debug -s` from the build directory.

You should see

```
Listening on TCP/IP port 2331
Connecting to target...Connected to target
Waiting for GDB connection...
```

## GDB Client

In another terminal navigate to the build dir and run `./debug` (or `arm-none-eabi-gdb *.elf` directly)

You should see `Reading symbols from kiibohd.elf...done.`

## Running

`monitor reset` will restart the chip from the beggining.

`c` (continue) begins execution.

When a fault occurs the debugger should automatically break

## Manual Breakpoints

`break <function>` or `break <file>:<line>` can be used to manually stop execution on a specific line.

## Finding the cause

Once a fault occurs you should see something similar to the following

```
Program received signal SIGTRAP, Trace/breakpoint trap.
fault_isr () at ../../Lib/sam.c:87
87              asm volatile("BKPT #01");
```

at this point you can use `bt` (backtrace) to see how we got here

```
#0  fault_isr () at ../../Lib/sam.c:87
#1  0x004062b2 in busfault_handler (faultStackedAddress=0x20008080) at ../../Lib/arm_cortex.c:169
#2  <signal handler called>
#3  0x0041af28 in cliFunc_help (args=0xdeadbeef <error: Cannot access memory at address 0xdeadbeef>) at ../../Debug/cli/cli.c:574
#4  0x0041a9a4 in CLI_commandLookup () at ../../Debug/cli/cli.c:371
#5  0x0041a67a in CLI_process () at ../../Debug/cli/cli.c:205
#6  0x00404468 in main () at ../../main.c:177
```

Note in this case that cliFunc_help caused the busfault handler to be executed.

## Inspecting the damage

Typing `f 1` (frame 1) we can inspect the state inside the error handler (or any other function in the backtrace)

Once in this function we can use `info locals` to print the current variables

```
frame = {
  r0 = 0x0,
  r1 = 0xdeadbeef,
  r2 = 0xdeadbeef,
  r3 = 0xffffeeee,
  r12 = 0x2,
  lr = 0x410239,
  pc = 0x410794,
  xpsr = 0x61000000
}
BFSR = {
  IBUSERR = 0x0,
  PRECISERR = 0x0,
  IMPRECISERR = 0x0,
  UNSTKERR = 0x1,
  STKERR = 0x0,
  BFARVALID = 0x1
}
BFAR = 0xffffeeee
```

In this case, the invalid instruction can then be found with `list *frame.pc`

```
0x41af28 is in cliFunc_help (../../Debug/cli/cli.c:574).
...
574             volatile uint32_t foo = *((uint32_t*)0xFFFFEEEE);
...
```

The exact instruction can also be viewed with `x/i frame.pc`

```
   0x41af28 <cliFunc_help+224>: ldr     r2, [r3, #0]
```

Here we can see that we attempted to load the value at r3+0 (ie: 0xFFFFEEEE) into r2.
This memory address is not valid and thus causes a bus error.

?> More info on faults can be found at [2.4.1 Fault types - Cortex-M4 Devices Generic User Guide](http://infocenter.arm.com/help/index.jsp?topic=/com.arm.doc.dui0553a/ch02s04s01.html)
