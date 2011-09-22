First you want a version of `git` that comes with the bash completion script installed.  Of course, you could also download the `current version <https://github.com/git/git/blob/master/contrib/completion/git-completion.bash>`_ and store it somewhere (e.g. in `~/.bash/`), but using the `git-core` port from `MacPorts <http://www.macports.org/>`_ or a the binaries available at the `Git home page <http://git-scm.com/>`_ has the advantage of (very likely) giving you a more recent version.  In the case of MacPorts_ you would run::

  $ sudo port install git-core +bash_completion

Next you want to add the following to your `~/.bashrc`::

  # include the (upstream) tab completion definition
  source /opt/local/share/doc/git-core/contrib/completion/git-completion.bash

  # add `g` alias for the `git` command & make completion work for it...
  alias g=git
  complete -o bashdefault -o default -o nospace -F _git g 2>/dev/null \
          || complete -o default -o nospace -F _git g

  # set up the shell prompt
  export GIT_PS1_SHOWDIRTYSTATE=1
  export GIT_PS1_SHOWSTASHSTATE=1
  export GIT_PS1_SHOWUPSTREAM="verbose"

Please note, that when using the installer the path to the git completion definition is different from above::

  source /usr/local/etc/bash_completion.d/git-completion.bash

Lastly you should modify your shell prompt.  Essentially you need to add::

  $(__git_ps1)

somewhere.  My complete prompt is defined as follows, YMMV::

  PS1='\[\033]; \u@\h:\w $(date '+@%H:%M')\007\]\w$(__git_ps1)-> '

The above mentioned git completion definition file contains more information about the various options you can use to tweak your prompt.
