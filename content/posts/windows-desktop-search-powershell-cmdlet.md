---
title: "Windows Desktop Search Powershell Cmdlet"
date: 2006-07-31T21:23:24+02:00
---

Microsoft are introducing a new command line shell named PowerShell, previously known as Monad. 
The main difference between PowerShell and other shells like cmd, bash, ksh etc. is the pipelining 
and processing of objects as opposed to plain text.
 
I had previously used the Windows Desktop Search API to write a music browser and thought it would 
be useful to create a Windows Desktop Search Powershell cmdlet to allow users to query their search 
index from the command line. The results of the query can then be pipelined to further cmdlets to 
act on the results or to simply display the result set.
 
A more detailed write up with the source code available for download is available at 
[CodeProject](https://www.codeproject.com/Articles/14602/Windows-Desktop-Search-Powershell-Cmdlet).

