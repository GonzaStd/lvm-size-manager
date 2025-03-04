## 📌 ➖ Reduce Logical Volume (LV)

First you have to **shrink the file system** and then the *LV*:

1️⃣ Check volume: `e2fsck -f /dev/mapper/<vg-name>--vg-<lv>
> *vg* means *Volume Group*

2️⃣ Shrink the file system: `resize2fs /dev/mapper/<vg-name>--vg-<lv> XG`

>`X` is the number of GB for the FINAL size to which we want to reduce the *filesystem*.

3️⃣ Reduce the logical volume `lvreduce -L XG /dev/mapper/<vg-name>--vg-<lv>

> `X` is the number of GB for the FINAL size to which we want to reduce the volume, but we can also use `-X` to indicate the size to which it is SUBTRACTED or REDUCED.

Example: If the volume is **150GB** and we want to extract **50GB**
`sudo lvreduce -L -50G /dev/mapper/<vg-name>--vg-<lv>`

## 📌 ➕ Logical Volume Extender (LV)

First you have to **extend the volume** and then the fs:

1️⃣ Check volume: `e2fsck -f /dev/mapper/<vg-name>--vg-<lv>

2️⃣ Extend the logical volume `lvextend -L XG /dev/mapper/<vg-name>--vg-<lv>

> `X` is the number of GB for the FINAL size to which we want to extend the volume, but we can also use `+X` to indicate the size to which it is ADDED or EXTENDED.

Example: If the volume has **150GB** and we want to add **50GB** to it
`sudo lvreduce -L +50G /dev/mapper/<vg-name>--vg-<lv>`

3️⃣ Extend the file system: `resize2fs /dev/mapper/<vg-name>--vg-<lv>

>The fs automatically adapts to the size of the volume.

## ✅ Extra Commands

- **See the size of our volume group and its free space**: `vgs`
- **See the size of our volumes**: `lvs`
- **See the size of the file systems**: `df -h`
