
# Kernel Modules

> Source: `https://en.wikibooks.org/wiki/The_Linux_Kernel/Modules`

The Linux kernel is a monolithic type kernel by design, meaning all required functionality for hardware operations are included in a single binary blob. However as of kernel version 3.0 (?) the it started external module support, this meant that if a user needed a said functionality he's not no more obliged to recompile the kernel from source "`make menuconfig`", all he's supposed to de is `load` or `unload` the module that adds support for the feature he wants to use.


## Listing

In order to check what modules are loaded use `lsmod`, and since the list might be a bit lengthy `grep` is perfect helper is you already knew what you're looking for

```
lsmod | grep [MOD_NAME]
```

## Loading (Inserting)

If the module you're after isn't there, `insmod` or `Insert Module` is the tool that will help you load the module.

```
insmod [MOD_NAME]

# equivalently
modprob [MOD_NAME]
```

## Offloading (Removing)

If you no longer need the module to be loaded for whatever reason ( Security, Performance... ), use `rmmod` or `Remove Module` to unload it.

```
rmmod [MOD_NAME]

# equivalently
modprob -r [MOD_NAME]
```

## Simple Kernel Module

Here is a simple kernel module source code in `C`, all it does is output to the kernel log `TESTING MODULE\n` when is starts and `END OF TESTING MODULE\n` when it's done.

```c
#include <kernel/init.h>
#include <kernel/module.h>

MODULE_LICENCE("DUAL BSD/GPL");
static int test_init(void)
{
    printk(KERN_ALERT "TESTING MODULE\n");
    return 0;
}
static void test_end(void)
{
    printk(KERN_ALERT "END OF TESTING MODULE\n");
}
module_init(test_init);
module_exit(test_end);
```

The `KERN_ALERT` argument to `printk` set the priority of the job,

```
#define KERN_EMERG      "<0>"   /* system is unusable                   */
#define KERN_ALERT      "<1>"   /* action must be taken immediately     */
#define KERN_CRIT       "<2>"   /* critical conditions                  */
#define KERN_ERR        "<3>"   /* error conditions                     */
#define KERN_WARNING    "<4>"   /* warning conditions                   */
#define KERN_NOTICE     "<5>"   /* normal but significant condition     */
#define KERN_INFO       "<6>"   /* informational                        */
#define KERN_DEBUG      "<7>"   /* debug-level messages                 */
```

In order to compile the kernel module

## Additional Info

The directory `/lib/modules`

The `depmod` tool is responsible for resolving module dependency before loading a module. So if a module calls function on another one it will make it a dependency for the first, in order to be loaded before the first one.

```
depmod
```

# System Calls (Syscalls)

In order for user space processes `Ring 3` to be able communicate to the kernel at `Ring 0` an interface must be used, it's called `System Calls` or `Syscalls`.

# Netem (Network Emulator)

>https://wiki.linuxfoundation.org/networking/netem

This kernel module can be used to manipulate packets to emulate WAN (Delay, Jitter, Corruption, Duplications...etc)

