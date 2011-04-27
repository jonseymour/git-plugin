NAME
====
git-pm - a plugin manager for git extensions

DESCRIPTION
===========
The initial deliverable of the project will be a plugin architecture proposal. The intent of this deliverable is to create specifications
that will allow plugin authors to create descriptors for their plugins that will be sufficient to enable git-pm to locate an appropriate
package manager and delegate installation of the plugin to that package manager.

In parallel to this deliverable, a plugin manager interface (git-pm) will be developed. Such an interface will manage git plugins on 
behalf of git by delegating to whatever package-managers are available and installed on the platform.

PRINCIPLES
==========
* define a repository layout specification
* define a plugin descriptor (using the git config syntax)
* package manager agnostic repo and plugin specifications
 * perhaps define a pluggable plugin manager interface
* support for:
 * existing contrib/ directory
 * existing git patterns for finding and using extensions
 * man pages
 * plugin specific configuration help
 * bash completions
 * scripts
* build support:
 * for documentation, archives
* layers
 * repo, plugin descriptors
 * tool interface specifications 
 * tool implementations
 * global plugin registry and repository

INTENDED SCENARIOS
==================

Installation and Removal
------------------------
There is completely understandable resistance to YAPM - yet another package manager. This is not the goal of git-pm. In particular, git-pm will delegate platform-specific build
and deployment concerns to platform-specific package managers such as apt-get, rpm, brew and cygwin. That said, there is no good reason why git-pm shouldn't know how to delegate such concerns to a platform-specific package manager.

The basic intent is to allow plugin authors to provide simple instructions to potential consumers of their plugin.

<hr/>
Installing a plugin should be as simple as:

	   git pm install foobar

Such a comamnd should work whether the platform is Linux, cygwin or Mac OSX. In fact, the only 
common denominator should be git itself, and its dependencies (POSIX shell and perl).
<hr/>
Install a plugin, given a URL that can locate its descriptor:

	   git pm install [ plugin-url | plugin-archive | plugin-name ]

<hr/>
Remove a plugin, given a name that can identify it:

	   git pm remove plugin-name

<hr/>
Update an installed plugin:

	   git pm update plugin-name

<hr/>
Inspect a registry of available available, installed, active or inactive plugins:

	   git pm list available|installed|active|inactive

<hr/>
Describe the current installation, availability or activation status of a plugin:

	   git pm status plugin-name

<hr/>

Activation/De-activation
------------------------
Activation is the means by which a locally available plugin can be made available to the git command line. The idea is to 

	   git-pm activate plugin-name
	   git-pm deactivate plugin-name

WHAT GIT-PM IS:
===============
* a native extension manager for the git platform
* an _activator_ for git extensions
* distribution and platform package mamager friendly
* git-aware

WHAT GIT-PM IS NOT:
===================
* a build tool
* a replacement for a package manager
* useful for anything other than git extensions

CONCEPTS
========

plugin
------
An extension to git that exports 1 or more commands to the git command line

package
-------
A platform-specific archive that is installable by a platform-specific package manager. Packages will _package_ plugins.

plugin-descriptor
-----------------
A package-manager agnostic descriptor that describes a plugin to the git platform, in particular git-pm.

package-descriptor
------------------
A package-manager specific descriptor that describes a package to a package manager.

plugin manager
--------------
A command, such as git-pm, that can install, remove, activate or deactive plugins by delegating platform specific
concerns to a platform-specific package manager.

package-manager
---------------
A platform-specific manager of packages.

plugin author
-------------
An author of git plugins.

package author
--------------
An author of package specifications for a package manager. In particular, the author of a package specification that allows
a git plugin to be bundled into a package for the purposes of distribution and management.

package-manager-adapter
-----------------------
A pluggable component of git-pm that exposes a platform-specific package manager via a uniform interface.

DEPENDENCY MANAGEMENT
=====================
It is unclear yet how important dependency management will be. Where possible, such concerns will be delegated to 
platform-specific package managers. That said, there may still be value in managing dependencies between git-pm 
packages at the git-pm level.

PACKAGE NAME
============
The package name is currently gpm. Howeve, the "General Purpose Mouse" package has already claimed this name in the apt space, at least.

So, it might be better to use 'git-pm' as the package name, which isn't so bad since idiomatic use of the package should be 'git pm blah'.

SUPPORTED PACKAGE MANGERS
=========================
The intent of git-pm is not to duplicate the functionality of existing package managers. The intent is to provide a package manager for git
as a platform itself. To the extent that a build process is required to install a git extension, then such concerns will be delegated
to a real package manager that knows how to deal with such concerns.

The intent is that a minimal plugin that depends only on the availability of a shell, should be installable with something as simple as:

    git pm install foobar

This should work whether your git install is running on Linux, cywgin, Windows (MSYSGIT), MAC, AIX or whatever.

If a compilation is required, then delegation to a platform package manager will be requried. 

Linux
-----
* git
* rpm
* apt

Mac
---
* git
* brew

cygwin
---
* git

CONTRACTS
=========
The following contracts will be required between:

<dl>
<dt>the git user and git-pm</dt>
<dd>
This contract will be specified in terms of the git-pm man page. It will specify the plugin management commands offered by
the git-pm interface to the user.
</dd>
<dt>the git runtime and git-pm</dt>
<dd>
This contract will specify the technique by which git-pm exposes git extensions to the git command line. It will include
support for exposing:
<ul>
<li>sub-commands</li>
<li>man pages</li>
<li>shell completions</li>
</ul>
</dd>
<dt>git-pm and package-manager adapters</dt>
<dd>
This contract will specify how to add a new package-manager adapter. The purpose will be to allow git-pm to delegate
its interface to backend package managers that know how to manage platform specific concerns such as building, 
dependency management, package distribution etc.
</dd>
</dd>
<dt>package-manager adapters and package managers</dt>
<dt>extension authors and the git-pm package manager</dt>
</dl>

INFLUENCES
==========
The following programs have influenced the design of git-pm.

npm
---
The node package manager. 

Node is an interesting, V8-JavaScript based runtime for implementing servers. Node comes with a tightly coupled package manager npm. If node is your platform, npm
is the package manager for that platform. In particular, npm works the same way irrespective of which platform you have node installed on.

brew
----
A Mac OSX specific package manager.

Brew is a relatively new package manager for the Mac OSX operating system. It has several nice features, including its formula registry that allows
authors to specify succinct package management formulae as short ruby scripts. Brew also uses git as an integral part of its registry and run-time.

SCEPTICS CHALLENGE
==================
Some people doubt there is value in a 'git plugin mamager'. In response to this scepticism, I pose the following 
challenge.

1. take an arbitrary git extension.
2. specify installation instructions for that extension in 4 words or less.
3. make sure those 4 words work on Linux, Cygwin, MAC OSX and AIX.
4. verify that following installation, the man pages work.

As an example, there is a package called gitwork. It is available somewhere on the Internet. I think, as a tarball. Or perhaps a zip. I don't think it has any dependencies, but I am really not sure. Why don't you suck it and see?

MAILING LIST
============
Until noted otherwise, please use the [http://dir.gmane.org/gmane.comp.version-control.git](git@vger.kernel.org) 
mailing list for discussions about design decisions. gpm: is suggested a good prefix for such discussions.

REVISIONS
=========
Ordered most recent, to less recent:

* changed 'gpm' to 'git pm' on the assumption that 'git-pm' will be in the path and that 'General Purpose Mouse' has already nabbed 'gpm'
* changed terminology from 'package' to 'plugin' to help reduce consfusion about the objectives of the project

AUTHOR
======
Jon Seymour




