XPrivacy
========

Privacy manager using the [Xposed framework](http://forum.xda-developers.com/showthread.php?t=1574401)

Description
-----------

XPrivacy can prevent leaking privacy sensitive information for any application
(including associated background services and content providers).
XPrivacy can restrict the types of information an application can access.
This is done by feeding an application with no or fake data.
There are several easy to use information type groups, for example *contacts* or *location*.
Restricting for example access to contacts for an application,
will result in sending an empty contact list to the application.
Similar, restricting access to your location for an application,
will result in sending random locations to the application.

XPrivacy doesn't revoke permissions from an application,
which means that most applications will continue to work as before and won't force close.
There is one exception to this, access to external storage (typically an SD card) is restricted by denying access.
There is no other way to realize this, since this permission is handled by Android in a special way.
Android delegates handling of this permission to the underlying Linux file system.

You can always allow an application access to an information type again
in case restricting the information type resulted into problems for the application.

Any new installed application will have no access to any information type
to prevent leaking privacy sensitive data from the beginning.
Soon after installing a new application
XPrivacy will ask which information types you want the new application to allow access to.
XPrivacy comes with a batch editor, which allows you to easily enable or disable access to an information type
for applications selected from a list of all installed applications.

To help you identify potential information leakage,
XPrivacy will monitor (attempts of) information usage for all applications.
XPrivacy will highlight an information type for an application (or an application name in the batch editor)
as soon as information of the information type has been used.
XPrivacy will also display if an application has internet access
and if an application has permissions to access an information type
(not in the batch editor, since checking permissions for all applications is quite slow).

XPrivacy also allows you to prevent starting an application at boot (when Android starts),
which not only prevents leaking information at that moment, but will also make your device start faster.

XPrivacy is accessible for each application from the Android manage apps menu.
The batch editor is accessible from the application list or drawer.

XPrivacy is built using the Xposed framework.
XPrivacy taps into a number of selected functions of Android through the Xposed framework.
Depending on the function XPrivacy conditionally skips execution of the original function
(for example when an application tries to set a proximity alert)
or alters the result of the original function (for example to return empty calendar information).

XPrivacy has been tested with CyanogenMod 10 and 10.1 (Android 4.1 and 4.2),
and will likely work with any Android version 4.1 or 4.2 variant, including stock ROM's.
Root access is needed to install the Xposed framework.
Because of a bug in the Xposed framework, XPrivacy currently needs a fixed Xposed binary,
which is provided as download.

If you encounter any bug or information leakage please [report an issue](https://github.com/M66B/XPrivacy/issues).
If you have any question or want to request a new feature, you can leave a message in the XDA XPrivacy forum thread.

**Using XPrivacy is entirely at your own risk**

Permissions
-----------

Currently implemented:

* APN info
* Boot start apps (including content providers)
* Browser (bookmarks, searches, etc)
* Calendar
* Contacts
* Identification (Android ID, Wi-Fi MAC address)
* Location (coarse/fine, cell location/info)
* Messages (SMS/MMS, voicemail: **untested**, ICC SMS)
* Phone (call log, in/outgoing/voicemail number, phone ID/number, subscriber ID, SIM info, ISIM, IMPI, IMPU, MSISDN, network details)
* Take photos (Media)
* Record audio (Media)
* Record video (Media)
* Accounts (auth token)
* Read sdcard (revoke permission)
* Restriction management
* Batch edit restrictions
* Default restrict new apps

Planned:

* System log
* Battery info
* Application info
* CM10.1 support

Installation
------------

* Root your device
* **Make a backup**
* Install the [Xposed framework](http://forum.xda-developers.com/showthread.php?t=1574401)
* Install XPrivacy from [here](http://goo.im/devs/M66B/xprivacy)
* Enable XPrivacy from the Xposed Installer app
* Flash the Xposed fix from [here](http://goo.im/devs/M66B/xprivacy) **CM10 only**
* Reboot

Usage
-----

* Select *Manage apps* from the main menu
* Select an app
* Press the XPrivacy button

To see it in action: try disabling *Identification* for [Android Id Info](https://play.google.com/store/apps/details?id=com.bzgames.androidid)
or try disabling *Contacts* for the Contacts app.

**Applying some restrictions requires an app restart**

Enabling storage restriction means blocking access to external storage (typically the SD card).
Because of the nature of this restriction, there is no usage data for this restriction.
All other restrictions have usage data and send no or fake data.
The only exception is boot complete: this is not really a restriction,
but makes it possible to block an application for doing things when the system starts.

Frequently asked questions
--------------------------

* Will you restrict internet access? No, you can use a firewall app, like [AFWall+](https://play.google.com/store/apps/details?id=dev.ukanth.ufirewall).
* Will you block outgoing SMS/MMS, the iptables command or force online state? No, XPrivacy is about restricting information, not about blocking actions.
* Will you make it possible to enter fake information? No, I want to keep things as simple as possible for maximum stability.
* Which functions are exactly restricted? See [here](https://github.com/M66B/XPrivacy/blob/master/src/biz/bokhorst/xprivacy/XPrivacy.java).

Similar solutions
-----------------

* [PDroid](http://forum.xda-developers.com/showthread.php?t=1357056)
* [PDroid 2.0](http://forum.xda-developers.com/showthread.php?t=1923576)
* [OpenPDroid](http://forum.xda-developers.com/showthread.php?t=2098156)

Developers
----------

To restrict new info:

* Find the package/class/method that exposes the info (look into the Android documentation/sources)
* Figure out a way to get a context (see existing code for examples)
* Create a class that extends [XHook](https://github.com/M66B/XPrivacy/blob/master/src/biz/bokhorst/xprivacy/XHook.java)
* Hook the method in [XPrivacy](https://github.com/M66B/XPrivacy/blob/master/src/biz/bokhorst/xprivacy/XPrivacy.java)
* Write a before and/or after method to restrict the info
* Do a [pull request](https://help.github.com/articles/using-pull-requests) if you want to contribute

License
-------

GNU General Public License version 3

Copyright (c) 2013 [Marcel Bokhorst](http://blog.bokhorst.biz/about/)

This program is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation; either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program; if not, write to the Free Software
Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA  02110-1301  USA
