# Tmux

## Shortcuts

``` sh
Ctrl-b # prefix

<prefix> ? # help

# session related
<prefix> d # exit current session
<prefix> $ # rename current session
<prefix> s # save current session env, need tmux-continuum support
<prefix> r # restore current session env, need tmux-continuum support

# window related
<prefix> c # add new window
<prefix> % # split window in vertical direction
<prefix> " # split window in horizaontal direction"
<prefix> 0~9 # change to specified window
<prefix> n # change to next window
<prefix> p # change to previous window
<prefix> l # change to last window
<prefix> , # rename current window
<prefix> . # move window
<prefix> w # show and select window
<prefix> Space # use next layout 
<prefix> Ctrl-o # rotate window

# pane related
<prefix> o # change to next pane in current window
<prefix> [hjkl] # change to another pane with directory key
<prefix> x # close current pane, need confirm
<prefix> m # mark pane
<prefix> q # display pane ids of current window
<prefix> z # zone out/in current pane to fullscreen
<prefix> i # show curren pane info
Ctrl-d # close current pane, close window if only one pane in current window

# copy and paste
<prefix> [ # enter scroll mode, start copy with Space key, end with Enter key.
<prefix> ] # paste data

# others
<prefix> : # command line
<prefix> t # show time, quit with 'q'
<prefix> = # select clipboard info

```

## commands

```sh
source-file ~/.tmux.conf
resize-pane [-D|-U|-L|-R] size
```

## common config

``` sh
# Enable mouse
setw -g mouse-resize-pane on
setw -g mouse-select-pane on
setw -g mouse-select-window on
set -g mouse on

# increase scrollback buffer size
set-option -g history-limit 1000000

# Disable auto rename of window
set-option -g allow-rename off

# Set default editor to vi
# set-window-option -g mode-keys vi
setw -g mode-keys vi

# Set colors
set -g default-terminal "screen-256color"

# Restore tmux env
set -g @continuum-save-interval '30'
set -g @continuum-restore 'on'
run-shell ~/.tmux/tmux-resurrect/resurrect.tmux
run-shell ~/.tmux/tmux-continuum/continuum.tmux
```

