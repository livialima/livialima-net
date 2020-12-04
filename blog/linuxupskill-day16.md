# Day 16 : Archive files

This is part of the [#LinuxUpSkillChallenge](../challenges/linux-upskill.html). Don't forget to also check out the [Official Instructions](https://github.com/snori74/linuxupskillchallenge/blob/master/16.md) and the [Reddit](https://www.reddit.com/r/linuxupskillchallenge/) posts.

*video*

## 1. **What is archiving?**

Archiving is the process by which information is securely stored for longer periods of time.

The Linux “tar” stands for **tape archive**, which was used by a large number of Linux/Unix system administrators to deal with tape backup. Remember tapes? Well, they are not dead. In fact, [they are very much alive](https://youtu.be/z4DP0Lg-qpw).

The tar command rips a collection of files and directories into an archive file (often combined with a compression method) commonly called **tarball** or tar.

## 2. **What is compressing?**

File compression is used to reduce the file size of one or more files. When a file or a group of files is compressed, the resulting "archive" often takes up 50% to 90% less disk space than the original file(s).

The most used tools for compression in Linux are gzip, bzip2, and zip.

  - Compress a file, replacing it with a gzipped compressed version: ```gzip file.ext```
  - Uncompress a file, replacing it with the original uncompressed version: ```gzip -d file.ext.gz```

```
$ du -h big-file*
65M	big-file

$ gzip big-file
$ du -h big-file*
60M	big-file

$ gzip -d big-file.gz
$ du -h big-file*
65M	big-file

$
```

## 3. **Your first tar ball**

Options:
 - **c**, --create : Create a new archive.
 - **t**, --list : List  the contents of an archive.
 - **f**, --file=ARCHIVE : Use  archive  file or device ARCHIVE.
 - **x**, --extract, --get : Extract  files  from  an archive.
 - **j**, --bzip2 : Filter the archive through bzip2.
 - **z**, --gzip, --gunzip, --ungzip : Filter the archive through gzip.
 - **v**, --verbose : Verbosely list files processed.

Creating tarballs:
  - Create an archive from files: ```tar cf target.tar file1 file2 file3```
  - Create a gzipped archive: ```tar czf target.tar.gz file1 file2 file3```

```
$ du -h file*
8.0K	file1
36K	file2
12K	file3

$ tar cf target.tar file1 file2 file3
$ du -h file* target*
8.0K	file1
36K	file2
12K	file3
60K	target.tar

$ tar czf target.tar.gz file1 file2 file3
$ du -h file* target*
8.0K	file1
36K	file2
12K	file3
60K	target.tar
16K	target.tar.gz

$
```

## 4. **Extracting files**

  - List the contents of a tar file: ```tar tvf source.tar```
  - Extract a (compressed) archive into the current directory: ```tar xf source.tar[.gz|.bz2|.xz]```
  - Extract a (compressed) archive into the target directory: ```tar xf source.tar[.gz|.bz2|.xz] -C directory```

For more detail on how I did each day, check out my log on [Reddit](https://www.reddit.com/user/livia2lima). Follow me on [Twitter](https://twitter.com/search?q=%23LinuxUpSkillChallenge%20%40livialimatweets&src=typed_query&f=live) for daily updates.
