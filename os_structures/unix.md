# The Unix Time-Sharing System

* **Key idea:** File-system interface that enables use by multiple users, a simplified device interface, and a user-shell with composable programs
* Written in C (simple to use)
* Can administer system within the system, as well as write new programs
* Key features:
  1) File-system (interface to persistent storage) 
     * Ordinary files, directories and `/dev`
       * `/dev`: read and write to IO devices
       * Advantages: (1) similar to file IO, (2) can pass device to a program, (3) can protect devices with file permissions
     * Mount/Unmount filesystems
     * Permissions
       * `setuid` lets files have special permissions
       * super-user has permissions for all
     * No filesystem locks (unecessary and insufficient)
  2) Processes
     * text, data and then stack segments
     * pipes and file descriptors abstract communication (like file IO)
  3) Shell
     * Can call programs from a shell
     * Pipes to connect programs, and filter
     * Backgrounding
  4) Traps
* Lessons
  * Simplicity is key
  * Internal requirements led to good design, rather than any particular customer
  * Designed for programmers, which makes it capable for more users as an interactive system (versus batch)
  * Size constraints led to simplicity in the design

