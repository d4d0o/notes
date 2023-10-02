See <https://www.kernel.org/doc/html/latest/dev-tools/kmemleak.html>

To test a critical section on demand with a clean kmemleak do:

```
# echo clear > /sys/kernel/debug/kmemleak
... test your kernel or modules ...
# echo scan > /sys/kernel/debug/kmemleak
```

Then as usual to get your report with:

```
# cat /sys/kernel/debug/kmemleak
```

 for full detail.

1. Run make menuconfig from the buildroot directory and setup a  cutom linux kernel defconfig file at ../base_external/configs/linux.config under the "Kernel" submenu.  This will allow you to track your changes to kernel configuration in your base_external tree.  Use the previous kernel set as BR2_LINUX_KERNEL_CUSTOM_CONFIG_FILE in your aesd_qemu_defconfig file as the initial content of this file by copying from the buildroot directory to your base_external path specified in the kernel submenu.  You can do this with command cp buildroot/board/qemu/aarch64-virt/linux.config base_external/configs/linux.config
2.  make linux-menuconfig from buildroot directory
3. Enable the following options:

- kernel hacking -> kernel debugging
- kernel hacking -> memory debugging -> kernel memory leak detector
- kernel hacking -> memory debugging -> Simple test for the kernel memory leak detector (This option would install a module which would have memory leaks.)
- kernel hacking -> memory debugging -> Maximum kmemleak early log entries - set to 4096 (see <https://stackoverflow.com/questions/55764173/kernel-memory-leak-detector>


- )
- kernel hacking->Sample Kernel Code

3\. Save the configuration using save-config.sh, build using build.sh and run qemu.

4\. Build and boot up the resulting image in qemu.  If the debugfs isn't already mounted, mount with:

mount -t debugfs nodev /sys/kernel/debug/

5\. Enter the following commands on terminal to check if the kernel memory leak detector has been properly installed and is detecting memory leaks.  This loads a module that deliberately leaks memory called “kmemleak-test”

- echo clear > /sys/kernel/debug/kmemleak
- modprobe kmemleak-test
- echo scan > /sys/kernel/debug/kmemleak
- cat /sys/kernel/debug/kmemleak
  - You should see memory leaks identified, which proves your leak test kernel config is working.
- rmmod kmemleak-test

6\.  Reboot and repeat steps 4 and 5 using your module instead of kmemleak-test, removing and adding your module after clearing any existing memory leaks.

- You should see no memory leaks identified by the scan step for /sys/kernel/debug/kmemleak when loading your module.