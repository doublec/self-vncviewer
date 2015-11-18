This is a work in progress VNC client written in Self. The current status is that it can connect to a VNC server that has no authentication and display the screen contents in a Morph.

To start a VNC session I did the following on Ubuntu:

1. Install tightvncserver.
2. Copy /usr/bin/vncserver to a temporary location.
3. Edit my copy of vncserver to remove the line that sets `$authType`.
4. Start with: `./vncserver -geometry 640x480 :1`

Load the vncViewer module using the transporter trees system by running the following from within Self:

    modules init
      registerTree: 'doublec_vncviewer'
                At: 'path/to/self-vncviewer'.

    bootstrap read: 'applications/vncViewer'
            InTree: 'doublec_vncviewer'.

    modules vncViewer tree: 'doublec_vncviewer'.

To connect from Self:

1. Display the `vncViewer` object as an outliner.
2. From an evaluator on that object, run `connect`
3. From an evaluator run `attachMorph` using `get` so you get the result in your hand.
4. Place the resulting outliner on the desktop, right click and choose `Show Morph`.
5. Place the Morph on the desktop.

You should now see the VNC session in the morph. If you run a VNC client and use the VNC session you should see the Self Morph update to reflect this.

An animated GIF of these steps can be seen below:

<img src='http://bluishcoder.co.nz/self/self_vnc2.gif'>

The Self code is based on the [RFB specification](http://www.realvnc.com/docs/rfbproto.pdf). Not all of it is implemented and those parts (like VNC authentication) have missing methods. The intent of this was for the debugger to appear for unimplemented parts of the spec and to implement them in the debugger and continue. This is how most of the existing code was written.

To make changes:

Middle clicking the desktop will bring up a menu with 'Changed Modules' as an option. Click that to show the changed modules morph. When the vncViewer code is edited this will show that the module has changed. Pressing the 'W' or 'W All' will write those changes to the directory specified in the `registerTree` for the `doublec_vncviewer` tree that was registered above. The standard `git` tools can then be used to show diffs, commit, etc.
