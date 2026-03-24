# Digital Forensics – Data Leakage Case Study

This was my final project for CSC300 (Introduction to Digital Forensics) at the College of Engineering. 
My partner and I were given a forensic disk image of a suspect's PC and tasked with investigating 
a data leakage incident — basically, figuring out what happened, what was leaked, and finding the evidence.


## What the case was about

Someone inside an organization was suspected of leaking confidential data. We had to analyze their 
computer forensically — without changing anything on the disk — and piece together what they did.


## How we investigated it

**First, we verified the evidence was untampered**  
Before touching anything, we generated SHA1 and MD5 hash values for all forensic images to confirm 
they hadn't been modified. This is standard practice in any real investigation.

**Then we dug into the disk**  
Using Autopsy, we examined the partition structure of the PC. The disk had 4 partitions — two were 
unallocated, and two were active (NTFS and exFAT). We focused on the system partition which contained 
Windows files, registry data, and user activity.

**We checked what websites they visited**  
The suspect had both Google Chrome and Internet Explorer installed. Their browsing history told a clear story:
- They searched for *"data leakage methods"*
- They searched for *"leaking confidential information"*
- They visited the FBI's Intellectual Property Theft page
- One site they visited was flagged on a known top-5 data leaking sources list

**We looked at their emails**  
The suspect was using Microsoft Outlook. We found a suspicious email account — `iaman.informant@nist.gov` — 
and recovered communication artifacts from the registry and user profile folder.

**We checked the Windows Registry**  
We traced through the registry hive at:
`System > ControlSet001 > Services > tcpip`
and pulled out network configuration data that supported the investigation timeline.

**Finally, we reviewed the security event logs**  
The Windows Security logs (`Security.evtx`) helped us confirm timing and actions taken on the machine.



## What we found

 Evidence  Details 

 Suspicious searches  "data leakage methods", "leaking confidential information" 
 Flagged websites  FBI IP Theft page + a known data leaking site 
 Email account  `iaman.informant@nist.gov` 
 Hidden executables  .exe files found in the system partition 
 Registry traces | Network activity linked to the suspect's actions 


## Tools we used

 **Autopsy** — our main forensic analysis tool
 **SHA1 / MD5 hashing** — for evidence integrity verification
 **Windows Registry analysis** — NTUSER.DAT, RegBack
 **Browser forensics** — Chrome and IE history recovery
 **Windows Event Viewer** — Security.evtx log analysis
 **Email forensics** — Microsoft Outlook artifact recovery

## What I learned

This project gave me real hands-on experience with how digital investigations actually work — 
from verifying evidence integrity, to recovering deleted or hidden artifacts, to building a 
timeline of what a suspect did on their machine. It made concepts like chain of custody, 
forensic imaging, and artifact analysis feel very real and practical.



*CSC300 – Introduction to Digital Forensics - College of Engineering*
