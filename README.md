# Build Wget from Source

Wget is an utility for downloading of files non-interactively. 

That means that you can download files in the background.

The name comes from World Wide Web and get.

It was made by our neighbour Hrvoje Nikšić in 1996.

This guide illustrates how the program can be compiled from source. I've tried all this on Ubuntu 24.04.2 LTS on WSL.

This is for educational pursposes only. Ubuntu and many other distributions already come with it installed.

## Install build dependencies

```bash
sudo apt update
sudo apt install build-essential git autoconf automake libssl-dev \
    libidn2-0-dev libpsl-dev libgnutls28-dev pkg-config \
    gettext texinfo
```
![screenshot](./screenshots/01.png)


> - build-essential - compiler and tools
> - autoconf, automake, pkg-config - other build tools
> - libssl-dev, libgnutls28-dev - libs for https support
> - libidn2-0-dev, libpsl-dev - support for internation domain names and suffixes
> gettext, texinfo - docs and translations


## Clone repo

```bash
git clone https://github.com/mirror/wget.git
cd wget
```
![screenshot](./screenshots/02.png)


## Preparing build system
```bash
./bootstrap
```

>Bootstrap will probably fail

![screenshot](./screenshots/02-1.png)

>Install required additional packages

![screenshot](./screenshots/02-2.png)

>This will run autoreconf and prepare configure file

>Also, a repo from savannag.gnu.rog will start to download
![screenshot](./screenshots/03.png)

> But it's too big and takes a lot of time
![screenshot](./screenshots/04.png)

> So, let's take only a part of it, using --depth=1 option
![screenshot](./screenshots/05.png)

> Let's clone from other faster repo
![screenshot](./screenshots/06.png)

> Continue building
![screenshot](./screenshots/07.png)

> Autoconf failed, so we need to install other packages
![screenshot](./screenshots/08.png)

>Install additional packages
![screenshot](./screenshots/09.png)

>Continue bootstrap
![screenshot](./screenshots/10.png)

>Finished, now you can continue with ./configure
![screenshot](./screenshots/11.png)


## Configure build
```bash
./configure --with-ssl=openssl
or 
./configure --with-ssl=gnutls
```
![screenshot](./screenshots/12.png)


## Compile the code
```bash
make -j$(nproc)
```
![screenshot](./screenshots/13.png)

## List all files
![screenshot](./screenshots/14.png)
### Go to src directory
And see the compiled wget executable, marked as green
![screenshot](./screenshots/16.png)

## Run the compiled wget
![screenshot](./screenshots/15.png)

## Compare versions of the compiled and already installed wget
![screenshot](./screenshots/19.png)
![screenshot](./screenshots/20.png)



