NAME
====
git-plugin - a plugin manager for git extensions

CODE
====
Some files, particularly scripts, in the root directory are intended to be eventually submitted as a contribution to git-core.

DOCUMENTATION
=============
Files in Documentation are intended to submitted as a contribution to git-core.

<dl>
<dt><a href="/jonseymour/git-plugin/blob/master/Documentation/gitplugins.txt">gitplugins(7)</a></dt>
<dd>An description of the git plugin management architecture</dd>
<dt><a href="/jonseymour/git-plugin/blob/master/Documentation/gitplugins-layout.txt">gitplugins-layout(5)</a></dt>
<dd>A description of the plugins directory structure</dd>
</dl>

DESIGN NOTES
============
Files in design are for documenting design decisions as they evolve and are not
intended for inclusion in a submission to git-core.
<dl>
<dt><a href="http://github.com/jonseymour/git-plugin/blob/master/design/ROADMAP.md">ROADMAP</a></dt>
<dd>A suggested roadmap.</dd>
<dt><a href="dttp://github.com/jonseymour/git-plugin/blob/master/design/MISC.md">MISC</a></dt>
<dd>Miscellaneous design notes culled from other places</dd>
</dl>

MAILING LIST
============
Please use the git mailing list [http://dir.gmane.org/gmane.comp.version-control.git](git@vger.kernel.org) mailing list 
for discussions that you believe require community involvement. 

Feel free to open an github issue if you would like to discuss anything that you feel does not need to be immediately 
aired before the git community. We can always move the mailing list if the issue is of sufficient merit to seek wider consultation.

However, discussions in either place are fine by me.

BRANCHES
========
<dl>
   <dt><a href="https://github.com/jonseymour/git-plugin/master">master</a></dt>
   <dd>Never back tracks, but always behind.</dd>
   <dt><a href="https://github.com/jonseymour/git-plugin/proposal">proposal</a></dt>
   <dd>Experimental branch. Rebuilt frequently. Do not base work on it.</dd>
</dl>

Any commit that is not reachable from a tag prefixed with 'stable-' or from the tip of master 
should be considered to be unstable and should ideally not be reachable from any pull request you
submit to me.

REVISIONS
=========
Ordered most recent, to less recent:

* move git-plugin, git-install command onto future branch
* added a <a href="http://github.com/jonseymour/git-plugin/blob/master/design/ROADMAP.md">ROADMAP</a>
* updated mailing list recommendations
* moved some documentation into design/MISC.md
* documented intent of each branch
* changed from 'git-pm' to 'git-plugin' so that there is no confusion about what the objectives of this project are.
* changed 'gpm' to 'git pm' on the assumption that 'git-plugin' will be in the path and that 'General Purpose Mouse' has already nabbed 'gpm'
* changed terminology from 'package' to 'plugin' to help reduce consfusion about the objectives of the project

AUTHOR
======
(c) Copyright 2011 - Jon Seymour et al.

CONTRIBUTORS
============
The following people have informed my thinking about git-plugin, even though may not always be pleased by the outcomes.

But please, if there is anything here that throws you into fits of apoplexy, blame me, not them.

* Jonathan Nieder
* Junio C Hamano
* Michael J Gruber
* Motiejus Jakštys
* Carlos Martín Nieto
* Ævar Arnfjörð Bjarmason
* Fredrik Gustafsson
* Andreas Ericsson
* Felipe Contreras
* Drew Northup
* A Large Angry SCM
* Pau Garcia i Quiles
* David Lang
* Joey Hess
