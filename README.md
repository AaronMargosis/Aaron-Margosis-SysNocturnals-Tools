# Aaron Margosis' SysNocturnals Tools

The **"SysNocturnals Tools"** are a set of utilities for the Windows platform, primarily for diagnostic, troubleshooting, and informational purposes. They are inspired 
by and not entirely dissimilar from Microsoft's [Sysinternals](https://www.sysinternals.com) tools, about which I co-wrote the authoritative 
reference books with Mark Russinovich. (BTW, _[Troubleshooting with the Windows Sysinternals Tools](https://www.microsoftpressstore.com/store/troubleshooting-with-the-windows-sysinternals-tools-9780735684447)_
makes a great gift!) I came up with the name "SysNocturnals" rather late at night, which is when I've always done most of my work.

Like the Sysinternals tools, the SysNocturnals tools are entirely free for use. Unlike the current Sysinternals tools, the SysNocturnals
tools' source code is also available and free for use under terms of the MIT license.

While I'm at it, I'm also providing a repository here for binaries and tools that I published on my blogs at Microsoft that are no
longer available on their blog platform, including LUA Buglight, the App Install Recorder scripts, and IEZoneAnalyzer. See “**SysNocturnals Extras**” [here](https://github.com/AaronMargosis/Aaron-Margosis-SysNocturnals-Extras).

## The SysNocturnals tool set

|Name|Description|
|---|---|
|||
|**Troubleshooting tools**||
|||
|[Zombie Finder](https://github.com/AaronMargosis/ZombieFinder/) [`(README)`](https://github.com/AaronMargosis/ZombieFinder/blob/master/README.md) [_(Video presentation)_](https://youtu.be/bKEvxSGhS-M)|Identifies zombie processes/threads and the living processes causing them to be undead.<br>A "zombie process" is the kernel memory leakage of process and thread handles of processes that have exited.|
|[GuiObjectUse](https://github.com/AaronMargosis/GuiObjectUse/) [`(README)`](https://github.com/AaronMargosis/GuiObjectUse/blob/master/README.md)|Reports GUI object use by process in session 0 or other sessions.<br>Its primary use case is to find the root cause of session 0 desktop heap exhaustion.|
|||
|**Management tools**||
|||
|[AppLockerPolicyTool](https://github.com/AaronMargosis/AppLockerPolicyTool/) [`(README)`](https://github.com/AaronMargosis/AppLockerPolicyTool/blob/master/README.md)|AppLocker policy management, through Local GPO and CSP, which is the interface used by MDM providers such as Intune.|
|[RunAsUsers](https://github.com/AaronMargosis/RunAsUsers/) [`(README)`](https://github.com/AaronMargosis/RunAsUsers/blob/master/README.md)|Tool for executing programs in the desktop and security context of interactively logged-on users, from code running as System in session 0.|
|[WindowTool](https://github.com/AaronMargosis/WindowTool/) [`(README)`](https://github.com/AaronMargosis/WindowTool/blob/master/README.md)|Window management tool|
|||
|**Informational tools**||
|||
|[TSSessions](https://github.com/AaronMargosis/TSSessions/) [`(README)`](https://github.com/AaronMargosis/TSSessions/blob/master/README.md)|Enumerates terminal services sessions, window stations, desktops, and more|
|[GetLocalizedResources](https://github.com/AaronMargosis/GetLocalizedResources/) [`(README)`](https://github.com/AaronMargosis/GetLocalizedResources/blob/master/README.md)|Extracts localized text from indirect strings, resource files, and other Portable Executable binaries|
|[RegBinaryToSD](https://github.com/AaronMargosis/RegBinaryToSD/) [`(README)`](https://github.com/AaronMargosis/RegBinaryToSD/blob/master/README.md)|Converts REG_BINARY data to a readable Security Descriptor or SDDL|
|[SddlHelp](https://github.com/AaronMargosis/SddlHelp/) [`(README)`](https://github.com/AaronMargosis/SddlHelp/blob/master/README.md)|Helps with writing and understanding Security Descriptor Definition Language (SDDL), which is a textual means for representing Windows security descriptors, and how to do so for a variety of object types.|
|||
|**Test-scenario tools**||
|||
|[VirtMemTest](https://github.com/AaronMargosis/VirtMemTest/) [`(README)`](https://github.com/AaronMargosis/VirtMemTest/blob/master/README.md)|GUI app for testing memory allocation, CPU-hog, hung-app, and other scenarios|
|[Zombie Maker](https://github.com/AaronMargosis/ZombieMaker/) [`(README)`](https://github.com/AaronMargosis/ZombieMaker/blob/master/README.md)|Creates zombie processes/threads for demonstration/testing purposes (e.g., with ZombieFinder)|
|||
|**SysNocturnals Suite**||
|||
|[SysNocturnalsSuite.zip](https://github.com/AaronMargosis/Aaron-Margosis-SysNocturnals-Tools/releases/download/SysNocturnalsSuite/SysNocturnalsSuite.zip)|All the latest SysNocturnals Tools in one zip file|

### Common features of the SysNocturnals tools

#### x64 and x86 builds
Most but not all of the SysNocturnals tools are provided in x64 and x86 versions, named _`ToolName`.exe_ and _`ToolName`32.exe_. The 32-bit versions will of course
work on 32-bit Windows versions (yes, there still are some), and should work correctly on 64-bit as well, as they will selectively and temporarily disable
WOW64 file system redirection. `AppLockerPolicyTool.exe` and `RunAsUsers.exe` are both x86 only, and will work correctly on all supported Windows versions.

#### Tab-delimited text with headers
The tools' text output is often tab-delimited text with headers. I prefer this format over comma-separated text, as it largely avoids the need of having 
to modify data when it contains embedded delimiter characters (e.g., having to quote text that contains commas and then deal with embedded quotes)
and then determine which is the data and which are added characters that should be removed. Also, tab-delimited text on the clipboard pastes
perfectly right into Microsoft Excel. Tab-delimited CSV is also super easy to work with in PowerShell: pipe it in to ``ConvertFrom-Csv -Delimiter "`t"`` and 
now you've got objects. For example:

``GuiObjectUse.exe | ConvertFrom-Csv -Delimiter "`t" | ?{ $_."User objects" -gt 30 }``

