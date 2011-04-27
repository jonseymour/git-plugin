NAME
====
gpm - a package manager for git extensions

DESCRIPTION
===========
This is place holder for a proposed plugin architecture for git extensions.

The initial deliverable of the project will be a plugin architecture proposal. 
In parallel to this deliverable a reference plugin manager will be developed.

PRINCIPLES
==========
* define a repository layout specification
* define a package descriptor (using the git config syntax)
* package manager agnostic repo and package specifications
 * perhaps define a pluggable package manager interface
* support for:
 * existing contrib/ directory
 * existing git patterns for finding and using extensions
 * man pages
 * package specific configuration help
 * bash completions
 * scripts
* build support:
 * for documentation, archives
* layers
 * repo, package descriptors
 * tool interface specifications 
 * tool implementations
 * global package registry and repository

INTENDED SCENARIOS
==================

Installation and Removal
------------------------
	gpm install package-name | package-url | package-archive
	gpm remove package-name
	gpm update package-name
	gpm list installed|available|active|inactive
	gpm status package-name

Activation/De-activation
------------------------
	gpm activate package-name
	gpm deactivate package-name

MAILING LIST
============
Until noted otherwise, please use the [http://dir.gmane.org/gmane.comp.version-control.git](git@vger.kernel.org) 
mailing list for discussions about design decisions. gpm: is suggested a good prefix for such discussions.

AUTHOR
======
Jon Seymour




