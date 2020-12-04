# Day 15 : Application repositories

This is part of the [#LinuxUpSkillChallenge](../challenges/linux-upskill.html). Don't forget to also check out the [Official Instructions](https://github.com/snori74/linuxupskillchallenge/blob/master/15.md) and the [Reddit](https://www.reddit.com/r/linuxupskillchallenge/) posts.

  *video*

## 1. **What are repositories?**

A repository is a storage location from which your system retrieves and installs OS updates and applications. Each repository is a collection of software hosted on a remote server (usually known as mirror) and intended to be used for installing and updating software packages on Linux systems.

To check the repositories available in Ubuntu: ```vim /etc/apt/sources.list```

The name and criteria for repositories vary between distributions, but the types of repositories usually are:
 - **Main or Stable** – officially supported software. The distro maintainer provides official support for these packages. It includes every open-source package available in the default installation.
 - **Multiverse or Fusion** – unsupported, closed-source, patent-encumbered software or legal-restricted packages.
 - **Restricted, Third Party or Non-Free** – officially supported, closed-source software.
 - Distros often have unstable, testing and deprecaded repositories. Personal and various community-maintened repositories are also common.

Check more about [licenses here](https://opensource.org/licenses).

## 2. **What are packages?**

A package refers to a compressed file archive containing all of the files that come with a particular application. The files are usually stored in the package according to their relative installation paths on your system.

- Show information about a package: ```apt-cache show package```

The rules and criteria (could be technical, could be ideological) for a package to be eligible to one or other repository is what gave birth to so many different Linux distributions.

- Show the name of each package APT knows (but not necessarily is available to
download, installable or installed): ```apt-cache pkgnames```

A distro is basically an operating system made from a software collection that is based upon the Linux kernel and a package management system. The software is usually adapted to the distribution and then packaged into software packages by the distribution's maintainers.

- Show whether a package is installed and up to date: ```apt-cache policy package```

```
$ apt-cache policy nano
nano:
  Installed: 4.8-1ubuntu1
  Candidate: 4.8-1ubuntu1
  Version table:
 *** 4.8-1ubuntu1 500
        500 http://us-east-1.ec2.archive.ubuntu.com/ubuntu focal/main amd64 Packages
        100 /var/lib/dpkg/status
```

Linux follows the phylosophy that software is easier to maintain when modular (in many pieces) as opposed to monolithic (one big piece). This idea makes it possible that each package can be maintained by a different developer. Also, the division into smaller modules (focused on a limited set of functionalities) allows other packages to make use of it for their own purposes too.

There is no reinventing the wheel, so it's very common for packages to interact with other packages. A **dependency** occurs when one package depends on another to function.

- Show dependencies for a package: ```apt-cache depends package```

```
$ apt-cache depends nano
nano
  Depends: libc6
  Depends: libncursesw6
  Depends: libtinfo6
  Conflicts: <pico>
  Breaks: nano-tiny
  Suggests: hunspell
  Replaces: nano-tiny
  Replaces: <pico>
```

- Show packages that depend on a particular package: ```apt-cache rdepends package```

```
$ apt-cache rdepends nano
nano
Reverse Depends:
  usrmerge
  ubuntu-standard
  ubuntu-standard
  junior-writing
  dms-core
  dms
```

## 3. **Enabling known repos**

```
sudo add-apt-repository universe
sudo add-apt-repository multiverse
sudo apt update
```

## 4. **Add an extra repo**

You can add repositories by adding the apt repository line to the end of the sources.list file: ```deb http://mirror-address/ <repository-name>```

```
deb http://security.ubuntu.com/ubuntu focal-security multiverse
```

**ATTENTION!** It's always a good idea to backup a configuration file like sources.list before you edit it: ```sudo cp /etc/apt/sources.list /etc/apt/sources.list.backup```

Personal Package Archives (PPA) is a service that allows users to upload source packages that are built and published as an apt repository.

```
sudo add-apt-repository ppa:<repository-name>
```

Don't forget to ```sudo apt update``` before installing packages, so you can use the repositories enabled.


For more detail on how I did each day, check out my log on [Reddit](https://www.reddit.com/user/livia2lima). Follow me on [Twitter](https://twitter.com/search?q=%23LinuxUpSkillChallenge%20%40livialimatweets&src=typed_query&f=live) for daily updates.
