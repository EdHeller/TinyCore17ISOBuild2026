# TinyCore 17

So this is a quick how to build tinycore as an iso. Using Rich's pre-made mutli version ISO from 15.x

Step 1 download the latest kernel source. distro [.] ibiblio [.] org/tinycorelinux/17.x/x86/release/src/kernel/

Step 2 extract tar ``-xvf linux- <version number> -patched.tar.xz``

Step 3 copy and rename config- <version number> -tinycore to linux- <version number>/.config

Step 4 use make menuconfig to adjust the things you'd like to include in the kernel*. 

Step 5 make the kernel 

Step 6 copy and rename bzImage under linux- <version number>/arch/x86/boot/bzImage to MakeISO/ISO/V17/vmlinuz


Step 7 extract core.gz
(Thankfully distro [.] ibiblio [.] org/tinycorelinux/17.x/x86/release/distribution_files/ has a nicely setup core.gz file. It's simple to extract and alter)
```
cp core.gz /tmp
cd /tmp
zcat /tmp/core.gz | sudo cpio -i -H newc -d
```

(Adjusting the modules and dependancies under tmp/lib/modules/<version number>-tinycore/ and adding them to the kernel is up to you the user.)

Step 8 repack core.gz
```
find | sudo cpio -o -H newc | gzip -2 > ../core.gz
cd ..
#compress the core more
advdef -z4 modules.gz
```

Step 9 Replace core.gz with the one you just repacked MakeISO/ISO/V17/core.gz

Step 10 build an iso from the MakeISO directory use bash ./MkISO

If something goes wrong compare to the original ISO at distro [.] ibiblio [.] org/tinycorelinux/15.x/x86/TestISO/
Note: If you're copying files from the ISO the permissions will likely be overly restrictive. I might have messed up what the permissions should be set to. Sorry.

##why?
I just wanted to enjoy how tiny the kernel is before I bloat the system with a full C++ compiler and tooling (~200MB)
