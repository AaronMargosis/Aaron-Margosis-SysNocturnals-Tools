# Aaron Margosis' SysNocturnals Tools

The **"SysNocturnals Tools"** are a set of utilities for the Windows platform, primarily for diagnostic, troubleshooting, and informational purposes. They are inspired 
by and not entirely dissimilar from Microsoft's [Sysinternals](https://www.sysinternals.com) tools, about which I co-wrote the authoritative 
reference books with Mark Russinovich. (BTW, _[Troubleshooting with the Windows Sysinternals Tools](https://www.microsoftpressstore.com/store/troubleshooting-with-the-windows-sysinternals-tools-9780735684447)_
makes a great gift!) I came up with the name "SysNocturnals" rather late at night, which is when I've always done most of my work.

Like the Sysinternals tools, the SysNocturnals tools are entirely free for use. Unlike the current Sysinternals tools, the SysNocturnals
tools' source code is also available and free for use under terms of the MIT license.

## The SysNocturnals tool set

|Name|Description|
|---|---|
|||
|**Troubleshooting tools**||
|||
|[`Zombie Finder`](/ZombieFinder/README.md)|Identifies zombie processes/threads and the living processes causing them to be undead.<br>A "zombie process" is the kernel memory leakage of process and thread handles of processes that have exited.|
|`GuiObjectUse`|Reports GUI object use by process in session 0 or other sessions.<br>Its primary use case is to find the root cause of session 0 desktop heap exhaustion.|
|||
|**Management tools**||
|||
|`AppLockerPolicyTool`|AppLocker policy management, through Local GPO and CSP, which is the interface used by MDM providers such as Intune.|
|`RunAsUsers`|Tool for executing programs in the desktop and security context of interactively logged-on users, from code running as System in session 0.|
|`WindowTool`|Window management tool|
|||
|**Informational tools**||
|||
|`TSSessions`|Enumerates terminal services sessions, window stations, desktops, and more|
|`GetLocalizedResources`|Extracts localized text from resource files and other Portable Executable binaries|
|`RegBinaryToSD`|Converts REG_BINARY data to a readable Security Descriptor or SDDL|
|`SddlHelp`|Helps with writing and understanding Security Descriptor Definition Language (SDDL), which is a textual means for representing Windows security descriptors, and how to do so for a variety of object types.|
|||
|**Test-scenario tools**||
|||
|`VirtMemTest`|GUI app for testing memory allocation, CPU-hog, hung-app, and other scenarios|
|`Zombie Maker`|Creates zombie processes/threads for demonstration/testing purposes (e.g., with ZombieFinder)|

## Common features of the SysNocturnals tools

### x64 and x86 builds
Most but not all of the SysNocturnals tools are provided in x64 and x86 versions, named _`ToolName`.exe_ and _`ToolName`32.exe_. The 32-bit versions will of course
work on 32-bit Windows versions (yes, there still are some), and should work correctly on 64-bit as well, as they will selectively and temporarily disable
WOW64 file system redirection. `AppLockerPolicyTool.exe` and `RunAsUsers.exe` are both x86 only, and will work correctly on all supported Windows versions.

### Tab-delimited text with headers
The tools' text output is often tab-delimited text with headers. I prefer this format over comma-separated text, as it largely avoids the need of having 
to modify data when it contains embedded delimiter characters (e.g., having to quote text that contains commas and then deal with embedded quotes)
and then determine which is the data and which are added characters that should be removed. Also, when tab-delimited text is on the clipboard, it pastes
very easily into Microsoft Excel.
