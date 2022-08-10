# Dnscrypt-Proxy-Maintenance-Script-Android-SH
A script to make managing dnscrypt-proxy (hopefully) a little bit easier via terminal

Okay so ive been using dnscrypt-proxy off and on for years now, and on a desktop its a little bit easier to maintain via the ease of opening up an allowed or blocked names/ips file and then restarting the service. But on Android its a bit of a pain in the butt. For a while i gave up and used Invisible, but that started annoying me and so i came back to dnscrypt-proxy about a year ago and have been using some terminal hacks to maintain it.

Then silly me put my hacky menu system out there for a couple of people to play with, and there was interest in it, so i set about turning what was functional but hacky enough for me to use into something a bit (LOT) more polished...as im sure most people do, the minute they want to release it to others, they agonise over making it more useful and understandable. Making it usable by others ia fricking burden :) Ive rewritten this twice in the last month, leading to delays, to make it more public friendly, hopefully you find it useful. I have removed some of the more fringy options so as to keep it simple and compact, they may or may not make it back in in future.

The script is commented pretty well so should be easy to follow...feel free to suggest changes or features - these are just the ones i find useful 99% of the time and i have some plans to optimize it even further. Theres a bit of clever stuff in it and credit (and a link) is given to the person who's menu code i pinched and wrangled to suit this project.

The user interface is designed as best as i could and with the intention of being as compact and usable above a popup keyboard as i could make it.

And now for the usual mumbo jumbo: This script was written for perosnal use, but slaved over to make actually better for release unto you, the great unwashed. It contains nothing that can harm your device, save for the possible loss of data of a few tct fiels whether by misuse or intentional use of the clearing fucntiosn included. as such its up to yuo to assess whether you feel confortable usign the script, and as mentioned its been well commented to give anyone the ability to peruse before use....which is what i always do, check 3rd party code/script before i run it.

The script is just called **dnshelp** , it is by design made with the intention of being packaged, subject to approval of the packager, of a well maintained dnscrypt-proxy magisk module, but it can be used my anyone with dnscrypt-proxy installed on Android, and with configuration and other userspace files in the usual /sdcard/dnscrypt-proxy/ folder, OR you can adjust the paths in the top of the script if youre for some reason running it outside of the normal path. Allyou need to do is put the script (ideally) somewher ein your path and set the permissions to 755.


## Features (by menu option): ##

### Main Menu: ###

 1) Allow A Domain or IP
 2) Block A Domain or IP
 3) Output or Clear Logs
 4) Sort Allowed Domains/IPs
 R) Restart DNSCrypt-Proxy
 0) Exit

** The main menus status line under the "DnsCrypt-Proxy Maintenance" heading shows the status of dnscrypt proxy, however as you go through the submenus and functions this line changes to show you which menu or function youre currently in 


### 1) Allow A Domain or IP Sub Menu: 

 **1) Allow Recently Blocked Domain(s)**
      
   This menu choice will (by default) grab the last 100 lines of blocked-names.log, sort, then uniq them, and then present the last 30 domains    in a super easy to use multi select menu, where you type the number next to the domain(s) you want to allow (type the number again if you      change yuor mind to deselect). When you ahve selected all the domains you wish to allow, press Enter. **Thats right, no more opening a text    file to type the name of the domain(s) in manually like a cave person.**
    
  As noted, currently by default, until someone suggests a better series of number ranges, its 100 last lines, sorted, uniq'd and then the       last 30 domains. If someone has a better theory, im all ears. I can also easily add the ability to read an options file from sdcard so
  you can set your own if theres any interest. Let me know via Issues here, crack one open and make a suggestion.... 
    
 **2) Allow Recently Blocked IP(s)**

  Same multi select menu as for domains, but for logged IP addresses, if yuo have that enabled, of course.
    
 **4) Allow Domain(s)**
 
  Manual domain entry
 
 **5) Allow IP(s)**

  Manual IP address entry
    
 **m) Return To Main Menu**
 
  Does what it says
 
 **0) Exit**

  Also shouldnt be any surprises with what this does



### 2) Block A Domain or IP Sub Menu:

 **1) Deny Domain(s)**
 
  Manually block a domain
 
 **2) Deny IP(s)**
 
  Manually block an IP
 
 **m) Return To Main Menu**
 
  Does what it says
 
 **0) Exit**

  Also shouldnt be any surprises with what this does



### 3) Output or Clear Logs Sub Menu

 **1) Output Blocked Domains (Readable)**
 
  This chugs through the blocked-names.log file and spits out human (to me, and im barely human) readable entries
    
  It, via some sed work, turns this:
  
  ```
  [2022-07-01 23:24:23]	127.0.0.1	su.ff.avast.com	*.su.ff.avast.com
  [2022-07-01 23:25:57]	127.0.0.1	shavar.prod.mozaws.net	*.shavar.prod.mozaws.net (alias for [shavar.services.mozilla.com])
  ```
  into this:
  ```
  su.ff.avast.com
  shavar.services.mozilla.com
  ``` 
  This is useful to me at least, and is used in some of the functions in the script.  
 
 **2) Clear Blocked Domains Log**
  
  Clears the blocked-names.log, because sometimes its good to do some housecleaning
  
 **3) Clear Blocked IPs Log**
 
  Clears the blocked-ip.log, because sometimes its good to do some housecleaning
 
 **4) Clear Both Logs**
 
  Clears both the blocked-xxxxx.logs, because sometimes its good to do some housecleaning
 
 **m) Return To Main Menu**
  
  Does what it says
  
 **0) Exit**

  Also shouldnt be any surprises with what this does


### 4) Sort Allowed Domains/IPs (Function)
 
No submenu, its simply a function that will sort and uniq the following files in the dnscrypt-proxy folder:
 
 allowed-names.txt
 allowed-ips.txt
 blocked-names.txt
 blocked-ips.txt
 
 
### R) Restart DNSCrypt-Proxy (Function)

No submenu, its simply a function that will just restart dnscrypt-proxy, recommended aftr performing most fucntions, theres a reminder after most functions to do this
