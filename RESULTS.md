WHAT I DID

For this assignment, I added symbolic link symlink support to the xv6 operarting system. A symbolic link is basically a file that points to another file.
When i open a symlink, the OS automatically opens the file it points to instead. I had to add a new inode type, a new sysyem call and update the file open 
logic to follow symlinks.

I added a new inode type called T_SYMLINK. This is how xv6 knows a file is a symlink. The symlink stores the path of the target file in it's data blocks as 
a sample string.

I added a new system call symlink target, linkpath. It creates a new inode of type T_SYMLINK, writes the target path into its data block and 
adds a null terminator. 

I modified sysopen so when i open a symlink it opens the real file. it checks if the inode is T_SYMLINK reads the target path looks up the 
target and repeats in a loop for chain symlink. 

TEST RESULTS

$testsymlink
PASS: symlink created
PASS: read through symlink
PASS: loopm detected

done testsymlink 
