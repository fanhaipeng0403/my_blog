---
title: zsh
date: 2017-01-05 11:39:11
tags: zsh

---

```

# If you come from bash you might have to change your $PATH.
# export PATH=$HOME/bin:/usr/local/bin:$PATH


set t_Co=256
# Path to your oh-my-zsh installation.
export ZSH=/home/fanhaipeng/.oh-my-zsh

# Set name of the theme to load. Optionally, if you set this to "random"
# it'll load a random theme each time that oh-my-zsh is loaded.
# See https://github.com/robbyrussell/oh-my-zsh/wiki/Themes
ZSH_THEME="wedisagree"

[[ -s ~/.autojump/etc/profile.d/autojump.sh ]] && . ~/.autojump/etc/profile.d/autojump.sh



#export pip_require_virtualenv=true
export workon_home=$home/.virtualenvs
source /usr/local/bin/virtualenvwrapper.sh

# Uncomment the following line to use case-sensitive completion.
# CASE_SENSITIVE="true"

# Uncomment the following line to use hyphen-insensitive completion. Case
# sensitive completion must be off. _ and - will be interchangeable.
# HYPHEN_INSENSITIVE="true"

# Uncomment the following line to disable bi-weekly auto-update checks.
# DISABLE_AUTO_UPDATE="true"

# Uncomment the following line to change how often to auto-update (in days).
# export UPDATE_ZSH_DAYS=13

# Uncomment the following line to disable colors in ls.
# DISABLE_LS_COLORS="true"

# Uncomment the following line to disable auto-setting terminal title.
# DISABLE_AUTO_TITLE="true"

# Uncomment the following line to enable command auto-correction.
# ENABLE_CORRECTION="true"

# Uncomment the following line to display red dots whilst waiting for completion.
# COMPLETION_WAITING_DOTS="true"

# Uncomment the following line if you want to disable marking untracked files
# under VCS as dirty. This makes repository status check for large repositories
# much, much faster.
# DISABLE_UNTRACKED_FILES_DIRTY="true"

# Uncomment the following line if you want to change the command execution time
# stamp shown in the history command output.
# The optional three formats: "mm/dd/yyyy"|"dd.mm.yyyy"|"yyyy-mm-dd"
# HIST_STAMPS="mm/dd/yyyy"

# Would you like to use another custom folder than $ZSH/custom?
# ZSH_CUSTOM=/path/to/new-custom-folder

# Which plugins would you like to load? (plugins can be found in ~/.oh-my-zsh/plugins/*)
# Custom plugins may be added to ~/.oh-my-zsh/custom/plugins/
# Example format: plugins=(rails git textmate ruby lighthouse)
# Add wisely, as too many plugins slow down shell startup.
plugins=(git vi-mode web-search  zsh-syntax-highlighting-filetypes last-working-dir wd colored-man extract zsh-syntax-highlighting powerline-shell sudo chucknorris command-not-found fabric pip jsontools urltools encode64 django)


source $ZSH/oh-my-zsh.sh

# User configuration

# export MANPATH="/usr/local/man:$MANPATH"

# You may need to manually set your language environment
export LANG=en_US.UTF-8

# Preferred editor for local and remote sessions
# if [[ -n $SSH_CONNECTION ]]; then
#   export EDITOR='vim'
# else
#   export EDITOR='mvim'
# fi

# Compilation flags
# export ARCHFLAGS="-arch x86_64"

# ssh
# export SSH_KEY_PATH="~/.ssh/rsa_id"

# Set personal aliases, overriding those provided by oh-my-zsh libs,
# plugins, and themes. Aliases can be placed here, though oh-my-zsh
# users are encouraged to define aliases within the ZSH_CUSTOM folder.
# For a full list of active aliases, run `alias`.
#
# Example aliases
# alias zshconfig="mate ~/.zshrc"
# alias ohmyzsh="mate ~/.oh-my-zsh"
alias grep='grep --color=auto'
alias deact='deactivate'
alias sougou='killall fcitx;fcitx;killall sogou-qimpanel;sogou-qimpanel'
alias update='sudo apt-get update'
alias zidian='sdcv'
alias quseqi='gpick'
alias  sshali='ssh root@120.27.31.238'                                      11:58:27
alias lz='ls -Ssh'
alias ll='ls -alF'
alias la='ls -A'
alias xiezai='sudo apt-get autoremove --purge'
alias dakai='nautilus'

#
export PATH="/usr/local/p/versions/python:$PATH"
export PATH=/home/fanhaipeng/.pyenv/bin:/home/fanhaipeng/.pyenv/bin:/usr/local/p/versions/python:/home/fanhaipeng/.autojump/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/usr/jdk-8/jdk1.8.0_111/bin:/usr/jdk-8/jdk1.8.0_111/jre/bin/

#--------------------tmuxinator-------------------------------------------
source $HOME/.tmuxinator/.tmuxinator.sh
export EDITOR='vim'

export KEYTIMEOUT=1

#---------------------------------------------------------------------------
# 只通过ctrl+z就可以在shell和vim之间快速转换的一个函数
fancy-ctrl-z () {
if [[ $#BUFFER -eq 0 ]]; then
    BUFFER="fg"
    zle accept-line
else
    zle push-input
    zle clear-screen
fi
}
zle -N fancy-ctrl-z
bindkey '^Z' fancy-ctrl-z


# ------------------------------------------------
# 根据文件类型不同显示不同的颜色

# Core highlighting update system

# Array used by highlighters to declare overridable styles.
typeset -gA ZSH_HIGHLIGHT_STYLES

# An `object' implemented by below 3 arrays' elements could be called a
# `highlighter', registered by `_zsh_highlight_add-highlighter`. In
# other words, these arrays are indexed and tied by their own
# functionality. If they have been arranged inconsistently, things goes
# wrong. Please see `_zsh_highlight-zle-buffer` and `_zsh_highlight_add-
# highlighter`.


