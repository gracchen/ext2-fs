# ext2-fs
Practice with file systems, data structures, and self-learning with documentation

This program generates a 1 MiB ext2 file system, cs111-base.img, that
contains 2 directories (root and root/lost+found), 1 regular file
(root/hello-world), and 1 symlink (root/hello that points to hello-world).

## Building

To build this program, navigate to the directory containing this README and type:
   make

## Running

To generate the file system image:
   ./ext2-create
   
To mount the image:
   mkdir mnt
   sudo mount -o loop cs111-base.img mnt
   cd mnt

Example output of 'ls -ain' inside mounted file system:
total 7
  2 drwxr-xr-x 3    0    0 1024 Nov 23 23:59 .
302 drwxr-xr-x 5 1000 1000 4096 Nov 23 23:59 ..
 13 lrw-r--r-- 1 1000 1000   11 Nov 23 23:59 hello -> hello-world
 12 -rw-r--r-- 1 1000 1000   12 Nov 23 23:59 hello-world
 11 drwxr-xr-x 2    0    0 1024 Nov 23 23:59 lost+found

Note that the properties of ".." is not, as expected, the same as
that of "." because this file system was mounted onto my machine
and the "root" folder is not the actual root but just another
subdirectory. Thus "." points to "root" and ".." points to "mnt".

## Cleaning up

To unmount, first navigate back to the parent directory of "mnt",
then umount:
   cd ..
   sudo umount mnt

To remove mount directory:
   rmdir mnt

To clean up binary files:
   make clean
