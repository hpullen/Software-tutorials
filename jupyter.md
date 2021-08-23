# Jupyter notebooks

## Running a jupyter notebook locally

To start a jupyter server, run the command
```
jupyter notebook
```

This will automatically open a window in your default browser, where you can browse files and create and run notebooks.

If you accidentally close the browser, the notebook will still be running in the terminal. The output in the terminal will include a message like:
```
The Jupyter notebook is running at:
http://localhost:<xxxx>
```
where `<xxxx>` is some number (default = `8888`). To access the server again, just type `localhost:<xxxx>` into the address bar of an internet browser.

The server can be shut down by pressing `Ctrl-c` or closing the terminal.

## Running a jupyter notebook remotely

On the remote server, set up a password:
```
jupyter notebook password
```
(only need to do this once). Next, start a notebook server without opening a browser:
```
jupyter notebook no-browser
```
The output message will tell you where the notebook is running; by default this is `localhost:8888`, but could be a different number if `8888` is already in use.

From your local machine, connect to the remote notebook server:
```
ssh -N -f -L localhost:<xxx>:localhost:<yyyy> <user>@<machine>.hep.phy.cam.ac.uk
```
then enter the password you use to log into the HEP cluster. 
* `localhost:<xxxx>` is the port you want to use on the **local machine**; by default you can just use `localhost:8888`. 
* `localhost:<yyyy>` is the port where you launched the server on the **remote machine**, and should be changed if the server is running on a different port.

To use the server, type `localhost:<xxxx>` into a browser.
