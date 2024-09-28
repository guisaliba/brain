**Amazon Elastic Compute Cloud (EC2)** web service that provides safe and scalable computation resources in the cloud, providing virtual machines called **instances**.

**Amazon Machine Image (AMI)** is a root-volume image for deploying EC2 instances, it usually contains the operational system of the machine, its arch (ARM x32, x64 etc) and other additional pre-installed software.

EC2 are the live instantiations of AMIs, just like a cake is a live demo of its receipt, it works just like the class-object relationship. When a new instance is created, AWS allocates a VM which is executed in a hypervisor.
Following, the AMI is then copied to the root-volume, to start booting it.
![[49iNf52V_SDOuOmw_0SbtA-3_O3ILWWX2.png]]AMIs are reusable, you may choose one based in Linux and configure an HTTP server on it, apps and other software, and create many instances over it. There is also the possibility of creating an image from a running instance, and run a new instance from this newly created image, creating a perfect copy of the current instance.

There are many different types of instances, for different purposes and use cases.

## Lifecycle
