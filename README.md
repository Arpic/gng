![](https://github.com/dantesun/gng/workflows/Validate%20Gradle%20Wrapper/badge.svg)

# GNG is Not Gradle

I worked on a lot of gradle-based projects with different gradle versions. A globally installed gradle distribution make no sense to me because I always use Gradle Wrapper. 
Keep typing `./gradlew` is cumbersome. Even worse when you have to type `../gradlew`, or `../../gradlew`.

GNG is a script that automatically search your `gradlew` when you are inside your Gradle project and execute it. 
It also provides a bootstrap function installing any Gradle wrapper version you prefer If you are creating a new Gradle project.

This is originally inspired by [gdub](https://www.gdub.rocks/) and [gradlew-bootstrap](https://github.com/viphe/gradlew-bootstrap). 
I shamelessly steal some code from them.

# How GNG installs your Gradle Wrapper?

Internally, it uses an embedded Gradle Wrapper with version 1.0 distribution. The reason use `1.0` is the small distribution package size.
You can trust the embedded gradle-wrapper.jar. It is verified by [Gradle Wrapper Validation](https://github.com/marketplace/actions/gradle-wrapper-validation).

# Usage

Just type 'gng' whenever you need to type `gradle`, then your life will be easier.

If you don't have any Gradle distribution, please don't worry. just type `gng --bootstrap`. It will create a Gradle wrapper in your current
working directory. By default, `gng` installs Gradle wrapper with version `4.8.1`. 

You can also use `gng --bootstrap [version]` to install whatever Gradle version you like. `gng --bootstrap latest` will install Gradle Wrapper with the latest Gradle version.



# Installation

## Homebrew
TODO :no_entry_sign: Please don't use this installing method.  I am still working on it.

```bash
brew install gng
```

>
>To install homebrew, visit [Homebrew Offical Site](https://brew.sh/), or excute 
>```bash
>/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
>```
>
## Installing from source

```bash
git clone https://github.com/dantesun/gng.git
cd gng
sudo ./install
```
You can also execute `sudo ./install.sh -u` to uninstall `gng`.

## Aliasing the `gradle` command
To avoid using any system wide Gradle distribution add a `gradle` alias to `gw` to your shell's configuration file.

Example *bash*:

```bash
echo "alias gradle=gng" >> ~/.bashrc
echo "export PATH=/usr/local/bin:${PATH}" >> ~/.bashrc
source ~/.bashrc
```
