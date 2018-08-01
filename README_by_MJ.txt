To boot up the iso: 
  qemu-system-i386 -cdrom os.iso

From the original documentation:
  make run-bin   : to run from qemu
  make build-iso : to build an iso file with grub. It needs xorriso.
  make run-iso   : launch qemu with iso file as a CDROM.
----
Prerequisite: The "xorriso"-tool:
Download it from: https://www.gnu.org/software/xorriso/#download
(or maybe check into https://github.com/clearlinux-pkgs/xorriso or
https://github.com/clearlinux-pkgs/xorriso/blob/master/xorriso.spec )

Move/extract it under the current working dir, e.g. ./xorriso-1.4.8/
=============================================================================

Build necessary files:
./configure --prefix=/home/martin/Downloads/resume_operating_system/
make
(not necessary: make install)

Next, Make-file config for "build-iso" should contain e.g. (notice the last option!):
	grub-mkrescue -o os.iso isofiles --xorriso=./xorriso-1.4.8/xorriso/xorriso
If the last option is not there, add it to the Makefile.

You might now run "make build-iso" and get something like:
"grub-mkrescue: error: 'mformat' invocation failed"

In that case: "pacman -S mtools" and the result should be:

--------------------------
$ make build-iso
cp -rf kernel.bin isofiles/boot/kernel.bin
#grub-mkrescue -o os.iso isofiles
grub-mkrescue -o os.iso isofiles --xorriso=./xorriso-1.4.8/xorriso/xorriso
GNU xorriso 1.4.8 : RockRidge filesystem manipulator, libburnia project.

Drive current: -outdev 'stdio:os.iso'
Media current: stdio file, overwriteable
Media status : is blank
Media summary: 0 sessions, 0 data blocks, 0 data, 12.4g free
Added to ISO image: directory '/'='/tmp/grub.kdzXwA'
xorriso : UPDATE : 897 files added in 1 seconds
Added to ISO image: directory '/'='/home/martin/Downloads/resume_operating_system/isofiles'
xorriso : UPDATE : 901 files added in 1 seconds
xorriso : NOTE : Copying to System Area: 512 bytes from file '/usr/lib/grub/i386-pc/boot_hybrid.img'
ISO image produced: 9914 sectors
Written to medium : 9914 sectors at LBA 0
Writing to 'stdio:os.iso' completed successfully.
--------------------------

sources : 
http://mikeos.sourceforge.net/write-your-own-os.html 
http://os.phil-opp.com/multiboot-kernel.html 
http://wiki.osdev.org/Bare_bones 
http://www.cs.vu.nl/~herbertb/misc/writingkernels.txt


