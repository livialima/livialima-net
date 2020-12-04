# Day 17 : Install from the source

This is part of the [#LinuxUpSkillChallenge](../challenges/linux-upskill.html). Don't forget to also check out the [Official Instructions](https://github.com/snori74/linuxupskillchallenge/blob/master/17.md) and the [Reddit](https://www.reddit.com/r/linuxupskillchallenge/) posts.

*video*

## 1. **Binaries vs Source**

Binaries contain computer-readable version of the application, meaning it is compiled.
The binary files are pre-compiled, and often customised by your distro. A big part of what package managers do (like apt), is to identify and install any required dependencies, making it easier to install new packages.

Source contains human-readable version of the application, meaning it has to be compiled before it can be used. The source release is the raw, uncompiled code. The dependency-check can be a bit tricky thing to resolve manually.

## 2. **Get the source**

When installing packages with a package manager (like apt), the binaries are already compiled and ready to run on your distribution. Now, installing from source, you have to get the source files aggregated and compressed into that tarball.

Download and uncompress the tarball. You may also enter the program uncompressed directory to work from there.

```
wget -v https://nmap.org/dist/nmap-7.70.tar.bz2
tar jxvf nmap-7.70.tar.bz2
cd nmap-7.70
```

## 3. **Prepare the environment**

Unix/Linux programs are often written in C, so we’ll usually need a C compiler (among other tools) to build them. So having the necessary packages to build a program is the first requirement.

The build-essential is a package that contains references to numerous packages needed for building software in general.

```
sudo apt install build-essential
```

## 4. **Configure the software**
The ```configure``` script responsibility is to get everything ready to build the software on your system. The configure script will check dependencies and return which packages are required to continue, if they are not installed yet.

```
./configure
```

## 5. **Build the software**

With the configure done, invoke ```make``` to build the software. This runs the **Makefile**: a script for compiling or building the "binaries", the executable portions of a package. The sequence defined in a Makefile launches cc or gcc (actually a preprocessor, a C/C++ compiler, and a linker). This process converts the source into the binaries.

Invoking ```make``` generally builds all the necessary executable files for the package in question.

```
make
```

## 6. **Install the software**

The binaries are built and ready to run, the files can be copied to their proper destinations within the system. This process is called installation. The ```make install``` command will perform this step as defined in the **Makefile**.

Be aware that ```make install``` may need to be invoked as root, especially when moving the binaries over to the /usr/bin or /usr/local/bin directories. Using make as an ordinary user without root privileges will likely result in write access denied error messages because you lack write permission to system directories.

```
make install
```

Check out this article for more details: [The magic behind configure, make, make install](https://thoughtbot.com/blog/the-magic-behind-configure-make-make-install)

For more detail on how I did each day, check out my log on [Reddit](https://www.reddit.com/user/livia2lima). Follow me on [Twitter](https://twitter.com/search?q=%23LinuxUpSkillChallenge%20%40livialimatweets&src=typed_query&f=live) for daily updates.
