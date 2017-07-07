#Batch Parameters & Environment

%~1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Expands %1 & removes  surrounding quotation marks<br>
%~f1&nbsp;&nbsp;&nbsp;&nbsp;Expands %1 to a fully qualified path name<br>
%~d1&nbsp;&nbsp;&nbsp;&nbsp;Expands %1 to a drive letter<br>
%~p1&nbsp;&nbsp;&nbsp;&nbsp;Expands %1 to a path<br>
%~n1&nbsp;&nbsp;&nbsp;&nbsp;Expands %1 to a file name <br>
%~x1&nbsp;&nbsp;&nbsp;&nbsp;Expands %1 to a file extension<br>
%~s1&nbsp;&nbsp;&nbsp;&nbsp;Expanded path contains short names only<br>
%~a1&nbsp;&nbsp;&nbsp;&nbsp;Expands %1 to file attributes<br>
%~t1&nbsp;&nbsp;&nbsp;&nbsp;Expands %1 to date and time of file<br>
%~z1&nbsp;&nbsp;&nbsp;&nbsp;Expands %1 to size of file

~~~~
%COMPUTERNAME%    - Returns Computer Name
%UserName%        - Returns UserName
%SystemDrive%     - Windows Drive
%SystemRoot%      - Windows Folder
%Temp%            - Temp Folder
%UserProfile%     - Users profile folder %ALLUSERSPROFILE% - Common profile folder %ProgramFiles%    - Program Files Folder
~~~~

#Useful One-Liners
Get User response<br>
Set /p VarName=StringToEcho 

Set a timeout (**forced** or not)<br>
timeout /t NumberOfSeconds **/NOBREAK**

Copy Folder Structure only (destination exists)<br> 
xcopy /t /e SourceFolder DestinationFolder

File size to Variable<br>
FOR /F "tokens=*" %%A IN (filenameandpath) DO set VarName=%%~zA

# Bits 32 or 64
~~~~
IF "%PROCESSOR_ARCHITECTURE%" == "AMD64" (
	ECHO 64-bit system
	ECHO.
	set bitdec=1
	set blev=64
) ELSE IF "%PROCESSOR_ARCHITEW6432%" == "AMD64" (
	ECHO 64-bit system
	ECHO.
	set bitdec=1
	set blev=64
) ELSE IF "%PROCESSOR_ARCHITECTURE%" == "x86" (
	ECHO 32-bit system
	ECHO.
	set bitdec=1
	set blev=32
) ELSE (
	ECHO 32 or 64 bit Unknown!
 	ECHO.
	set bitdec=0
)

echo.

if %bitdec% == 0 (
	echo Choose bits
	echo 3 32 bit machines
	echo 6 64 bit machines
	echo.
	set /p bit=[3,6]?
	echo.
	echo.
	if "%bit%"=="3" set blev=32
	if "%bit%"=="32" set blev=32
	if "%bit%"=="6" set blev=64
	if "%bit%"=="64" set blev=64
)
~~~~
# FOR IN
~~~~
FOR-Files
       FOR %%parameter IN (set) DO command 
   
FOR-Files-Rooted at Path   
       FOR /R [[drive:]path] %%parameter IN (set) DO command 
   
FOR-Folders
       FOR /D %%parameter IN (folder_set) DO command 
   
FOR-List of numbers   
       FOR /L %%parameter IN (start,step,end) DO command 
   
FOR-File contents   
       FOR /F ["options"] %%parameter IN (filenameset) DO command 
   
       FOR /F ["options"] %%parameter IN ("Text string to process") DO command
   
FOR-Command Results 
       FOR /F ["options"] %%parameter IN ('command to process') DO command
~~~~
**options**:

- **set** A set of one or more files, separated by any standard delimiter. Wildcards can be used
- **folder_set** A set of one or more foldersWildcards must be used
- **/r** Recurse into subfolders
- **delims=xxx** The delimiter character(s) (default = a space)
- **skip=n** A number of lines to skip at the beginning of the file
(default = 0)
- **eol=;** Character at the start of each line to indicate a comment 
The default is a semicolon ; 
- **tokens=n** Specifies which numbered items to read from each line 
(default = 1)
- **usebackq** Use the alternate quoting style: 
	- Use double quotes for long file names in filenameset
	- Use single quotes for Text string to process
	- Use back quotes for command to process
- **Filenameset** A set of one or more files.
- **command_to_process** The output of the 'command_to_process' is 
passed into the FOR parameter.
- **command** The command to carry out, including any 
command-line parameters
- **%%parameter** A replaceable parameter: 
in a batch file use %%G (on the command line %G)

# Find the Windows Drive
~~~~
@echo off
setLocal Enabledelayedexpansion

for %%d in (c d e f g h i j k l m n o p q r s t u v w x y z) do (
	if exist %%d:\Windows\System32\ (
		set drv=%%d
	)
) 
~~~~
