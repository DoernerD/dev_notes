# tmux cheatsheet

## Swap windows

    C-a :swap-window -t 1

Swaps the current window with window one. The tmux prefix C-a (C = cntrl)
calls the tmux command prompts, then the key is to have : before writing
out the command.

    C-a :swap-window -s 3 -t 1

Swaps window 3 with window 1

## Rename Panes

    C-a ,
    
This allows you to rename a pane.

## List Sessions

    tmux ls

lists all current sessions.

## Attach to Session

    tmux a 
    tmux a -t <session_name>

If you got kicked out of the terminal or accidentially closed it, you can attach
to the current session again with this command.