# Actual recolorize functions to be called.
typeset -a zsh_highlight_functions; zsh_highlight_functions=()

# Predicate functions whether its recolorize function should be called or not.
typeset -a zsh_highlight_predicates; zsh_highlight_predicates=()

# Highlight storages for each recolorize functions.
typeset -a zsh_highlight_caches; zsh_highlight_caches=()

_zsh_highlight-zle-buffer() {
if (( PENDING )); then
    return
fi

local ret=$?
{
    local -a funinds
    local -i rh_size=$#region_highlight
    for i in {1..${#zsh_highlight_functions}}; do
        local pred=${zsh_highlight_predicates[i]}
        local cache_place=${zsh_highlight_caches[i]}
        if _zsh_highlight-zle-buffer-p "$rh_size" "$pred"; then
            if ((${#${(P)cache_place}} > 0)); then
                region_highlight=(${region_highlight:#(${(P~j.|.)cache_place})})
                local -a empty; empty=(); : ${(PA)cache_place::=$empty}
            fi
            funinds+=$i
        fi
    done
    for i in $funinds; do
        local func=${zsh_highlight_functions[i]}
        local cache_place=${zsh_highlight_caches[i]}
        local -a rh; rh=($region_highlight)
        {
            "$func"
        } always  {
        : ${(PA)cache_place::=${region_highlight:#(${(~j.|.)rh})}}
    }
done
  } always {
  ZSH_PRIOR_CURSOR=$CURSOR
  ZSH_PRIOR_HIGHLIGHTED_BUFFER=$BUFFER
  return $ret
  }
}

# Whether supplied highlight_predicate satisfies or not.
_zsh_highlight-zle-buffer-p() {
local region_highlight_size="$1" highlight_predicate="$2"
# If any highlightings are not taken into account, asume it is needed.
# This holds for some up/down-history commands, for example.
((region_highlight_size == 0)) || "$highlight_predicate"
}

# Whether the command line buffer is modified or not.
_zsh_highlight_buffer-modified-p() {
[[ ${ZSH_PRIOR_HIGHLIGHTED_BUFFER:-} != $BUFFER ]]
}

# Whether the cursor is moved or not.
_zsh_highlight_cursor-moved-p() {
((ZSH_PRIOR_CURSOR != $CURSOR))
}

# Register an highlighter.
_zsh_highlight_add-highlighter() {
zsh_highlight_functions+="$1"
zsh_highlight_predicates+="${2-${1}-p}"
zsh_highlight_caches+="${3-${1//-/_}}"
}


# Main highlighter

ZSH_HIGHLIGHT_STYLES+=(
default                       'fg=248'
unknown-token                 'fg=196,bold,bg=234'
reserved-word                 'fg=197,bold'
alias                         'fg=197,bold'
builtin                       'fg=107,bold'
function                      'fg=85,bold'
command                       'fg=166,bold'
hashed-command                'fg=70'
path                          'fg=30'
globbing                      'fg=170,bold'
history-expansion             'fg=blue'
single-hyphen-option          'fg=244'
double-hyphen-option          'fg=244'
back-quoted-argument          'fg=220,bold'
single-quoted-argument        'fg=137'
double-quoted-argument        'fg=137'
dollar-double-quoted-argument 'fg=148'
back-double-quoted-argument   'fg=172,bold'
assign                        'fg=240,bold'
)

mkstyle () {
    local lastlast
    local last

    while [ "$#" -gt 0 ]; do
        cur=$1
        shift

        if [ "$last" = 5 ]; then
            if [ "$lastlast" = 38 ]; then
                style+=( "fg=$cur" )
                lastlast=
                last=
                continue
            elif [ "$lastlast" = 48 ]; then
                style+=( "bg=$cur" )
                lastlast=
                last=
                continue
            fi
        fi

        lastlast=$last
        last=$cur
    done

    case "$last" in
        00|0) style+=( "none" )       ;;
        01|1) style+=( "bold" )       ;;
        04|4) style+=( "underscore" ) ;;
        05|5) style+=( "blink" )      ;;
        07|7) style+=( "reverse" )    ;;
        08|8) style+=( "concealed" )  ;;
    esac
}

function {
local coloring ext rawstyle
local -a style

for coloring in ${(s.:.)LS_COLORS}; do
    ext=${coloring%%\=*}
    rawstyle=${coloring##*\=}
    style=()

    mkstyle ${(s.;.)rawstyle}
    style=${(j.,.)style}

    ZSH_HIGHLIGHT_STYLES+=(
    "$ext" "$style"
    )
done
}

# Tokens that are always immediately followed by a command.
ZSH_HIGHLIGHT_TOKENS_FOLLOWED_BY_COMMANDS=(
'|' '||' ';' '&' '&&' 'noglob' 'nocorrect' 'builtin'
)

# Check if the argument is variable assignment
_zsh_highlight_check-assign() {
setopt localoptions extended_glob
[[ ${(Q)arg} == [[:alpha:]_]([[:alnum:]_])#=* ]]
}

# Check if the argument is a path.
_zsh_highlight_check-path() {
[[ -z ${(Q)arg} ]] && return 1
[[ -e ${(Q)arg} ]] && return 0
[[ ! -e ${(Q)arg:h} ]] && return 1
[[ ${#BUFFER} == $end_pos && -n $(print ${(Q)arg}*(N)) ]] && return 0
return 1
}

# Highlight special chars inside double-quoted strings
_zsh_highlight_highlight_string() {
    setopt localoptions noksharrays
    local i j k style
    # Starting quote is at 1, so start parsing at offset 2 in the string.
    for (( i = 2 ; i < end_pos - start_pos ; i += 1 )) ; do
        (( j = i + start_pos - 1 ))
        (( k = j + 1 ))
        case "$arg[$i]" in
            '$')  style=$ZSH_HIGHLIGHT_STYLES[dollar-double-quoted-argument];;
            '%')  style=$ZSH_HIGHLIGHT_STYLES[globbing];;
            '^')  style=$ZSH_HIGHLIGHT_STYLES[globbing];;
            "\\") style=$ZSH_HIGHLIGHT_STYLES[back-double-quoted-argument]
                (( k += 1 )) # Color following char too.
                (( i += 1 )) # Skip parsing the escaped char.
                ;;
            *)    continue;;
        esac
        region_highlight+=("$j $k $style")
    done
}

# Core syntax highlighting.
_zsh_main-highlight() {
setopt localoptions extendedglob bareglobqual
local start_pos=0 end_pos highlight_glob=true new_expression=true arg style
region_highlight=()

for arg in ${(z)BUFFER}; do
    local substr_color=0

    style=

    [[ $start_pos -eq 0 && $arg = 'noglob' ]] && highlight_glob=false

    ((start_pos+=${#BUFFER[$start_pos+1,-1]}-${#${BUFFER[$start_pos+1,-1]##[[:space:]]#}}))
    ((end_pos=$start_pos+${#arg}))

    if $new_expression; then
        new_expression=false

        res=$(LC_ALL=C builtin type -w $arg 2>/dev/null)
        case $res in
            *': reserved')  style=$ZSH_HIGHLIGHT_STYLES[reserved-word];;
            *': alias')     style=$ZSH_HIGHLIGHT_STYLES[alias]
                local aliased_command="${"$(alias $arg)"#*=}"
                [[ -n ${(M)ZSH_HIGHLIGHT_TOKENS_FOLLOWED_BY_COMMANDS:#"$aliased_command"} && -z ${(M)ZSH_HIGHLIGHT_TOKENS_FOLLOWED_BY_COMMANDS:#"$arg"} ]] && ZSH_HIGHLIGHT_TOKENS_FOLLOWED_BY_COMMANDS+=($arg)
                ;;
            *': builtin')   style=$ZSH_HIGHLIGHT_STYLES[builtin];;
            *': function')  style=$ZSH_HIGHLIGHT_STYLES[function];;
            *': command')   style=$ZSH_HIGHLIGHT_STYLES[command];;
            *': hashed')    style=$ZSH_HIGHLIGHT_STYLES[hashed-command];;
            *)              if _zsh_highlight_check-assign; then
                style=$ZSH_HIGHLIGHT_STYLES[assign]
                new_expression=true
            elif _zsh_highlight_check-path; then
                style=$ZSH_HIGHLIGHT_STYLES[path]
            elif [[ $arg[0,1] = $histchars[0,1] ]]; then
                style=$ZSH_HIGHLIGHT_STYLES[history-expansion]
            else
                style=$ZSH_HIGHLIGHT_STYLES[unknown-token]
            fi
            ;;
    esac
else
    for key in ${(k)ZSH_HIGHLIGHT_STYLES}; do
        case $key in
            "*."*) ;;
            *) continue ;;
        esac
        case $arg in
            *.$key[3,-1]) style=$ZSH_HIGHLIGHT_STYLES[$key] ;;
        esac
        [ -n "$style" ] && break
    done
    if [ -z "$style" ]; then
        case $arg in
            '--'*)   style=$ZSH_HIGHLIGHT_STYLES[double-hyphen-option];;
            '-'*)    style=$ZSH_HIGHLIGHT_STYLES[single-hyphen-option];;
            "'"*"'") style=$ZSH_HIGHLIGHT_STYLES[single-quoted-argument];;
            '"'*'"') style=$ZSH_HIGHLIGHT_STYLES[double-quoted-argument]
                region_highlight+=("$start_pos $end_pos $style")
                _zsh_highlight_highlight_string
                substr_color=1
                ;;
            '`'*'`') style=$ZSH_HIGHLIGHT_STYLES[back-quoted-argument];;
            *"*"*)   $highlight_glob && style=$ZSH_HIGHLIGHT_STYLES[globbing] ||
                style=$ZSH_HIGHLIGHT_STYLES[default];;
        *)       if _zsh_highlight_check-path; then
            style=$ZSH_HIGHLIGHT_STYLES[path]
        elif [[ $arg[0,1] = $histchars[0,1] ]]; then
            style=$ZSH_HIGHLIGHT_STYLES[history-expansion]
        else
            style=$ZSH_HIGHLIGHT_STYLES[default]
        fi
        ;;
