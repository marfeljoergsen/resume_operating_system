sources : 
http://mikeos.sourceforge.net/write-your-own-os.html 
http://os.phil-opp.com/multiboot-kernel.html 
http://wiki.osdev.org/Bare_bones 
http://www.cs.vu.nl/~herbertb/misc/writingkernels.txt

================================
qemu-system-i386 -cdrom os.iso
----
About the "xorriso"-tool:

./configure --prefix=/home/martin/Downloads/resume_operating_system/
make
(not necessary: make install)

Next, Make-file config for "build-iso" should contain e.g. (notice the last option!):
	grub-mkrescue -o os.iso isofiles --xorriso=./xorriso-1.4.8/xorriso/xorriso

You might now run "make build-iso" and get something like:
"grub-mkrescue: error: 'mformat' invocation failed"

In that case: "pacman -S mtools" and the result should be:


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





