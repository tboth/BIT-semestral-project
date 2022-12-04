# BIT-semestral-project
Semestral project for subject Information Technologies Security at FIIT STUBA 2022/23

# DISCLAIMER
!!! This code was developed for educational purposes only, please do not use it for malicious activities. !!!

The goal of this proect was to create a PoC file-less malware attack on Windows 11 using MS Office, PowerShell and VBA macros.
Since this should be a file-less attack, no .exe file should be created on the HDD of the victim, the malware should exist only in the RAM of the computer, masked as another process (in this case, as an Excel instance).

## Approach:
1. Victim obtains the Excel file with malicious vba macro (e.g. as an email attachment)
2. Victim opens the Excel file
3. VBA macro is automatically launched in the Excel file, it should make the following steps:
    * disable Windows Defender
    * disable ASMI - Antimalware Scan Interface
    * download a Powershell script from the attacker's server, which creates a reverse shell to the attacker's server 
    * make the powershell script automatically start on computer startup (by writing entries to the registry)

## Testing
The original approach to test the attack was to create 5 virtual machines with 5 different free antivirus software on them and 
check which of them can or cannot detect the attack. Sine I was not able to disable the ASMI interface, Windows Defender
detected the attack.

## Software setup:
- 1 Linux server - Ubuntu 22.04, rented from digitalocean.com
    * http server - simple http server (python3 -m http.server), from here is the malicious ps script downloaded
    * netcat (OpenBSD netcat (Debian patchlevel 1.187-1ubuntu0.1)), listening for the reverse shell
- 1 Windows 11 VM (Windows 11 Enterprise evaluation, version 2H21), downloaded from https://developer.microsoft.com/en-us/windows/downloads/virtual-machines/
    * MS Office 365 (Version 22.10, build 15726.20202)

## Repo Contents:
- The excel file contains the malicious macro for launching powershell
- The VBA code (also in a seperate file with comments)
- Powershell script for launching reverse shell
- readme file

## Resources:
* https://gist.github.com/egre55/c058744a4240af6515eb32b2d33fbed3
* https://www.excel-pratique.com/en/vba_tricks/vba-obfuscator
* https://amsi.fail
* https://www.youtube.com/watch?v=-hhgiTP_fXQ
