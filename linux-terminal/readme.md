# Linux and Terminal Learnings and Reference Page  
This page was created to store random notes, throughts, and snippets regarding:  
- Linux, its subsystems and behaviour, etc.  
- Bash and other linux-y shells, specifically commands that I forget about or haven't yet learned.  

The primary resource for these notes was through reading [Ryans Tutorials](https://ryanstutorials.net/linuxtutorial/).  

NOTE: I made a best-effort to verify these work in Windows PowerShell, but do not guarantee I made note of successes or any errors while doing so.

## Linux Facts and Figures
Many of these concepts will also apply to Unix and other unix-based operating systems.  

## Everything is a file.
- System will have read, write, or both permissions, based on what the file represents and the underlying capabilities.
- An audio card is repreented by System write-only file, for example (meaning System can only write to it).  
- Folders are actually files with different properties than the files they 'contain'.  

## Linux is extensionless
- Windows relies on file extensions to associate an applicable parent or executor program.  
  - Ex: `.txt` is usually associatd with `Notepad.exe` and is of FileTyle `text` or `plaintext`.  
- Linux 'looks inside' a file to determine its 'type'.

## Linux is case SENSITIVE  
- Windows is case INsensitive. 
- Terminal commands in a Linux shell will fail if CaSe rUlEs aRe nOt fOlLoWeD.  
  - This applies to filenames as well for ex: `file_name.txt` is not the same as `FileName.txt`.  

## Quote around spaces
- Use single `'` or double `"` quotation marks to identify a file or folder name that contains a space.  
  - Ex: `ls spacey folder name` returns an error.  
  - Ex: `ls 'spacey folder name'` works.  
  
### Question: Where do quotations go when using `../` notation?  
- `ls '../spacey folder name'` ?  
- `ls ../'spacey folder name'` ?  

## Hidden files
Just prefix the file or folder name with a dot:
- Folder `my_configurations` can be made hidden by renaming to `.my_configurations`  
- File `config` can be made hidden by renaming to `.config`  
> Use `ls -a` to list hidden files in a directory.  

## Linux is full of MANuals
Invoke `man` command followed by the command name you want information about to get an on-screen instruction MANual.  
Exit MAN pages by pressing `q` on the keyboard.  
To search all MAN pages from Terminal: `man -k <search_term>`  
To search terms WITHIN a MAN page display: `/ <search_term>` then press `n` for Next page.  

## Manipulating Files
Create a directory: `mkdir <name>`  
- Create a directory tree: `mkdir <parent_name>/<child_name>`  
Remove files and empty directories: `rm [options] <filespec>`  
- Recursive: `rm -r <filespec>`  
Remove an empty directory: `rmdir <name>`  
- Can be used to remove multiple directories in one command.  
- Directories will not be removed unless they are empty of files and child directories.  
Create a new blank file: `touch <path>/<filename>[.ext]`  
Copy a file or directory: `cp [options] <source_path> <dest_path>`  
- Note: PATHs can be absolute or relative.  
- Remember: Folders ARE files, so both folders and files are part of a path.  
- Recuse over directories: `cp -r <source_path> <dest_path>`  
Move/Rename files or directories: `mv [options] <source_path> <dest_path>`  
- Can move directories without using recuse option.
- Will rename if paths are the same except:  
  - Directory rename: dest_path directory name is only difference  
  - File rename: dest_path filename is only difference  


