Hello, I am Moteen Shah from VJTI, Mumbai. This is the first introduction with opensource contributions. After going through a vast array of Organisations and learning about their projects, I finally found **libvirt** and virtual machines most interesting.

## Getting Started

I joined the IRC channel, subscribed to the libvirt mailing list, and began digging more into the project. I began tackling bitsized issues and learned about the project after discussing it with mentors on mail. And now I'm writing this blog to summarise my journey.

By completing a portion of [this](https://gitlab.com/libvirt/libvirt/-/issues/7) issue, I began to familiarise myself with the code base.
In addition, after speaking with mentors about the project, I was assigned a heading to work on.
Because my project code was meant to end up there, I first became acquainted with the job code.

### 1. Building libvirt
 First I followed the [compiling blog](https://libvirt.org/compiling.html) section on libvirt's website, which involved installing all dependencies and building libvirt. I was able to successfully build and test its working on my PC. 

### 2. Submitting my First Patch 
- I had experience with sending PRs for solving issues on Github, but *email-based patch* system was relatively new for me.
  Looking at the [resources](https://libvirt.org/hacking.html) given by libvirt on their website, I began setting it up and learning how to send a patch.
- Being not very well versed with the codebase at that time, I decided to fix bitsized issue and send a patch for it.
- After correcting few errors and learning patch system, I finally sent my first patch to libvirt. It was reviewed by the mentors and based on their suggestions a couple more patches which got merged, here's the [link](https://listman.redhat.com/archives/libvir-list/2022-April/230013.html)

### 3. The Storage Driver
* Currently, libvirt support job cancellation and progress reporting on domains. That is, if there's a long running job on a domain, e.g. migration, libvirt reports how much data has already been transferred to the destination and how much still needs to be transferred. However, libvirt lacks such information reporting in storage area, to which libvirt developers refer to as the storage driver. 

* I dug into the libvirt storage driver to find a solution. Here are several key theories I came upon:
    * Libvirt provides storage management on the physical host through storage pools and volumes.
    * A storage pool is a quantity of storage set aside by an administrator, often a dedicated storage administrator, for use by virtual machines. Storage pools are divided into storage volumes either by the storage administrator or the system administrator, and the volumes are assigned to VMs as block devices.
    * Cgroup funcs : Cgroups allow you to allocate resources — such as CPU time, system memory, network bandwidth, or combinations of these resources — among user-defined groups of tasks (processes) running on a system. 
    * I found these cgroup function as a good reference point.
    * Some of available Subsystems in Red Hat Enterprise Linux: 
        * 'blkio' — this subsystem sets limits on input/output access to and from block devices such as physical drives (disk, solid state, or USB).
        * 'cpu' — this subsystem uses the scheduler to provide cgroup tasks access to the CPU.
        * 'cpuacct' — this subsystem generates automatic reports on CPU resources used by tasks in a cgroup.
        * 'cpuset'  — this subsystem assigns individual CPUs (on a multicore system) and memory nodes to tasks in a cgroup.
        * 'devices' — this subsystem allows or denies access to devices by tasks in a cgroup.
        * 'freezer' — this subsystem suspends or resumes tasks in a cgroup.

### 4. The Job Code   
* The task code under src/hypervisor/ is the most crucial section of all; this is intended to be where the fix should end up.
* I became acquainted with the code and gained a general understanding of what is needed to be done for the project.


