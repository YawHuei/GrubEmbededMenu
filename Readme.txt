Method of Modify grub embedding configuration file:


grubmenu_x86.exe, grubmenu_x64.exe, mkimage_x86.exe, mkimage_x64.exe, 
grub-mkimage_x86.exe, grub-mkimage_x64.exe are compiled with Ubuntu 20.04 Mingw.
and Compressed with UPX.


1. {Grub4Dos}
grldr   ,See: https://github.com/chenall/grubutils

Examples:
grubmenu_x??.exe import grldr menu.lst

Usage:
grubmenu info grldr
grubmenu print grldr
grubmenu [-r] export grldr menu.lst
grubmenu [-r] [-k] import grldr menu.lst

#define FG_KEEP	2
-k : (! old_style) && ((fg & FG_KEEP)==0))

#define FG_RAW	1
-r : fopen(menu,((O_BINARY!=0) && (fg & FG_RAW))?"rb":"r");



2.1 {grub4dos-for_UEFI}
BOOTX64.EFI     , See: https://github.com/grub4dos/mkimage

Examples:
mkimage_x??.exe -d ./x86_64-efi -p /efi/grub -c "%~dp0menu.lst" -O x86_64-efi -o BOOTX64.EFI  


2.2 {grub4dos-for_UEFI}
BOOTIA32.EFI    , See: https://github.com/grub4dos/mkimage

Examples:
mkimage_x??.exe -d ./i386-efi -p /efi/grub -c "%~dp0menu.lst" -O i386-efi -o BOOTIA32.EFI

Usage:
See: grub-mkimage.c
-d "DIR" , directory, use images and modules under DIR [default=%s/<platform>]
-p "DIR" , set prefix directory
-m "FILE" , embed FILE as a memdisk image
-c "FILE" , embed FILE as an early config
-f "FILE" , embed FILE as a font
-o "FILE" , output a generated image to FILE [default=stdout]
-O "FORMAT" , generate an image in format
-C none|auto , choose the compression to use for core image
-E , Use pe32 optional header
-v , print verbose messages.


3. {grub 2}
grub2.img   , See:  https://www.gnu.org/software/grub/

Examples:
set /p modules=<%~dp0legacy.lst
grub-mkimage_x??.exe -c ..\cfg\grub_hd.cfg -d i386-pc -p /grub -o core.img -O i386-pc %modules%
copy /b %cd%\i386-pc\boot.img+core.img ..\grub2.img

legacy.lst , See: i386-pc/*.mod, The contents of the file are below:
biosdisk boot normal cat chain configfile ...

Usage:
Reference website https://www.gnu.org/software/grub/manual/grub/grub.html
