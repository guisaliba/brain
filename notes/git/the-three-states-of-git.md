# subject: [[git]]
# topics: #git
---
## git's three states

git has three stages (or states), which are the main mechanism of how everything works. this is the most important concept of this VCS. your files can reside in three different states: **modified**, **committed**, and **staged**.

- **Modified:** this state means that something has been modified in your files/directory but has **not** yet been committed to your database.
- **Staged:** a file in the staged state is a file that has been modified and marked as **ready** to be committed and stored in the next snapshot of your code.
- **Committed:** committed means that your file (or more than one) has been uploaded to the database and is safely stored. in the snapshot taken by git, these files will be there.

these three states introduce us to the concept of git's **working tree**, a workflow.

git's workflow is basically this:

1. you **modify** files in your working tree.
2. you **select** by hand which changes you want to be in the next commit, meaning you put these selected files in **stage**.
3. you make the **commit**, which takes only the selected modified files (**staged**), and stores a permanent **snapshot** in your git directory.

a **git directory** is a folder automatically created by git once you initialize it in your project. it's in this folder that it stores all information about changes, stage, commit, flow, and **.gitignore**, a file where you tell git what it should **ignore**, not including such specified folders or files in the next snapshot.