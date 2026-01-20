# subject: [[git]]
## topics: #git
--- 
## introduction:
git is a type of **Version Control System (VCS)** used to keep code updated/in the correct version, roll back when a critical error occurs, among various other functions. it is essential when working in teams, and even alone. git is responsible for allowing us to interact with GitHub and organize our files and projects.

## snapshots:
git works with **snapshots**, basically it takes a picture of all your project files every time its state is changed, either by commits or saves. to be efficient, git doesn't take a picture of files if nothing has been changed. git treats data as if it were a **photo album**. this is an important distinction between git and other VCSs.

## local operations:
most operations performed with git are done using only **local files and resources**, generally no information from another computer or network is necessary. this is possible because your project's entire history is saved on your **local disk**, git takes advantage of this to make operations seem almost **instantaneous**. for example, if you want to see the differences between your project's current files and the same project from 1 month ago, git simply calculates which files were present at that time and which are present now.

## integrity:
everything in git undergoes a **checksum** before being stored, and then this checksum becomes the **reference point** for all changes made to the project. this means it's **impossible** to change the content of a file or directory **without git knowing** about their existence. because of this, it's impossible to **lose** any information or have any file **corrupted** without git detecting it before something like that happens. the mechanism git uses to create these checksums is called a **SHA-1 hash**. it's a 40-character string of 0-9 and a-f. a SHA-1 hash looks like this: `24b9da6552252987aa493b52f8696cd6d3b00373`.