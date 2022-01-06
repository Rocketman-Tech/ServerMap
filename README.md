# Server Map

Creates a map of Jamf Pro server objects to see which are in use and which can be deprecated/deleted.

<!-- TOC depthFrom:2 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Usage](#usage)
- [Examples](#examples)
- [Sample Output](#sample-output)
- [Where's the source code?](#wheres-the-source-code)
- [TODO](#todo)
- [Disclaimer](#disclaimer)

<!-- /TOC -->

## Usage
The following parameters are required:

- **-u | --url** - Full URL to server (e.g. --url='https://rocketman.jamfcloud.com')
- **-l | --login** - Username (e.g. -l rocketman)
- **-p | --pass** - Password - It is ***strongly*** advised to single quote this parameter

## Examples

```txt
  ./servermap -u 'https://rocketman.jamfcloud.com' -l healthcheck -p 'Jamf1234!'
  ./servermap --url='https://rocketman.jamfcloud.com' --login=healthcheck --pass='Jamf1234!'
```

## Sample Output

Note: The numbers in parenthesis at the end of the line refer to the object ID. For example, in the abbreviated sample output below, there are the following lines:

```txt
Active Scripts:
---------------
Easy Button (1)
	SS: Easy Button (48)
```

This says that the script, "Easy Button" has a script ID of 1 and is deployed in the policy, "SS: Easy Button" which has a policy ID of 48.

```ext
Creating tables...
Getting scripts...
Getting packages...
Getting extension attributes...
Getting policies...
Getting profiles...
Getting groups...
Creating Reports...



Disabled Policies:
------------------
0. Jamf Connect Launch Agent and Designs (53)
0. Rosetta (50)
1. Firefox (44)
2. Google Chrome (43)
3. Microsoft Office (45)
4. Cache Install macOS Big Sur.app (47)
macOS Update (57)
SS Easy Button M1 (54)
SS: Easy Button (48)

Active Scripts:
---------------
Easy Button (1)
	SS: Easy Button (48)
Install Rosetta (2)
	0. Rosetta (50)
Easy Button M1 (4)
	SS Easy Button M1 (54)
Install TeamViewer (6)
	TeamViewer Deployment (55)
Bootstrap : Install (7)
	Bootstrap Token Install (56)
Bootstrap : Password Prompt (8)
	Bootstrap Token Install (56)
Onboarding with DEPNotify (10)
	0.0 Onboarding (59)
Cisco AnyConnect Choices XML (11)
	1.1 Cisco AnyConnect (61)
Backdoor Admin 3.0 (27)
	Backdoor Admin 3.0 (77)

Orphaned Scripts:
-----------------
onboarding.sh (5)
Bootstrap : Install Backdoor Admin (14)
CIS Remediation: Login Window (20)
CIS Remediation: Disable Content Caching (23)
CIS Remediation: Screen Saver Get Inactivity Interval (24)
CIS Remediation: Time Zone Set Automatically (26)

Packages in use:
----------------
NoMAD.pkg (24)
	1.2 NoMAD (62)
NoMAD-LaunchAgent.pkg (25)
	1.2 NoMAD (62)
Firefox 85.0.pkg (36)
	1. Firefox (44)
Google Chrome 88.0.4324.146 .pkg (37)
	2. Google Chrome (43)
RocketmanLogoandBackground.pkg (39)
	0. Jamf Connect Launch Agent and Designs (53)
JamfConnectLaunchAgent.pkg (40)
	0. Jamf Connect Launch Agent and Designs (53)
TeamViewer.dmg (43)
	TeamViewer Deployment (55)
Microsoft_Office_16.54.21101001_BusinessPro_Installer.pkg (44)
	1.3 Install Microsoft Office (63)
DEPNotify v1.1.6.pkg (45)
	0.0 Onboarding (59)
Enrollment Videos.pkg (46)
	0.0 Onboarding (59)
Rocketman R.pkg (54)
	0.0 Onboarding (59)
Rocketman-VPN.xml-BigSur.pkg (55)
	1.1 Cisco AnyConnect (61)
JamfConnectLaunchAgent2.5.pkg (59)
	Jamf Connect (74)
Jamf Connect 2.6.pkg (60)
	Jamf Connect (74)

Orphaned Packages:
------------------
VLC 3.0.6.pkg (17)
VMware Fusion 11.1.0.pkg (18)
Dropbox 74.4.115.pkg (19)
GoogleChrome_74.0.3729.169.pkg (20)
Google Chrome 75.0.3770.80.pkg (21)
Google Chrome pref.pkg (22)
NoMADLoginAD-1.2.2.pkg (26)
JamfConnectSync-1.0.9.pkg (30)
JamfConnectSyncLA-1.0.pkg (31)
JamfConnectLoginOkta-1.6.0.pkg (32)
Google Chrome.pkg (33)
JamfConnect.pkg (35)
TeamviewerChoices.pkg (42)
JamfConnect-2.5.0.pkg (58)

Extension Attributes in Groups:
-------------------------------
Battery Health Status (4)
	M: Battery is dying (12)
Bootstrap (7)
	Bootstrap Token : Installed (20)
	Bootstrap Token : Not Installed (21)
Chipset (6)
	M: M1 and Big Sur Cached (18)
	S: M1 (17)

Orphaned Extension Attributes:
------------------------------
Last Reboot (1)
Battery Health (2)
Battery Health Status (Jamf Nation) (5)
Secure Token users (8)
Bootstrap Crypto Users (9)
Breakglass Admin Password (10)

Groups in use by other objects:
-------------------------------
macOS Big Sur Cache (16)
	Policy
		SS: Easy Button (48)
	SubGroup
		M: M1 and Big Sur Cached (18)
S: M1 (17)
	Policy
		SS: Easy Button (48)
Bootstrap Token : Not Installed (21)
	Policy
		Bootstrap Token Install (56)
S: Has Cisco AnyConnect (23)
	Policy
		1.1 Cisco AnyConnect (61)
S: Has NoMAD (24)
	Policy
		1.2 NoMAD (62)
Exclusions (31)
	Profile
		Rocketman Wifi (46)
		AnyConnect PPPC (47)
		NoMAD Configuration (48)
		Approved AnyConnect System and Kernel Extensions (54)
		McAfee System Extension (55)
R: Jamf Connect Pilot (32)
	Profile
		GUI Jamf Connect AZURE (56)
		GUI Jamf Connect Login AZURE (61)

Orphaned Groups:
----------------
Bootstrap Token : Installed (20)
M: Battery is dying (12)
M: Has Branding (15)
S: Does Not Have InTune Company Portal App (13)
S: Has Company Portal (14)
S: Has Google Chrome (10)
S: Pilot Computers (11)
```

## Where's the source code?

This script is built in Python 3.x and (currently) relies on a number of libraries that have to be installed in order to use it. Not to mention, the code is _very experimental_ and, if I'm honest, embarrassing to look at.

Once the executable version has been tested a bit more, a few more features are added, and I've had a chance to clean up the code; we'll look at releasing the source as well.

## TODO
- [ ] Clean up output
  - [ ] Add options for which sections are included
  - [ ] Create a markdown format option
- [ ] Add list of ~~disabled or~~ un-scoped policies
- [ ] Add list of un-scoped configuration profiles

## Disclaimer
This code is ***extremely*** alpha test right now. There is a lot of functionality that needs to be added and the output is hideous. And while it uses get/read-only calls to the API, we still can't guarantee that it won't rise up and destroy all the humans or something. So... no promises, okay?
