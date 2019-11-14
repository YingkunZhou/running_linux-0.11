### Decompress .tar.xz file if you need it
```
tar Jvxf hdc-0.11-new.tar.xz
tar Jvxf rootimage-0.11.tar.xz
tar Jvxf hdc-0.11.tar.xz
tar Jvxf diska.tar.xz
```
### Compile the src
```
make
```
### Ungraceful!!!
```
./setrootdev.sh Image 021d
./setrootdev.sh Image 0301
```
### Configure the .gdbinit file and modify the path to your own home directory!!! Not elegant, can someone tell me how to avoid using this command before debug?
```
echo "add-auto-load-safe-path .gdbinit" > /home/zhou/.gdbinit
```
### Normal mode
```
../bochs-2.6.9/bochs -q -f bochsrc-hd.bxrc
```
### Debug mode, here the terminal is lxterminal, if you know how to launch normal terminal on ubuntu, contact with me!!! Make sure to enable debug mode in bochsrc-hd.bxrc first!!!
```
lxterminal -T "gdb --quiet kernel.sym" -e "gdb --quiet kernel.sym" & ../bochs-2.6.9/bochs -q -f bochsrc-hd.bxrc
```
### Or use current terminal to launch gdb. Make sure to enable debug mode in bochsrc-hd.bxrc first!!!
```
../bochs-2.6.9/bochs -q -f bochsrc-hd.bxrc & gdb kernel.sym
```
### Qemu emulation commands
```
../qemu/qemu-system-i386 -no-kqemu -L ../qemu -m 16M -boot a -fda Image 2>/dev/null -fdb rootimage-0.11
../qemu/qemu-system-i386 -no-kqemu -L ../qemu -m 16M -boot a -fda Image 2>/dev/null -fdb rootimage-0.11 -s -S & gdb kernel.sym
../qemu/qemu-system-i386 -no-kqemu -L ../qemu -m 16M -boot a -fda Image 2>/dev/null -hda hdc-0.11-new.img # -fdb diska.img
../qemu/qemu-system-i386 -no-kqemu -L ../qemu -m 16M -boot a -fda Image 2>/dev/null -hda hdc-0.11-new.img -s -S & gdb kernel.sym
```
### Also you can use your own system build-in qemu-system-i386 to emulate linux-0.11
```
sudo # needed for -enable-kvm 
qemu-system-i386 -m 16M -boot a -fda Image 2>/dev/null -hda hdc-0.11-new.img #-enable-kvm -fdb diska.img
qemu-system-i386 -m 16M -boot a -fda Image 2>/dev/null -hda hdc-0.11-new.img -s -S & gdb kernel.sym
```
