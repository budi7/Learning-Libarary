# I. Create Repo From Existing Project
**Case :**  
I allready create a real working project, and i need to upload to Source Control Managamenet Platform

**Environment**  
- SCM : Git  
- SCM Service : Github  
- SCM Tools : VS Code - Source Control Tool

**Step By Step**  
1. Create the repo  
Open Github.com, and create new repository. After that, you Quick Setup documentation will be showed up.

2. Follow the instruction on "**…or create a new repository on the command line**" section

3. Go to terminal and run **git init**

4. Are you need to ignore files?  
**What is that?** Git will ignore file/directory from your list, so it wont be synced. For example, you have configuration file (.env) file consist of any API keys / your web settings that you dont want people see it on your github repo, so the gitignore there for you.  
**How to use?** create a .gitignore file on your base directory. then type your list of directory or file within it.

5. Add remote repo
type on terminal **git remote add origin "your repo url"**

6. First Commit  
**What is commit?** *A commit, or "revision", is an individual change to a file (or set of files). It's like when you save a file, except with Git, every time you save it creates a unique ID (a.k.a. the "SHA" or "hash") that allows you to keep record of what changes were made when and by who. Commits usually contain a commit message which is a brief description of what changes were made.* - according to Github official.  
Go to visual studio and go to **source control** or press ctrl+shift+g. Write commit title, and click the tick button to commit. Wait till done.

7. Push  
**What is push?** *Pushing refers to sending your committed changes to a remote repository, such as a repository hosted on GitHub. For instance, if you change something locally, you'd want to then push those changes so that others may access them.* - according to Github official.  
So go to triple dots beside the tick button on visual studio, click and the dropdown menu wil popped up. Choose push. Wait, enter your github username and password if needed, and you're done. Headback to your repo on github and you can see your project would be there.