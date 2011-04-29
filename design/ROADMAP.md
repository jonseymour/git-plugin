ROADMAP

Implementation will be managed in stages. The first stage provide extensions to be integrated 
with git-core that will support a minimal plugin architecture, consistent with existing
git practices.

* unmanaged plugins
 * no plugin management
 * no package management
 * guidelines about where to install:
  * man pages
  * scripts
  * executable binaries
  * html pages
  * plugin-specific resources
 * guidelines about:
  * how to discover the installation directory of plugin-specific resources
 * extensions to git-core
  * --man-path
  * --plugins-path
  * runtime support for integrating plugins into the PATH, MANPATH
  * runtime support for multiple plugin directories, to allow user-specific tailoring

Once minimal plugin support is enabled, ideas for more sophisticated plugin
management can be experimented using the plugin system itself.

* managed plugins
 * all of unmanaged plugins
 * support for managing the integrity of a single plugin directory
 * one directory per plugin to reduce conflicts between packages
 * activation step to reduce conflicts in the command name space
 * compatibility with the unmanaged plugins architecture
 
A longer term goal would be to support git-mediated package management - not to
replace the functions of a platform package manager, but to provide a uniform
user interface to such package managers for the limited purpose of locating
packages that contain git plugins and then invoking the package manager's
package installation functions.

* managed packages
 * all of managed plugins
 * delegation to one or more platform package managers for plugin discovery and installation


