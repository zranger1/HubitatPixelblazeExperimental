
# hubitatpixelblazedriver (experimental version)
Hubitat Elevation device handler for the Pixelblaze addressable LED controller.
This version may have features and bugs not present in the main branch.

## What is a Pixelblaze?
For information on the Pixelblaze, visit its home:  www.electromage.com

Pixelblaze is an ESP32 based programmable LED controller with a fast
fixed-point integer Javascript-like interpreter built in. It's very easy
to create and save complex lighting patterns, animated or not.

## What can I do with this driver?
This driver gives the Hubitat basic control over the Pixelblaze - on/off, brightness,
get pattern list, set active pattern, etc.. It works with Dashboards and RuleMachine on
the hub, so you can coordinate the Pixelblaze with your other home automation devices.

## What's New in the experimental version
You can now subdivide an LED strip into multiple segments and control each one
individually via a child device on the hub.   The segmentation is done on the 
pixelblaze, using a the pattern Multisegment V1.epe, which is in the repo.

Import and run this pattern on your pixelblaze, then install the parent and child
drivers.   Once you've created your device on the hub and connected it to your pixelblaze, 
create the child devices for each segment by pressing the "Get Variables" button, followed by the 
"Reset Children" button.  ("Reset Children alone should do the job, but especially on initial
setup, it helps reliability to "Get Variables" first just to make sure a connection is established.

Each child device controls a segment of the LED strip as though it were an RGB bulb.  The number of 
segments is controlled by code on the pixelblaze side, and can be changed if you (1) know a little
javascript, and (2) follow the naming conventions in the code (e.g. The segment numbering scheme
starts from zero. The control array for the xth segment must be named "z_x". 

Per segment special effects will eventually be supported.  Right now, all the control machinery works
on the hub side, but the rendering code on the pixelblaze side isn't baked yet.

## To Use
Set up your Pixelblaze.  Take note of it's IP address.

On your Hubitat Elevation's admin page, select "Drivers Code", then click the
"New Driver" button.  Paste the Groovy driver code from this repository into 
the editor window and click the "SAVE" button.

Create a new virtual device on your Hubitat, name and label it, and select 
"Pixelblaze Controller" as the device type.  Save your new device.

Click the new device on the Hubitat's "Devices" page, and enter your Pixelblaze's
IP address and port number (which should be *81*) in the provided field.

IMPORTANT: In preferences, Leave the "Use Patterns for On/Off" switch set to OFF.  
If you change the running pattern on the pixelblaze to one that doesn't support segmentation,
the child drivers will stop working.  They will work again when you set the pixelblaze
back to the right pattern, but since the pixelblaze re-initializes its variables when
you load a new pattern, it is not guaranteed that your lights will be in the same state as
when you left them.
 
 
 
 

