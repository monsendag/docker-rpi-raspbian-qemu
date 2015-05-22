# docker-rpi-raspbian-qemu

Runs Raspbery Pi Raspbian in a Docker container on an x86 Linux kernel.

---

* Useful for building and testing arm-based applications on x86 before deployment
* Requires a linux kernel with binfmt_misc (but can be run through boot2docker on OSX)
* Because of the way the filesystem works in Docker, we can't just mount qemu-arm-static as a volume – it needs to be in the container file system

---

1. Make sure the kernel recognizes the arm binary by its fingerprint and runs it with qemu using binfmt_misc:

```shell
sudo echo ':arm:M::\x7fELF\x01\x01\x01\x00\x00\x00\x00\x00\x00\x00\x00\x00\x02\x00\x28\x00:\xff\xff\xff\xff\xff\xff\xff\x00\xff\xff\xff\xff\xff\xff\xff\xff\xfe\xff\xff\xff:/usr/bin/qemu-arm-static:' > /proc/sys/fs/binfmt_misc/register
```

2. Run the Docker image:

```shell
docker run -it monsendag/rpi-raspbian-qemu /bin/bash
```
