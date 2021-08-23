To **create a new tmux session:**

```
tmux new -s <session name>
```

This will essentially put you in a new terminal within your session on the HEP cluster, which you can detach from and reattach to, while leaving code running inside if you wish. You should see a green bar containing the session name appear at the bottom of your screen, which shows you that you are inside a tmux session.

If you forget to give it a name (i.e. you just type `tmux new`), the session will simply be named with a number starting at 0.

To **detach from the tmux session** (i.e. get back to the place you were at before you started the session), you can either type:

```
tmux detach
```

or press `Ctrl-b` then `d`.

Once you're outside tmux, you can **check which sessions are running** by typing

```
tmux ls
```

You can create as many different tmux sessions as you like, provided they all have different names.

To **get back into a running tmux session** (even if you have logged out of the cluster and back in), type 

```
tmux attach -t <session name>
```

To **kill a tmux session** once you're finished with it, you can either type 

```
tmux kill-session
```

from within the session itself, or

```
tmux kill-session -t <session name>
``` 

from outside the session.

You can also **get rid of all of your tmux sessions** at once by typing 

```
tmux kill-server
```

Tmux can be used to do a lot of other cool things, like opening multiple tabs of sessions within one login to the cluster, and displaying panes of terminals side-by-side, but I'll end the guide here for now.
