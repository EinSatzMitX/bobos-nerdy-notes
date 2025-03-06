#Programming #osdev 
Target triplets are usually used in [[Compiler]]s to specify compile targets. They describe a platform, containing [[CPU Architectures]], a vendor (which can be usually be left out) and an [[Operating System]]. This can get a bit complex, as the [[Operating System]] field can contain a '-' character, e.g. "linux-gnu"

**General structure:**
machine-vendor-operatingsystem

**Example:**
x86_64-unkown-freebsd 
OR
x86_64-freebsd

To find out the target triplet of their current machine, one could simply run
```gcc -dumpmachine```
