meric
======

A package manager utility for pacman repositories and the AUR. meric
is a fork of famous "meric".  meric only handles tasks that may
require access to the AUR or are required by tasks that do.
For everything else, simply use pacman.

Installation
------------

The easiest way to install meric is from the AUR. Also you can
use provided PKGBUILD.If you want to install it manually, simply
run these commands as root :

  # install -m 755 meric /usr/bin/meric
  # mkdir /usr/share/meric && install -m 644  \
  {meric.lang,COPYING,README,ChangeLog} /usr/share/meric/
  # install -m 644  meric.conf /etc/meric.conf
  # mkdir /usr/share/zsh/site-functions && install -m 644 \
  meric.zshcomp /usr/share/zsh/site-functions/_meric
  # mkdir /etc/bash_completion.d && install -m 644 meric.bashcomp \
  /etc/bash_completion.d/meric

Usage:
------

meric's usage is similar to pacman, but there are a few differences.
One is that meric only supports the following actions and options:

### Actions

 * -S
   install
 * -Ss(q)
   search (quietly)
 * -Si
   get info about package
 * -Sc(c)
   delete cached files including ones from meric (delete more)
 * -S(y)u
   update (get new cache data)
 * -a
   only preform AUR-based actions. can be used with -S,-Ss(q) actions
 * -G
   download and extract aur tarball only
 * -U
   make local PKGBUILD with AUR support
 * -v
   print version info

### Options

 * --quiet
   same as the optional 'q' in -Ss(q)
 * --ignore
   a package to ignore
 * --noconfirm
   don't ask any questions
 * --sign
   sign package
 * --asdeps
   install packages as dependancies
 * --noedit
   don't ask if the user wants to edit AUR files
 * --auronly
   only preform AUR-based actions
 * --devel
   add all VCS packages to the list of packages to be updated
 * --skipinteg
   skip makepkg's integrity checks
 * --keeptar
   copy tarballs to 'SRCPKGDEST' specified in '/etc/makepkg.conf'
 * --cleandeps
   clean dependencies after package building process
 * --skip-repo
   skip comma-separated list of repos
 * -h, --help
   print a usage message
 * --version
   print version info
 * --
   assume all of the following arguments are packages

Another difference is the inclusion of an interactive mode. Running
meric with a package name (and options) but without specifying an
action will start interactive mode. In this mode a numbered list of
search results for the given package is displayed, and one or more
numbers are requested. Entering the coresponding numbers will
install those packages.

One last small difference is that, if sudo is installed, meric will
automatically prompt for you password when it needs. For security
reasons it is recommended you install and configure sudo properly,
and then run meric as a normal user, not as root. For more
information on sudo, take a look at [the ArchWiki's Sudo article]
[aw-sudo].

### Examples

To install a package:

	meric -S <package>

To search for a package:

	meric -Ss <keyword>

Install without confirmation:

	meric -S --noconfirm <package>

Search and install using interactive mode:

	meric <package>

Build and install package then remove dependancies:

	meric -Sa --cleandeps <package>

Search for a package, colorize results, and display in less:

	meric -Ss --color <package> | less -R

Configuration
-------------

Meric uses its own configuration file located as '/etc/meric.conf'
or '$HOME/.config/meric/meric.conf'

In meric.conf users are allowed to specify mainly two things:
 * makepkg options
   specified makepkg options are passed to main 'meric' script
   and treated just like 'makepkg --option'

 * meric options
   specified meric options are passed to main 'meric' script and
   treated just like 'meric --option'. For more info please look
   at meric.conf file.

meric reads the following settings from pacman.conf:

 * IgnorePkg
 * DBPath

Both of these settings have the same effect on meric's operation as
they do on pacman. Obviously, if pacman is called it will read any
settings it needs.

If you want to use another pacman configuration file instead of the
default one, you can use your own pacman.conf located in
'$HOME/.config/meric/meric.conf'. /etc/pacman.conf will be ignored
in this case.

If you want to edit a file, the $EDITOR environment variable is used.
If editor is not set, meric will use vi.


diffpac
-------

If you've been using yaourt and just can't stop because of
pacdiffviewer then you should take a look at diffpac, a stand-alone
pacdiffviewer fork. If you don't like it, or want some of the other
features that that yaourt provides, you can always use both meric
and yaourt. Since meric is designed to only do what it needs to do,
it requires you to use at least pacman as well. There's no reason you
can't use it with something else (such as yaourt) too.

Translations
------------
Meric has locale support in form of bash scripts.
For the sake of keep package and its dependencies minimal; only one
text file (in bash script format) is used to hold and provide all translations

Note to Translators
-------------------
Please use the meric.lang as a template. Do not change the format.
Just translate lines after "=" equal sign and do not change variables format i.e:

 *Text to translate:
   ERROR11="Package \`$package' does not exist on aur."

 *Translated text:
   ERROR11="\`$package' paketi AUR üzerinde yok."

Send your translations (including your names and e-mails) to my e-mail adress shown below:

Authors
-------

 * Atilla ÖNTAŞ <tarakbumba@gmail.com>

 - packer :
  * Matthew Bruenig <matthewbruenig@gmail.com> <https://github.com/bruenig/packer>

 - Some code, this README.md, zsh-completion and bash-completion :
  * DeedleFake <YissZev@BeckForce.com> <https://github.com/DeedleFake/packer>

[aw-sudo]: http://wiki.archlinux.org/index.php/Sudo
