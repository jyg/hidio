# `hidio`
`[hidio]` object for pure-data / vanilla Pd

This is a modified version of hidio external, as the current vesrion (found here https://puredata.info/downloads/hidio/releases/0.1) is incompatible with Multi-touch (MT) Protocol (version B) touchscreens.

In hidio.c, on line 526 some events are filtered (when they appear several times) and not sent to Pd. Furthermore, some events are duplicated as there is an instruction hidio_output_event(x, output_element) both in the parent function (hidio.c, line 528) and in the called function (hidio_linux.c, line 361).

For a correct use of the MT Protocol, each incoming event has to be transmitted, only one time, in order of arrival.

(for an explanation of the protocol, see https://www.kernel.org/doc/Documentation/input/multi-touch-protocol.txt)

In this modified version, I commented the lines 519-533 of hidio.c, but this may generate some issues with other hid-devices types. However, I don't think that the instruction hidio_output_event shoud be present in both hidio.c and hidio_linux.c.

Original README.md contents :

* This is a fork of the `[hidio]` 0.1 alpha sourcecode from https://puredata.info/downloads/hidio
* It has been built on macOS 10.14.3 and the build artifacts are included.  You may clone directly to your externals folder if you wish and start using `[hidio]` right away.  `[hidio]` is licensed under GPL2 and comes with ABSOLUTELY NO WARRANTY.
* PRs welcome.
* Issue a `make clean` first to build other platforms.
<hr>

````
Project Description:

This is the next generation of HID API for Pd and Max/MSP.
The aim is to have this object perform the same on Pd on
GNU/Linux, Mac OS X, and Windows, and Max/MSP on Mac OS X
and Windows. 

Hans-Christoph Steiner <hans@eds.org> 
Olaf Matthes <olaf@nullmedium.de> 
David Merrill <dmerrill@media.mit.edu>
````
