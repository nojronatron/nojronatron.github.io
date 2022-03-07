# Linux and Terminal Learnings and Reference Page  

This page was created to store random notes, throughts, and snippets regarding:  

- Linux, its subsystems and behaviour, etc.  
- Bash and other linux-y shells, specifically commands that I forget about or haven't yet learned.  

The primary resource for these notes was through reading [Ryans Tutorials](https://ryanstutorials.net/linuxtutorial/).  

NOTE: I made a best-effort to verify these work in Windows PowerShell, but do not guarantee I made note of successes or any errors while doing so.

## Linux Facts and Figures

Many of these concepts will also apply to Unix and other unix-based operating systems.  

## Everything is a file

- System will have read, write, or both permissions, based on what the file represents and the underlying capabilities.
- An audio card is repreented by System write-only file, for example (meaning System can only write to it).  
- Folders are actually files with different properties than the files they 'contain'.  

## List files

Remember, EVERYTHING is a file so `<pathspec>` actually means `filename` or `foldername/filename` etc.  
List files in current directory: `ls [options] <filespec>`  
There are MANY options, see the LS MAN pages for more.  

## Linux is extensionless

- Windows relies on file extensions to associate an applicable parent or executor program.  
  - Ex: `.txt` is usually associatd with `Notepad.exe` and is of FileTyle `text` or `plaintext`.  
- Linux 'looks inside' a file to determine its 'type'.

## Linux is case SENSITIVE  

- Windows is case INsensitive
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

## Vi Text Editor

This is less critical information (for me, right now, as a Windows user) but should be kept in mind for diving into a linux-based environment (JS/Python full stack dev and webapp dev, etc).

- All CLI, no UI.  
- Two modes:  
  1. Insert/Input Mode: Enter data into a file.  
    - Tap `i` to change to INSERT mode  
    - `--INSERT--` will be displayed at bottom when in this mode  
  2. Edit Mode: Move around the file, add, delete, or copy data, search for data and replace data.  
    - Tap `[esc]` to change to EDIT mode.  
- Launch VI: `vi <filename>`  
  - Will create a new file if `<filename>` does not exist already.  
  - Starts VI in EDIT mode.  
- Command usage
  - Commands starting with a colon require pressing `[Enter]` to execute them.  
- Save and Close (multple options):
  - `ZZ` Save AND Exit.  
  - `:q!` Discard changes and Exit.  
  - `:w` Save changes (without exiting).  
  - `:wq` Save changes and exit.  
  - `:set nu` Sets 'line numbers' in file view.  

  Advice:
  - Use the man pages for more details on commands.  
  - Also check out [Ryans Tutorials VI page](https://ryanstutorials.net/linuxtutorial/vi.php) for more.  

## Display file contents on-screen

- `cat <filespec>` Displays file contents.  
- `less <filespec>` Use arrow keys to scroll up and down, `b` to go "back a page", and `q` to quit.  

## Wildcards

- `*` Zero or more characters.  
  - Remember, these affect the entire pathspec, which includes directories and filenames and file extensions.  
- `?` Single character.  
- `[]` A range of characters.  
Example: `ls [Qq][0-9][0-3]*` results in a listing of files in the current directory whose 1st character is a Q or q, second character is within the range 0 to 9, third character is within the range 0-3, and there are any number of any other characters following.  
- `^` Not. As the first character within a range wildcard causes the filter to eliminate files that match that first character range wildcard characters.  

## Permissions

Linux permissions place rules on what can be done with a file:

- Read: `r`  
- Write: `w`  
- Exectute: `x`  

Linux defines three groups that permissions can be applied to:  

- Owner: Typically the username that created the file.  
- Group: Every file must belong to a single group.  
- Others: Any users not in Owner or Group.  

Show permissions with `ls -l <pathspec>`  
Result example: `-rwxr----x 1 pi owner 1.2K Jan 1 00:00 /home/pi/file.txt`
Dissected, from left to right:  
Character 1: File = `-`, Directory = `d`, so this is a FILE.  
Characters 2, 3 and 4: Owner permissions. Owner members can Read, Write, and Execute this file.  
Characters 5, 6, and 7: Group permissions. Group members can Read this file, but cannot Write nor Execute it.  
Characters 8, 9, and 10: Everyone Else permissions. Users that are not members of Owners or Group can NOT Read nor Write to the file, but the CAN Execute it.  

Change Permissions on a file (meaning everything): `chmod [permissions] [filespec]`  
