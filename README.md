# cncjs-pendant-keyboardreader
A CNCjs pendant for remote jogging using a keyboard. Implements GRBL's "smooth jogging" ($J commands).

I'm currently using this with a Logitech K400+ and GRBL

## Pre-requisite

`Node.JS` and `npm` must have been installed.
This version of the pendant was tested using Node.JS [v10.19.0](https://nodejs.org/en/blog/release/v10.19.0/)

## Installation

After cloning the repository to your work directory, change into this directory and run
```
npm install
```

## Usage

CNCjs must be running (either the standalone app, or as a server)

From a shell/command window, go to `cncjs-pendant-keyboardreader` directory, and run: 

`bin/cncjs-pendant-keyboardreader --socket-port <socket_port> --port <port> --device <device>`

### To determine `<socket_port>` value: 

* On Windows, if using the CNCjs standalone app, go to the "View" menu, click "View in browser", this should open a browser window to a URL that will look something like "http://127.0.0.1:57325/#/workspace". The number right after the "127.0.0.1:" part is the XXXXX to be passed along.

* On Linux, if using the CNCjs server, the `<socket_port>` value is normally 8000, unless specified otherwise.

### To determine `<port>` value: 

This is the name of the serial port that CNCjs uses to connect to the machine (see "Port" field in the "Connection" widget in CNCjs)

* On Windows, `<port>` will often be something like "COM5"

* On Linux, `<port>` will often be something like "/dev/ttyACM0"

Pass --help to `bin/cncjs-pendant-keyboardreader` for more options.

### To determine the `<device>` value:

run `bin/cncjs-pendant-keyboardreader --list-devices`

Use the `path` value for the `<device>` argument. On linux, this may be something like `/dev/hidraw1`

If execution is successful, you should see something like this:

>Connected to ws://{loooong string of characters here}

>Connected to port `<port>` (Baud rate: 115200)

At this point, the pendant will react to the following keys:

* pressing the left,right,up,down,pageUp,pageDown keys will jog the machine by the FINE step size, along X/Y/Z
* holding the **Alt** key while pressing these jog keys will jog by the MEDIUM step size
* holding the **Ctrl** key while pressing these jog keys will jog by the LARGE step size

The distances for FINE, MEDIUM and LARGE can be modified in the source code, they are 0.1mm, 1mm, and 10mm by default.

* /!\ holding the **Shift** key while pressing a jog key will trig a **CONTINUOUS** smooth jog along the selected axis (no need to hold the key). Releasing the shift key will **STOP** the movement.


