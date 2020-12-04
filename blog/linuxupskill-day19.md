# Day 19 : Links and shortcuts

This is part of the [#LinuxUpSkillChallenge](../challenges/linux-upskill.html). Don't forget to also check out the [Official Instructions](https://github.com/snori74/linuxupskillchallenge/blob/master/19.md) and the [Reddit](https://www.reddit.com/r/linuxupskillchallenge/) posts.

*video*

## 1. **Inodes**

The inode (index node) is a data structure in a Unix-style file system that describes a file-system object such as a file or a directory. Each inode stores the attributes and disk block locations of the object's data, such as the access mode (read, write, execute permissions), ownership, file type, file size, group, number of links, etc.

Each inode has an inode number, which is unique within a file system. The same inode number might appear in more than one file system. However, the file system ID and inode number combine to make a unique identifier, regardless of how many file systems are mounted on your Linux system.

The -i (inodes) option of the df command instructs it to display its output in numbers of inodes:

```
$ df -i
Filesystem      Inodes  IUsed  IFree IUse% Mounted on
/dev/root      1024000 113229 910771   12% /
devtmpfs        124235    313 123922    1% /dev
tmpfs           125263      2 125261    1% /dev/shm
tmpfs           125263    500 124763    1% /run
tmpfs           125263      3 125260    1% /run/lock
tmpfs           125263     18 125245    1% /sys/fs/cgroup
$
```

To see the inode number of a file, we can use ls with the -i (inode) option:

```
$ ls -i file
1056790 file
$
```

## 2. **Touch**

In its default usage, ```touch``` is the equivalent of creating or opening a file and saving it without any change to the file contents. Instead it simply updates the dates associated with the file or directory.

When you create a file in your file system, such as by issuing the following command:

```
touch file
```

The data for the actual file is stored in a data block. The permissions for the file, GroupID, OwnerID, size of file, and times relating to modification and access, is stored in the inode block.

## 3. **Stat**

Display that metadata information from the inode:

```
$ stat file
  File: file
  Size: 0         	Blocks: 0          IO Block: 4096   regular empty file
Device: 28h/40d	Inode: 1056790     Links: 1
Access: (0664/-rw-rw-r--)  Uid: ( 1000/   livia)   Gid: ( 1000/   livia)
Context: unconfined_u:object_r:user_home_t:s0
Access: 2020-12-02 11:23:48.164775122 -0300
Modify: 2020-12-02 11:23:48.164775122 -0300
Change: 2020-12-02 11:23:48.164775122 -0300
 Birth: 2020-12-02 11:23:48.164775122 -0300
$
```

## 4. **Soft links**

Symbolic links (or soft links) are similar to shortcuts in other operating systems. They are not the actual file, or data block, instead they are simply an inode that links to a data block of another file.

```
ln -s file link
```

The new soft link you created will indicate which regular file is pointing to:

```
$ ls -li file symlink
1056790 -rw-rw-r--. 2 livia livia 2769 Dec  2 11:30 file
1056858 lrwxrwxrwx. 1 livia livia    4 Dec  2 11:28 symlink -> file
```

Note the inode number is different:

```
$ stat file
  File: file
  Size: 2769      	Blocks: 8          IO Block: 4096   regular file
Device: 28h/40d	Inode: 1056790     Links: 1
...
$ stat symlink
  File: symlink -> file
  Size: 4         	Blocks: 8          IO Block: 4096   symbolic link
Device: 28h/40d	Inode: 1056858     Links: 1
Access: (0777/lrwxrwxrwx)  Uid: ( 1000/   livia)   Gid: ( 1000/   livia)
...
$
```

If you use stat on a file that is actually a symbolic link, it will report on the link. If you wanted stat to report on the file that the link points to, use the ```-L```. Note the inode number is the same:

```
$ stat -L file
  File: file
  Size: 2769      	Blocks: 8          IO Block: 4096   regular file
Device: 28h/40d	Inode: 1056790     Links: 1
Access: (0664/-rw-rw-r--)  Uid: ( 1000/   livia)   Gid: ( 1000/   livia)
...
$ stat -L symlink
  File: symlink
  Size: 2769      	Blocks: 8          IO Block: 4096   regular file
Device: 28h/40d	Inode: 1056790     Links: 1
Access: (0664/-rw-rw-r--)  Uid: ( 1000/   livia)   Gid: ( 1000/   livia)
...
$
```

If the link is to be deleted, the original file remains intact. If the original file is deleted, the link will be hanging, pointing to nothing.

## 5. **Hard links**

Hard links do not create a separate inode, that is they simply insert an entry into the directory file that points to the same inode of the file it is linked to.

```
ln file link
```

The new hard link you created is indistinguishable from a regular file:

```
$ ls -li file hardlink
1056790 -rw-rw-r--. 2 livia livia 2769 Dec  2 11:30 file
1056790 -rw-rw-r--. 2 livia livia 2769 Dec  2 11:30 hardlink
```

Note the inode number is the same:

```
$ stat file
  File: file
  Size: 2769      	Blocks: 8          IO Block: 4096   regular file
Device: 28h/40d	Inode: 1056790     Links: 1
...
$ stat hardlink
  File: hardlink
  Size: 2769      	Blocks: 8          IO Block: 4096   regular file
Device: 28h/40d	Inode: 1056790     Links: 1
...
$
```

If you delete the original file, the link will still contain the original file content, as that's not removed until there is one hard link pointing to it.

## 6. **Alias**

An alias is a short cut command to a longer command. Users may type the alias name to run the longer command with less typing.

Without arguments, ```alias``` prints a list of defined aliases:

```
$ alias
alias grep='grep --color=auto'
alias ll='ls -l --color=auto'
alias ls='ls --color=auto'
$
```

A new alias is defined by assigning a string with the command to a name.

```
alias vi='vim'
```

For more detail on how I did each day, check out my log on [Reddit](https://www.reddit.com/user/livia2lima). Follow me on [Twitter](https://twitter.com/search?q=%23LinuxUpSkillChallenge%20%40livialimatweets&src=typed_query&f=live) for daily updates.
