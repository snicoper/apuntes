.. _reference-linux-mi_bashrc:

##########
Mi .bashrc
##########

**Fuentes**

* https://gist.github.com/stuarteberg/4446426

----

.. code-block:: bash

    # Colors for the prompt
    blue="\033[0;34m"
    white="\033[0;37m"
    green="\033[0;32m"

    # Brackets needed around non-printable characters in PS1
    ps1_blue='\['"$blue"'\]'
    ps1_green='\['"$green"'\]'
    ps1_white='\['"$white"'\]'

    parse_git_branch() {
        gitstatus=`git status 2> /dev/null`
        if [[ `echo $gitstatus | grep "Changes to be committed"` != "" ]]
        then
            git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1***)/'
        elif [[ `echo $gitstatus | grep "Changes not staged for commit"` != "" ]]
        then
            git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1**)/'
        elif [[ `echo $gitstatus | grep "Untracked"` != "" ]]
        then
            git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1*)/'
        elif [[ `echo $gitstatus | grep "nothing to commit"` != "" ]]
        then
            git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
        else
            git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1?)/'
        fi
    }

    # Echo a non-printing color character depending on whether or not the current git branch is the master
    # Does NOT print the branch name
    # Use the parse_git_branch() function for that.
    parse_git_branch_color() {
        br=$(parse_git_branch)
        if [[ $br == "(master)" || $br == "(master*)" || $br == "(master**)" || $br == "(master***)" ]]; then
            echo -e "${blue}"
        else
            echo -e "${green}"
        fi
    }

    # No color:
    #export PS1="@\h:\W\$(parse_git_branch) \$ "

    # With color:
    export PS1="$ps1_blue@\h:$ps1_white\W\[\$(parse_git_branch_color)\]\$(parse_git_branch) $ps1_blue\$$ps1_white "
