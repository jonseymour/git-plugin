NAME
====
git-plugin - a plugin manager for git extensions

DESCRIPTION
===========
The initial deliverable of the project will be a plugin architecture proposal. The intent of this deliverable is to create specifications
that will allow plugin authors to create descriptors for their plugins that will be sufficient to enable git-plugin to locate an appropriate
package manager and delegate installation of the plugin to that package manager.

In parallel to this deliverable, a plugin manager interface (git-plugin) will be developed. Such an interface will manage git plugins on 
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

ALTERNATIVE APPROACHES
======================

1a. unmanaged plugins - single directory
----------------------------------------
* git-core defines a standard directory into which plugins are placed
* GIT_EXEC_PATH includes this directory by default.
* last-plugin-dropped wins semantics
* git-core does not specify how plugins are dropped into the directory, only that they may be

1b. unmanaged plugins - one directory per plugin
------------------------------------------------
* like 1a., but git-core defines a standard directory into which plugins are placed
* each directory has its own subdirectory
* git-core composes a GIT_EXEC_PATH including the executable dirs of such directory at runtime

#1 managed plugins
------------------

#2 managed packages
-------------------


INTENDED SCENARIOS
==================

Installation and Removal
------------------------
There is completely understandable resistance to YAPM - yet another package manager. This is not the goal of git-plugin. In particular, git-plugin will delegate platform-specific build
and deployment concerns to platform-specific package managers such as apt-get, rpm, brew and cygwin. That said, there is no good reason why git-plugin shouldn't know how to delegate such concerns to a platform-specific package manager.

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

	   git-plugin activate plugin-name
	   git-plugin deactivate plugin-name

WHAT GIT-PLUGIN IS:
===============
* a native extension manager for the git platform
* an _activator_ for git extensions
* distribution and platform package mamager friendly
* git-aware

WHAT GIT-PLUGIN IS NOT:
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
A package-manager agnostic descriptor that describes a plugin to the git platform, in particular git-plugin.

package-descriptor
------------------
A package-manager specific descriptor that describes a package to a package manager.

plugin manager
--------------
A command, such as git-plugin, that can install, remove, activate or deactive plugins by delegating platform specific
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
A pluggable component of git-plugin that exposes a platform-specific package manager via a uniform interface.

DEPENDENCY MANAGEMENT
=====================
It is unclear yet how important dependency management will be. Where possible, such concerns will be delegated to 
platform-specific package managers. That said, there may still be value in managing dependencies between git-plugin 
packages at the git-plugin level.

PACKAGE NAME
============
The package name is currently gpm. Howeve, the "General Purpose Mouse" package has already claimed this name in the apt space, at least.

So, it might be better to use 'git-plugin' as the package name, which isn't so bad since idiomatic use of the package should be 'git pm blah'.

SUPPORTED PACKAGE MANGERS
=========================
The intent of git-plugin is not to duplicate the functionality of existing package managers. The intent is to provide a plugin manager for git
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
<dt>the git user and git-plugin</dt>
<dd>
This contract will be specified in terms of the git-plugin man page. It will specify the plugin management commands offered by
the git-plugin interface to the user.
</dd>
<dt>the git runtime and git-plugin</dt>
<dd>
This contract will specify the technique by which git-plugin exposes git extensions to the git command line. It will include
support for exposing:
<ul>
<li>sub-commands</li>
<li>man pages</li>
<li>shell completions</li>
</ul>
</dd>
<dt>git-plugin and package-manager adapters</dt>
<dd>
This contract will specify how to add a new package-manager adapter. The purpose will be to allow git-plugin to delegate
its interface to backend package managers that know how to manage platform specific concerns such as building, 
dependency management, package distribution etc.
</dd>
</dd>
<dt>package-manager adapters and package managers</dt>
<dt>extension authors and the git-plugin package manager</dt>
</dl>

INFLUENCES
==========
The following programs have influenced the design of git-plugin.

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

MAILING LIST
============
Until noted otherwise, please use the [http://dir.gmane.org/gmane.comp.version-control.git](git@vger.kernel.org) 
mailing list for discussions about design decisions. gpm: is suggested a good prefix for such discussions.

REVISIONS
=========
Ordered most recent, to less recent:

* changed from 'git-pm' to 'git-plugin' so that there is no confusion about what the objectives of this project are.
* changed 'gpm' to 'git pm' on the assumption that 'git-plugin' will be in the path and that 'General Purpose Mouse' has already nabbed 'gpm'
* changed terminology from 'package' to 'plugin' to help reduce consfusion about the objectives of the project

AUTHOR
======
Jon Seymour
