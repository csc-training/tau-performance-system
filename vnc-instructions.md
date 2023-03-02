# Using Paraprof GUI with the VNC

Video of the whole process, step by step instructions below. 




https://user-images.githubusercontent.com/40563680/222256648-7ecba3cc-1720-45dd-98ff-9d641d21d06b.mp4





## Enabling the course modules

After loggin into Lumi using ssh, run:

```bash
module use /appl/local/csc/courses/tau_prof_march23/modules/
```

After this you can use tau by loading the module:

```bash
module load tau
```

The tau module also provides the **parprof** and **pprof** commands

## Running paraprof GUI 

**Avoid running paraprof on the login node as the memory limits are strict and the java based GUI will start failing when it hits the limits**


The GUI for **paraprof** can be run using direct X forwarding 

```
ssh -X <user>@lumi.csc.fi
```
_As there is no X11 forwarding enabled in LUMI slurm, this can only be used to run graphical applications on the login nodes_

Or using the VNC tool, the vnc tools is usually a bit more responsive and can be used on the compute nodes. 
To start an interactive shell on a compute node run (adjust memory and cpu requirements according to need):

```bash
srun  -p interactive -A <project> --pty -c 1 --mem=6G --time=00:60:00 bash
```

Then when logged into a Lumi compute node (and after enabling the course modules) run:

```bash
module load glx-vnc 
start-vnc
paraprof
```

The `start-vnc` command will print instructions on how to connect to the vnc using either
a browser or a dedicated vnc client, **Both methods still require manual port forwarding using ssh**.

The printed instructions will look something like this:

```
StartTime: 2023-03-01T15:47:44
Generating password
Starting vnc server
	Vnc server running on display :1
	Vnc port: 5901
Starting novnc proxy ( 60sec timeout )
Resolving novnc proxy port ( 60sec timeout)
	Novnc proxy on port: 43741


CONNECT WITH BROWSER
==================
Run on local machine to forward vnc connection from Lumi to local computer, if the port is in use locally change the port 
    ssh -N -L 43741:nid50824160:43741  nortamoh@lumi.csc.fi
Connect to this url in browser on local machine after running , port needs to be the same as in the ssh command (left value)
    http://localhost:43741/vnc.html?password=XnhRZMGI
==================

CONNECT WITH VNC CLIENT
==================
Run on local machine to forward vnc connection from Lumi to local computer, if the port is in use locally change the port (left value)
    ssh -N -L 5901:nid50824160:5901  nortamoh@lumi.csc.fi
Connect with native (locally installed) vnc client, e.g TigerVNC
    vncviewer localhost:5901
When prompted for a password, use XnhRZMGI
```

### Connecting

Following the printed instructions and copy pasting the commands:

**Browser**

1. Open a new connection to Lumi (No prompt or welcome message will printed, but the command is still successful): 
	`ssh -N -L 43741:nid50824160:43741  <user>@lumi.csc.fi`
2. Open a new web browser tab and paste the url ` http://localhost:43741/vnc.html?password=XnhRZMGI` into the address bar.

3. Press the connect button 
![vnc_screen](https://user-images.githubusercontent.com/40563680/222176346-d41e8d45-66e1-4d3d-ac80-bdc7b1a8b710.png)

4. Start using paraprof
![vnc_tau](https://user-images.githubusercontent.com/40563680/222176439-ebd41e9a-223d-4771-87da-766f8872cfad.png)

**VNC client**
1. If using a vnc client, run the other port forwarding command:
	`ssh -N -L 5901:nid50824160:5901  nortamoh@lumi.csc.fi`
2. Start the vnc client and point it to the correct local port, either using the cli or the gui (here we are using tigervnc)
	`vncviewer localhost:5901`
3. Insert the provided password, in our case `XnhRZMGI`
4. Start using paraprof


### Changing the resolution

_Only applies to the browser see vnc client specific instructions to find out how to change the resolution._

Select `Settings -> Advanced` to show the `Quality` and `Compression level` sliders. You can also set the `Scaling mode` to **Remote Resizing** to scale the vnc window to your screen. The `Settings` can be accessed using the gear icon on the far left side of the vnc window (or in case the tool bar is hidden using the small arrow on the far left side of the vnc window).  

