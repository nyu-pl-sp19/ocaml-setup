# OCaml Setup

## Installation, Build Tools, and IDEs

### Windows 10

If you are using Windows 10, I suggest to proceed as follows (this is
the setup I'll be using in class). Install Ubuntu via the Windows
Subsystem for Linux. Use e.g. the instructions in the following two
tutorials to do this:

* [Install WSL - Windows Subsystem for Linux](https://solarianprogrammer.com/2017/04/15/install-wsl-windows-subsystem-for-linux/)

* [Using the Windows Subsystem for Linux with Xfce 4](https://solarianprogrammer.com/2017/04/16/windows-susbsystem-for-linux-xfce-4/)

Then follow the installation instructions for Ubuntu below and install
everything within your Ubuntu subsystem. In particular, install Visual
Studio Code within the Ubuntu subsystem rather than as a Window app.

If you notice blurry fonts when you open applications from within
Ubuntu WSL that use the Xming X11 server (e.g. Visual Studio Code,
Emacs, etc.), then do the following steps:

1. Open the directory C:\Program Files (x86)\Xming

2. Right-click the file Xming.exe and choose "Properties" from the context menu

3. Select the tab "Compatibility" and then click "Change high DPI settings"

4. Then under "High DPI scaling override" click the checkbox "Override
   high DPI scaling behavior" and select "Application" in the drop
   down menu labeled "Scaling performed by:".

5. Then close both pop-up windows by clicking "OK"

After this, the fonts should be crisp the next time you start the X11
server. If you already have it running in the background, you'll have
to manually kill the process before you restart it. Rebooting will
also do the trick.


### Linux and MacOS

Most Linux distributions as well as homebrew on Mac OS come with
precompiled packages for OCaml. There is also a Windows
installer. However, I suggest to install OCaml
using [opam](https://opam.ocaml.org/), which is a package manager for
OCaml that makes it easy to install many other useful tools for
developing OCaml programs. 

#### Installing opam on MacOS

Make sure that you have XCode installed; [see Scala setup](https://github.com/nyu-pl-sp19/scala-setup#xcode-osx-only))

Then install opam by executing

```bash
brew install ocaml
brew install opam
```

#### Installing opam on Ubuntu [Window subsystem for Linux]:

Ubuntu 18.04 on WSL uses an older version of opam by default. To
install the latest opam version, first add the latest ppa containing the
stable version of opam:

```bash
sudo add-apt-repository ppa:avsm/ppa
sudo apt update
```
Then install the latest stable version of opam:

```bash
sudo apt install opam
```

Once you have opam installed, you can install and set up the most
recent version of the OCaml language and compiler by first executing the
following commands in a terminal:

```bash
opam init --disable-sandboxing
```

then continue with the instructions for all platforms below following the steps after `opam init` has been executed.

#### Installing opam on Ubuntu [native]

To install opam execute:

```bash
sudo apt install opam
```

#### Installing opam on other operating systems

Please read the [installation instructions of
opam](https://opam.ocaml.org/doc/Install.html) if you have another
operating system.

#### All platforms (after opam is installed)

Once you have opam installed, you can install and set up the most
recent version of the OCaml language and compiler by executing the
following commands in a terminal:

```bash
opam init
```

If you see a warning related to a missing `m4` dependency, then
install `m4` before you proceed using

```bash
brew install m4
```

respectively

```bash
sudo apt install m4
```

Then you can create a 'switch' for the most recent OCaml release by executing

```bash
opam switch create 4.07.1
eval `opam config env`
```

The installation will take a while since opam will download the
sources of the OCaml compiler and compile it from scratch. Follow
the instructions provided by the output of these commands to set up your
environment variables. Once, the installation has completed, you can
execute `ocaml`, which starts an OCaml REPL session:

```ocaml
        OCaml version 4.07.1

#
```

If you want to evaluate an OCaml expression in the REPL, you need to
terminate it by a double semicolon `;;` and then press `Enter`:

```ocaml
# 3 + 1 ;;
- : int = 4

# let x = 3 + 1 ;;
val x : int = 4

# #quit ;;
```

These double semicolons are only needed in the REPL but not in source
code files that are processed by the compiler.

In addition to the OCaml compiler and runtime, you also want to
install the OCaml library manager
[ocamlfind](http://projects.camlcity.org/projects/findlib.html), the
OCaml build tool [ocamlbuild](https://github.com/ocaml/ocamlbuild/),
and the OCaml unit testing framework
[OUnit](http://ounit.forge.ocamlcore.org/). You can do this via opam:

```bash
opam install -y ocamlfind
opam install -y ocamlbuild
opam install -y ounit
```

These tools provide similar functionality as `sbt` and `scalatest`
do for Scala.

Several IDEs have plugins for OCaml. I suggest to use
[Merlin](https://github.com/ocaml/merlin) which provides IDE support
for OCaml in common editors like Emacs and Vim. Merlin can also be
integrated into other editors and IDEs via third-party plugins,
including Atom, Sublime, and Visual Studio Code. You can install it
via opam by executing:

```bash
opam install -y merlin
```

See the installation instructions on [Merlin's project
website](https://github.com/ocaml/merlin) for further details on how
to configure various editors.

If you want a modern IDE, [Visual Studio
Code](https://code.visualstudio.com/) works well with OCaml in my
experience. Follow the installation instructions for your operating
system/distribution. For supporting OCaml, you should install the
[OCaml and Reason
IDE](https://marketplace.visualstudio.com/items?itemName=freebroccolo.reasonml)
extension. You can do this from within Visual Studio Code by selecting

```
File -> Preferences -> Extensions
```

Then search for the `vscode-reasonml` extension and install it. The
extension builds on top of Merlin which you can install via opam (see
above).

