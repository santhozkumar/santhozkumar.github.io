# Libvirt


![[Linux Architecture](/assets/img/post-imgs/linux-architecture.png)](/assets/img/post-imgs/linux-architecture.png)


# QEMU










# KVM
It solves the software binary translation problem by using hardware virtualization extensions in modern CPUs, such as Intel VT-x and AMD-V. These extensions allow KVM to run guest operating systems directly on the host CPU, providing near-native performance.
Without VT-x/AMD-V instructions KVM cannot function as a hypervisor, and it will fall back to using QEMU's software emulation mode, which is significantly slower than hardware-assisted virtualization.





### References
- https://namastedev.com/blog/x86-hardware-virtualization-vt-x-amd-v/
- https://docs.oracle.com/en/virtualization/virtualbox/6.0/admin/swvirt-details.html
