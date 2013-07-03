0. Introduction

This kernel module turns what my dance pad sends through a PS/2 to USB adapter into something that works for the game Stepmania.

My PS/2 to USB adapter (Pu120T) is identified by lsusb as:

ID 0810:0001 Personal Communication Systems, Inc. Dual PSX Adaptor

The original patch, that I adapted for Linux kernel 3.9, was obtained from:

http://www.inf.ufsc.br/~adiel/en/misc/dance-pad/index.html

Miriam Ruiz <miriam@debian.org>


1. Install and prepare the kernel headers

$ sudo -i
# apt-get install module-assistant
# m-a prepare


2. Compile the code

$ make
make -C /lib/modules/[version]/build M=/[DIRECTORY] modules
make[1]: se ingresa al directorio `/usr/src/linux-headers-[version]'
  CC [M]  /home/inniyah/joydev/joydev-dancepad.o
  Building modules, stage 2.
  MODPOST 1 modules
  CC      /home/inniyah/joydev/joydev-dancepad.mod.o
  LD [M]  /home/inniyah/joydev/joydev-dancepad.ko
make[1]: se sale del directorio `/usr/src/linux-headers-[version]'


3. Remove the vanilla module from the running kernel

$ sudo rmmod joydev


4. Insert the compiled module into the running kernel

$ sudo insmod joydev-dancepad.ko


5. Check that the module has been successfully installed

$ lsmod | grep joydev
joydev_dancepad        17087  0 


6. Check that the module works okay

$ jstest-gtk 


7. More information

Stepmania:
http://www.stepmania.com/

Getting my dance pad to work:
http://www.inf.ufsc.br/~adiel/en/misc/dance-pad/index.html

“Hello World” Loadable Kernel Module:
http://blog.markloiseau.com/2012/04/hello-world-loadable-kernel-module-tutorial/
