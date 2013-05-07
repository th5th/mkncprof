# mkncprof

## Objectives

1. Learn about system calls
1. Write a useful "glue-style" tool for creating netctl wireless profiles.

## Design

The end tool will consist of the following calling syntax.

mkncprof \[-d | --dry-run\] \[-e | --essid essid\_hint\] profname

Invoking mkncprof as above will cause a full scan on each available wireless interface to be run. If specified, the value of essid\_hint will be used to filter which APs to include in the skeleton profile. The environment's EDITOR will then be invoked, with a skeleton netctl profile in. The ESSID lines will be commented out, allowing the user to select which available network the profile is for, and enter other bits. The skeleton form will be pulled from somewhere (perhaps defualt to /etc/netctl/examples/wireless-wpa or whatever). On exit from the editor, the created temp file will be checked by some vague parseriness before asking the user to confirm it. Unless -d is specified, the file will then be copied to /etc/netctl/profname.

After this point mkncprof will probably output a completion message.

## Starting Points

* Investigate wireless\_tools and iwlist in particular for ioctl / other system calls for AP scanning.
* Figure out environment interaction (getting value of EDITOR, launching a new process).
* Look into netctl profile parsing - possibly rifle through some netctl code, or just write a nice simple one from the netctl and netctl.profile man pages.

