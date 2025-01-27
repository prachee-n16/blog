---
title: File System
---
**File System**
The file system provides organization for the files through a directory structure and maintains metadata related to files. 

In UNIX, "everything is a file"
- TODO: Look into: https://tldp.org/LDP/sag/html/dev-fs.html
- An area of disk is designates as belonging to a file, and file is just a logical unit to organize this.

Files have the following attributes:
- Name
- Identifier: numerical value that serves as a unique identifier for the file within the file system (find this for a file)
	- there is not much of a difference between this and name
- Type
	- in most OS, any program can open arbitrary files and the extensions are just a suggestion. 
- Location
- Size
- Protection
- Time, Date, User ID

QNX (OS provided by Blackberry) - primarily used in embedded systems
- files are maintained in a structure. Directories are really just like files, information about what files are where, and they are also being stored on disks

There are multiple "[[File Manipulation]]" operations
