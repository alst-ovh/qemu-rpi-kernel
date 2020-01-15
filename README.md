# qemu-rpi-kernel

Ready-made kernels that can be used to emulate a Raspberry Pi using QEMU.

They are compiled from the same [kernel sources] used for official Raspian
images, with tweaks to make them suitable for use with QEMU, and are supposed
to be used along with official Raspbian images.

## Obtaining Raspbian

Before starting, you should download a [Raspbian image] from the Raspberry Pi
website and extract the `.zip` archive to obtain an `.img` file.

## Kernel Image

 `kernel-qemu-4.*.*-buster` are the most recent images, which are compatible
  with Raspbian Buster and Stretch. To use these images, you'll need the
  `versatile-pb.dtb` file which is also contained in this repository.

## Using kernel images with QEMU

The QEMU command line will look like

    $ qemu-system-arm \
      -M versatilepb \
      -cpu arm1176 \
      -m 256 \
      -hda /.../2019-09-26-raspbian-buster-lite.img \
      -net nic \
      -nic user,hostfwd=tcp::5022-:22 \
      -dtb /.../versatile-pb.dtb \
      -kernel /.../kernel-qemu-4.19.50-buster \
      -append 'root=/dev/sda2 panic=1' \
      -no-reboot

with the paths to the disk image, `.dtb` file and kernel image adjusted
appropriately.

## Building your own kernel image

See the contents of the `tools/` directory, where the build scripts and
instructions on how to use them are stored.

## Origin of this repository

While searching the Internet for information on emulating a Raspberry Pi using
QEMU in Jun 2015, most of the guides pointed to kernel images hosted on
[xecdesign.com]; however, at the time the resource was no longer online, and
that's still the case as of Feb 2019.

This repository was initially created as a way to make those kernel images
available once again, and has since been expanded to provide improved and
up-to-date images.

## Further information

Additional documentation can be found on the [wiki].

[Raspbian image]: https://www.raspberrypi.org/downloads/raspbian/
[kernel sources]: https://github.com/raspberrypi/linux/
[xecdesign.com]: https://xecdesign.com/downloads/linux-qemu/kernel-qemu
[wiki]: https://github.com/dhruvvyas90/qemu-rpi-kernel/wiki
