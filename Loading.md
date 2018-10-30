#+TITLE: Basic Setup to Configure the Inifinty Keyboard
#+AUTHOR: ricky-pz2
#+EMAIL: reddit.com/user/khalki
#+STARTUP: align

- Notes
  Be aware that the following was tested with a standard version of the
  infinity 60% keyboard. Instructions may deviate if you are using the
  infinity ergodox or the alphabet layouts. Since I do not own this
  variations, I can not provide notes on how to handle them. Contributions
  with notes on how to handle them are welcome.

* After Building Your Keyboard

  So you finish soldering your keyboard. You have plugged in your keyboard
  and right away you can start typing. However, you are a unique person that
  likes buttons to be in different parts. For example, you like to use the
  superior layout Dvorak to the inferior QWERTY. Perhaps you disagree where
  the backspace button belongs into. Perhaps you want to create your personal
  efficient layout.

  I am going to attempt to walk you on a step by step process on getting your
  personal layout. I am assuming that you know how to navigate the filesystem.
  If you do not know how to do this, then you may want to look at this
  [[https://www.youtube.com/watch?v=j8ZRWSVfuiU&list=PLrC-HcVNfULZxXqyiAVzck8fRMFQNNa8t][youtube videos]]. Just know that you don't need how to program or anything
  fancy, but it is essential that you know how to change directories via
  the terminal.

  For editing files via terminal you can use nano or pico, but you can
  probably use the graphical user interfaces.

- First Steps: Setup Your System

  The very first thing that you ought to do is to setup your system.
  In the wikis you can find information on how to do this.

  [[https://github.com/kiibohd/controller/wiki/Linux-Setup][linux setup]]

  [[https://github.com/kiibohd/controller/wiki/Mac-Setup][mac setup]]

  [[https://github.com/kiibohd/controller/wiki/Windows-Setup][windows setup]]

  I have tried Ubuntu for Linux and OSX 10.10 for Mac. They both work well.
  However I have not tried compiling using Cygwin for Windows, please keep
  this in mind if using Windows.

- Second Step: Clone the Project

  In order for you to build the necessary things for your project, you need
  to clone this project.
  You simply do this by running the following command in the terminal.

  #+BEGIN_SRC
  git clone https://github.com/kiibohd/controller.git
  #+END_SRC

  This will create a folder called `controller` on the directory that you are
  working on.

  #+BEGIN_SRC
  cd controller
  #+END_SRC

* Third Step: First Compile

  First we need to compile the project. We aren't really going to use anything
  from this first compile. However, by compiling the project, we will get some
  essential folders and files that will make our lifes easier.

  Doing the compile is already covered in the Building page.
  However, I will write down the commands that you really need to perform.
  Make sure that you are inside the project (Folder called `controller`).

  #+BEGIN_SRC
  mkdir first_compile
  cd first_compile
  cmake ..
  make
  #+END_SRC

  You really only needed to perform the cmake step in the controller folder.
  However is a good idea to compile everything. This way you can ensure that
  you have all the necessary tools when compiling for your layout.

  Assuming that you had no hiccups when compiling, let's go back to the project
  main directory that we cloned early on:

  #+BEGIN_SRC
  cd ..
  #+END_SRC

* Fourth Step: Create Your KLL Files

  We now need to create our configuration files. In this example I am making
  two files. I am picking the arbitary name of myconfig.kll and myconfig1.kll on my files.
  Also, since I am a Dvorak user, so I will be remapping my keys to the Dvorak layout. I suggest to
  follow the next steps with your own KLL files. However, I hope that my
  files give you an idea on how to modify your layout.

  First we need to change directory to the folder where we will store our layouts:
  #+BEGIN_SRC bash
  cd kll/layouts
  #+END_SRC

  Then we create will create our files. In this example I will create the file with `gedit`,
  but feel free to use any other editor (gedit should open a GUI window to work in).
  #+BEGIN_SRC bash
  gedit myconfig.kll
  #+END_SRC

  NOTE: `gedit` comes in the default ubuntu installation. Other distros may have other GUI editors
  like kate in Kubuntu. Just make sure to use a editor that you have and know how to use.

  This is my myconfig.kll file:
  #+NAME: myconfig.kll
  #+BEGIN_SRC
  Name = "Myconfig";
  Layout = "Standard";
  Version = "1";
  Author = "ricky.pz2";
  KLL = "0.3";
  Date = "2015-06-05";

  U"ESC" : U"BACKTICK";
  U"MINUS" : U"LBRACE";
  U"EQUAL" : U"RBRACE";
  U"BACKSLASH" : U"BACKSPACE";
  U"BACKTICK" : U"BACKSPACE";
  U"Q" : U"QUOTE";
  U"W" : U"COMMA";
  U"E" : U"PERIOD";
  U"R" : U"P";
  U"T" : U"Y";
  U"Y" : U"F";
  U"U" : U"G";
  U"I" : U"C";
  U"O" : U"R";
  U"P" : U"L";
  U"LBRACE" : U"SLASH";
  U"RBRACE" : U"EQUAL";
  U"BACKSPACE" : U"BACKSLASH";
  U"CTRL" : U"CAPSLOCK";
  U"S" : U"O";
  U"D" : U"E";
  U"F" : U"U";
  U"G" : U"I";
  U"H" : U"D";
  U"J" : U"H";
  U"K" : U"T";
  U"L" : U"N";
  U"SEMICOLON" : U"S";
  U"QUOTE": U"MINUS";
  U"Z" : U"SEMICOLON";
  U"X" : U"Q";
  U"C" : U"J";
  U"V" : U"K";
  U"B" : U"X";
  U"N" : U"B";
  U"COMMA" : U"W";
  U"PERIOD" : U"V";
  U"SLASH" : U"Z";
  U"FUNCTION1" : U"RSHIFT";
  U"FUNCTION2" : U"LCTRL";
  U"RGUI" : U"RALT";
  U"RALT" : U"RGUI";
  U"FUNCTION3" : layerShift( 1 );
  U"FUNCTION4" : U"RCTRL";
  #+END_SRC

  Create myconfig1.kll too:
  #+BEGIN_SRC bash
  gedit myconfig1.kll
  #+END_SRC

  This is my mycofig1.kll file:
  #+NAME: myconfi1.kll
  #+BEGIN_SRC
  Name = "Myconfig1";
  Layout = "Standard";
  Version = "0.1";
  Author = "ricky.pz2";
  KLL = "0.3";
  Date = "2015-06-05";

  U"ESC" : U"ESCAPE";
  U"1" : U"F1";
  U"2" : U"F2";
  U"3" : U"F3";
  U"4" : U"F4";
  U"5" : U"F5";
  U"6" : U"F6";
  U"7" : U"F7";
  U"8" : U"F8";
  U"9" : U"F9";
  U"0" : U"F10";
  U"MINUS" : U"F11";
  U"EQUAL" : U"F12";
  U"BACKSLASH" : U"DELETE";
  U"BACKTICK" : U"INSERT";
  U"Q" : U"PAGEDOWN";
  U"W" : U"UP";
  U"E" : U"PAGEUP";
  U"R" : U"HOME";
  U"F" : U"END";
  U"P" : CONS"MUTE";
  U"LBRACE" : CONS"VOLUMEDOWN";
  U"RBRACE" : CONS"VOLUMEUP";
  U"FUNCTION1" : U"RSHIFT";
  U"FUNCTION2" : U"LCTRL";
  U"RGUI" : U"RALT";
  U"RALT" : U"RGUI";
  U"FUNCTION4" : U"RCTRL";
  #+END_SRC

* Fifth Step: Second Compile - Your Files

  We are almost there. We need to compile a second time with our configuration
  files. In order to do this, we need to go into the Keyboard folder in the project.
  #+BEGIN_SRC bash
  cd ../../Keyboards
  #+END_SRC

  In this folder you will see a file called
  `infinity.bash`. We need to modify the file with the following changes:

  #+BEGIN_SRC
  #This line:
  DefaultMap="md1Overlay stdFuncMap"
  #Changes to:
  DefaultMap="myconfig"
  #This other line:
  PartialMaps[1]="hhkbpro2"
  #Changes to:
  PartialMaps[1]="myconfig1"
  #+END_SRC

  PartialMaps[n] will map it to the layer number n, so in our example I am
  adding those keys to the first layer.

  Now we can use this script to compile the our layouts. All you need to do is
  the following in the terminal:
  #+BEGIN_SRC bash
  bash infinity.bash -f -o my_layout
  #+END_SRC

  This will create a folder called `my_layout`.
  Let's go to the folder and see what is inside the folder with:
  #+BEGIN_SRC bash
  cd my_layout && ls -alF
  #+END_SRC

  You should see a file called `load`. This is the file that we use to load the
  configuration into the keyboard.

* Sixth Step: Load Layout to Infinity Keyboard

  Now let's load the layout into the keyboard.
  The first step that you need to do is plug in your keyboard into your computer.
  After the computer loads the keyboard, you need to push the button on the back
  of the keyboard, this should turn on a orange led on.

  Finally, on the terminal do:
  #+BEGIN_SRC bash
  bash load
  #+END_SRC

  Your keyboard now have your layout. You should be able to type right away the
  layout that you just created.