esac
      fi
  fi
  [[ $substr_color = 0 ]] &&
      region_highlight+=("$start_pos $end_pos $style")
  [[ -n ${(M)ZSH_HIGHLIGHT_TOKENS_FOLLOWED_BY_COMMANDS:#"$arg"} ]] && new_expression=true
  start_pos=$end_pos
  done
}


# Setup functions

# Intercept specified ZLE events to have highlighting triggered.
_zsh_highlight_bind-events() {

# Resolve event names what have to be bound to.
zmodload zsh/zleparameter 2>/dev/null || {
echo 'zsh-syntax-highlighting:zmodload error. exiting.' >&2
return -1
  }
  local -a events; : ${(A)events::=${@:#(_*|orig-*|.run-help|.which-command)}}

  # Bind the events to _zsh_highlight-zle-buffer.
  local clean_event
  for event in $events; do
      if [[ "$widgets[$event]" == completion:* ]]; then
          eval "zle -C orig-$event ${${${widgets[$event]}#*:}/:/ } ; $event() { builtin zle orig-$event && _zsh_highlight-zle-buffer } ; zle -N $event"
      else
          case $event in
              accept-and-menu-complete)
                  eval "$event() { builtin zle .$event && _zsh_highlight-zle-buffer } ; zle -N $event"
                  ;;
              .*)
                  # Remove the leading dot in the event name
                  clean_event=$event[2,${#event}]
                  case ${widgets[$clean_event]-} in
                      (completion|user):*)
                          ;;
                      *)
                          eval "$clean_event() { builtin zle $event && _zsh_highlight-zle-buffer } ; zle -N $clean_event"
                          ;;
                  esac
                  ;;
              *)
                  ;;
          esac
      fi
  done
}

# Load highlighters from specified directory if it exists.
_zsh_highlight_load-highlighters() {
[[ -d $1 ]] && for highlighter_def ($1/*.zsh) . $highlighter_def
}


# Setup

# Bind highlighting to all known events.
_zsh_highlight_bind-events "${(@f)"$(zle -la)"}"

# Register the main highlighter.
_zsh_highlight_add-highlighter _zsh_main-highlight _zsh_highlight_buffer-modified-p

# Load additional highlighters if available.
_zsh_highlight_load-highlighters "${${(%):-%N}:h}/highlighters"
eval $(dircolors -b $HOME/.dircolors)

```

