# TMUX

Terminal that runs the window in a process and not tied to the session.

1. Frist thing you want to do, is create a TMUX session

```
tmux new -s MYSESSION
```

2. open a new tab using the prefix CTRL+b

3. Switch back to the first tab with CTRL+ 0 or back again to the new tab with CTRL+ 1

4. Edit the configuration file ~/.tmux.conf

This changes the default (Prefix) wich is Ctrl+b to Ctrl+a

```
# If you're used to screen
set -g prefic C-a
bind C-a send-prefix
unbind C-b
# life easier
set -g history-limit 10000
set -g allow-rename off
```

5. Screen splitting

Split the screen vertically: (Prefix) + %
Split the screen horizontally: (Prefix) + "
Move to other split: (Prefix) + arrowkeys
Make a splitted pan full screen: (Prefix) + z

6. Go to the beginning or end of the line 

Ctrl + a a
Ctrl + e


