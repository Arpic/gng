![](https://github.com/dantesun/gng/workflows/Validate%20Gradle%20Wrapper/badge.svg)

# GNG is merging with gdub

I am working on merge gng and gdub together after talked with the author of `gdub`. `gng` will still be kept as a symbol
link to `gw`.

# GNG is Not Gradle

GNG is a script that automatically search your `gradlew` when you are inside your Gradle project and execute it. It also
contains an official Gradle wrapper. You can create gradle projects from scratch without installing Gradle.

This is originally inspired by [gdub](https://www.gdub.rocks/)
and [gradlew-bootstrap](https://github.com/viphe/gradlew-bootstrap).

## What's the problem?

I worked with a lot of gradle projects, every project has its own Gradle Wrapper. So the global installed one, normally
installed with `brew install gradle`, is seldom used. In fact, the global installed gradle’s version may conflict with
the project you are working on and some weird and unexpected building failures may happen. **The best practice is always
using Gradle Wrapper comes with a project.** It's more better to not keep a copy of global available gradle.

But keep typing `./gradlew` is cumbersome. It becoms even worse when you have to type `../gradlew`, or `../../gradlew`.

I am a heavy Gradle user, I always need to create a new Gradle project for trying some new ideas, without the globally
installed gradle , it is not possible installing Gradle Wrapper into a brand-new project.

You might interest in these discussions.
>
> Quoted from [gdub](https://gdub.rocks)
>
> - [Issue Gradle-2429](http://issues.gradle.org/browse/Gradle-2429)
> - [Spencer Allain's Gradle Forum Post](http://gsfn.us/t/33g0l)
> - [Phil Swenson's Gradle Forum Post](http://gsfn.us/t/39h67)
>

# Usage

Just type `gw` whenever you need to type `gradle` or `gradlew`, then your life will be easier.

If you don't have any Gradle or Gradle Wrapper installed, please don't worry. just type `gng wrapper`. It will create a
Gradle wrapper in your current working directory.

## 'gng' and 'gw'

There are two commands `gw` and `gng`. They both behave exactly like `gradlew`.

* `gw` is originally from [gdub](http://gdub.rocks) and shorter than `gng`. It's easy to type and good for daily use.
* `gng` is the new name, and provides more features than `gw`. For example, `gng wrapper` can generate a copy of Gradle
  Wrapper for you, type `gng wrapper -h` for details.

```bash
gng wrapper -h
Generates a Gradle Wrapper
Usage: gng wrapper [-v|--version <arg>] [-t|--distribution-type <arg>] [-m|--mirror <arg>] [-h|--help] [ -d|--destination-dir <arg>
	-v, --version: Gradle Version (default: 'latest', version information is from https://services.gradle.org/versions/current, visit https://services.gradle.org/versions/all for all available versions)
	-t, --distribution-type: Gradle Distribution Type (default: 'all')
	-m, --mirror: Gradle Distribution Mirror URL Prefix(Optional with no default value, The url prefix replaces https://services.gradle.org/distributions/)
	              It replaces the whole distributionUrl except the file part in a URL. For example, if specify '-m "https://example.com/gradle/"', then
	              "https://services.gradle.org/distributions/gradle-6.8-all.zip" will become "https://example.com/gradle/gradle-6.8-all.zip"
	-d, --destination-dir : Your Gradle project root directory. (default: 'Your current working directory retrieved using ${PWD}')
	-h, --help: Prints help
```

Please note that `gng wrapper` OVERRIDES the original command `gradle wrapper` that executes Gradle Wrapper task. If you
want to execute the Gradle wrapper task instead, please type `gw wrapper`.

Example: The following command will create a directory 'test' and install a copy of Gradle Wrapper with the latest
version Gradle.

```bash
gng wrapper -d test
```

It will output like this(version number may vary as time goes by):

```bash
Fetching the latest Gradle version from services.gradle.org

The latest Gradle version is 6.8.1

Installing Gradle Wrapper in test. (version=6.8.1, distributionType=all, mirrorUrl=<Not Specified>)
```

## More examples

1. `gng wrapper` will silently upgrade your existing Gradle Wrapper to the latest version
2. `gng wrapper -v 4.8.1` will silently set your existing Gradle Wrapper to the version 4.8.1
3. `gng wrapper -t all` will silently set your existing Gradle Wrapper to the latest version with Gradle source code
   archive(gradle-xxx-all.zip).
4. `gng wrapper -v 4.2.1 -m 'http://example.com/gradle/` will set your Gradle version to 4.2.1 and distributionUrl
   to `http://example.com/gradle/gradle-4.2.1-bin.zip`
5. `gng wrapper -v 4.2.1 -t all -m 'http://example.com/gradle/` will set your Gradle version to 4.2.1 and
   distributionUrl to `http://example.com/gradle/gradle-4.2.1-all.zip`

# Installation

## Homebrew (TODO)

I am still working on it ...

## Installing from source

```bash
git clone https://github.com/dantesun/gng.git
cd gng
sudo ./install.sh
```

## Aliasing the `gradle` command

To avoid using any system wide Gradle distribution add a `gradle` alias to `gw` to your shell's configuration file.

Example *bash*:

```text
echo "alias gradle=gng" >> ~/.bashrc
echo "export PATH=/usr/local/bin:${PATH}" >> ~/.bashrc
source ~/.bashrc
```

## install.sh usage

```bash
sudo ./install.sh [-fhsu]

Install gng from git source tree. See http://github.com/dantesun/gng for details.

-u uninstall
-f re-install
-h usage
-s check for update
```

examples:

1. `./install.sh -f` will re-install everything
2. `./install.sh -s` will check for latest updates from remote master
3. `git reset --hard && git pull` will keep your copy to the latest

# How does GNG install Gradle Wrapper?

It copies the embedded Gradle Wrapper to your project directly. You can trust the embedded gradle-wrapper.jar. It is
verified
by [Gradle Wrapper Validation](https://github.com/marketplace/actions/gradle-wrapper-validation) ![](https://github.com/dantesun/gng/workflows/Validate%20Gradle%20Wrapper/badge.svg)
.
