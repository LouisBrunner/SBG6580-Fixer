# SBG6580 Fixer

[Try it here!](https://LouisBrunner.github.io/SBG6580-Fixer)

If you own (or lease) a Motorola SGB6580 modem, you may have experienced some difficulty with the Wi-Fi settings.
I got mine from Time Warner Cable and I can't say it has been a real pleasure to use it.

After calling TWC to activate the line, the Wi-Fi that I had correctly configured stopped working.
No more light on the modem. In the settings? A grayed-out dropdown list prevents you to re-enable it.

# The problem

I don't know a lot about telecommunications and ISP processes, but from what I gathered from some Google-fu and a little experiment the cause seems to be the ISP.
TWC (and Comcast too apparently) seems to send a bad opcode/request/answer while initialising the connection and this disable and lock the Wi-Fi module.
(Some people talked about them doing that willingly to ask the customers to pay more to get Wi-Fi... You are free to believe whatever.)

An easy way to verify this problem is to enable the Wi-Fi (or restore it using the following sections), disconnect the coaxial cable, notice the Wi-Fi is working, then reconnect the cable and observe that the Wi-Fi disappeared. Magic!

After digging on the web, I found a lot of sources dissing this model (and the corresponding ISP) because of this problem.
Some solutions were really helpful alas having to be reapplied after each time the modem is rebooted. Mine is slightly better, but more importantly: automated.

# A good working, solution

On this [forum](http://forums.timewarnercable.com/t5/Connectivity/SBG6580-Primary-WiFi-Disabled-and-Grayed-out/m-p/16211#M2427),
a user describes that resetting the modem to factory defaults re-enable the Wi-Fi, but all the configuration has to be done from scratch.
Moreover, this solution has to be reapplied each time the modem is rebooted (and probably after each WAN lease renewal). But at least, it works.

# My solution

I found a slightly better way to fix the problem, but it has the same problems: reboot and probably lease renewal.
It doesn't reset all the modem and doesn't require any reboot or reset, but you will still have to reconfigure the device's Wi-Fi settings.
Because I hate stupid repetitive tasks, I built a script for that (hey, I am lazy person).

You can just go [there](https://LouisBrunner.github.io/SBG6580-Fixer), choose your desired SSID, the Wi-Fi password and edit your gateway credentials (IP, username and password) if you changed them (probably not).
Press the big button and voilà, you have a working Wi-Fi. Thanks ~~Obama~~Time Warner Cable/Comcast!
Each time the Wi-Fi is disabled again, just pop an Ethernet cable, run this script and it will be fixed again. Easy.

# Why it works

You can simply take a look at the code to see how it works, either on the webpage previously linked or more easily on this [repository](https://github.com/LouisBrunner/SBG6580-Fixer/blob/master/index.html).

To create this solution, I looked at the code in the webpages of the administration interface of the modem and found some interesting functions.
Notably one in the Wireless menu named `restoreDefaults`. Weird. There is no "Restore defaults" button in the Wireless interface.
But oddly enough, if you call this method (that only reset an hidden field), and submit the form, the Wi-Fi module is reset.
Including the Enabled/Disabled dropdown! (Which is back to "Enabled" but still grayed-out though.)
So now, you can simply configure your Wi-Fi again and you are done until the next power outage!

If you fear that I would take advantage of that to modify something on your modem, you can simply look at the code, it's only harmless Wi-Fi fixing. Promise. :)

# License

MIT License, Copyright (c) 2015 Louis Brunner
