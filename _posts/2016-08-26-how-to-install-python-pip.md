---
layout: single
title: How to Install Python Pip
modified:
categories: "python"
excerpt: The right way to install Python Pip on Ubuntu, CentOS, Mac, and Windows
tags: [pip, python, ubuntu, centOS, Mac, windows]
image:
  feature:
date: 2016-08-26
---

Python [pip](https://en.wikipedia.org/wiki/Pip_(package_manager)) is a great package manager for python which helps in installing and managing python packages which can be found on [PyPI](https://pypi.python.org/pypi)

**Note:** Python 2.7.9 and later and Python 3.4 and later include pip by default so you do not have to install it.

If you have a new machine you probably want to update your distribution packages.


## Install using get-pip.py

This method works on all Operating Systems..

```bash
curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py" && python get-pip.py
```


## Install pip on Ubuntu

```bash
sudo apt-get update && sudo apt-get upgrade
sudo apt-get -y install python-pip
```

## Install pip on CentOS

Lets install pip using yum.

```bash
rpm -iUvh http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-5.noarch.rpm
yum -y update
yum -y install python-pip
```


## Install pip on Mac (OS X)

pip is available on OS X via easy_install

```bash
sudo easy_install pip
```

In case you do not have python on your mac, you can use brew to install and pip will come bundled with it.

**Install brew**

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

**Install python**

```bash
brew install python
```

## Install pip on Windows

The best method to install pip on windows is via get-pip.py which is mentioned above.


## Verify Installation

```bash
pip --version
```

You should see something like this.
**pip 8.1.2 from /Library/Python/2.7/site-packages (python 2.7)**

Incase these steps do not work for you, do mention them in the comments below or tweet me on twitter and I would be eager to help you.
