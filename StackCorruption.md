# Debugging a stack check fail

# Finding the area

 - Get a debugger open

 - Wait for your crash

 - Get the backtrace & find the function

# Disasembling the function

`(gdb) disassemble`

```
Dump of assembler code for function: 
0x0040e74c <+0>:     push    {r4, r7, lr}
0x0040e74e <+2>:     sub     sp, #108        ; 0x6c
0x0040e750 <+4>:     add     r7, sp, #8
0x0040e752 <+6>:     str     r0, [r7, #4]
0x0040e754 <+8>:     str     r1, [r7, #0]
0x0040e756 <+10>:    ldr     r3, [pc, #660]
0x0040e758 <+12>:    ldr     r3, [r3, #0]
0x0040e75a <+14>:    str     r3, [r7, #92]   ; 0x5c
...
...
...
0x0040eb4a <+1022>:  ldr     r3, [pc, #28]   ; (0x40eb68)
0x0040eb4c <+1024>:  ldr     r2, [r7, #92]   ; 0x5c
0x0040eb4e <+1026>:  ldr     r3, [r3, #0]
0x0040eb50 <+1028>:  cmp     r2, r3
0x0040eb52 <+1030>:  beq.n   0x40eb58
0x0040eb54 <+1032>:  bl      0x4043d4 <__stack_chk_fail>
0x0040eb58 <+1036>:  adds    r7, #100        ; 0x64
0x0040eb5a <+1038>:  mov     sp, r7
0x0040eb5c <+1040>:  pop     {r4, r7, pc}
0x0040eb5e <+1042>:  nop
0x0040eb60 <+1044>:  ldr     r0, [r4, #60]   ; 0x3c
0x0040eb62 <+1046>:  lsls    r2, r0, #1
0x0040eb64 <+1048>:  lsls    r0, r0, #6
0x0040eb66 <+1050>:  lsls    r2, r0, #1
0x0040eb68 <+1052>:  lsls    r0, r0, #5
0x0040eb6a <+1054>:  movs    r0, #0
End of assembler dump.

0x0040eb58 <+1036>:  ...
```

# Finding the canary

Look for __stack_chk_fail towards the bottom.

Notice the `beq` on the previous line, this will either call the fail or go to the following line (0x40eb58 in this example) depending on if the values in the `cmp` line before it are equal or not. In this case we are comparing `r2` and `r3`.

r3 is set to `0x40eb68` (the end of the function).

r2 is set to `[r7, #92]` (r7+92).  Looking above at the start of the disassembly we can see that r7 is set to `sp + #8` (AKA $fp). This means that r2 is equal to `$fp + 92`.

This can be confirmed by printing the value at this location. It should be equal to __stack_chk_guard.

```
(gdb) p __stack_chk_guard
$1 = 0xbaadc0de
(gdb) p $fp+92
$2 = (void *) 0x20003e28
(gdb) p *0x20003e28
$3 = (void *) 0xbaadc0de
```

?> Because the the code is compiled, this offset will be constant.

# Catching the canary

 - Set a breakpoint (with optional conditions). ex: `break <file>:<line> if <foo> == <bar>`.

 - Restart the processor `monitor reset`, and continue execution `continue`

 - <Hit the breakpoint>

 - Find the exact address (at double check its correct)

```
(gdb) p $fp+92
$1 = (void *) 0x20003e28
(gdb) p *0x20003e28
$2 = (void *) 0xbaadc0de
```

 - Set a watchpoint at this address

```
(gdb) watch *0x20003e28
Hardware watchpoint 2: *0x20003e28
```

 - Continue execution `continue`

 - <Hit the watchpoint>

```
Hardware watchpoint 2: *0x20003e84
Old value = 0xbaadc0de
New value = 0xa030000
```

# Inspecting

 - Run a `bt`
 - jump to a frame `f #`
 - inpect the variables `info locals`
 - etc
