```
Hi Team,

The latest functional code is now in the main branch of the repository. Please ensure that any future changes are made using the main branch as the base.

Using the main Branch as the Base for Your Work

Sync Your Local Repository with the Latest main Branch

First, switch to the main branch:

git checkout main  
Pull the latest changes from the remote repository:

git pull origin main  
Create a New Feature/Working Branch from main

Create and switch to a new branch:

git checkout -b your-feature-branch  
Work on Your Changes

Make your edits and commit them to your new branch:

git add .  
git commit -m "Description of your changes"  
Regularly Rebase or Merge Updates from main

To keep your branch up-to-date with the latest changes in main:

git checkout main  
git pull origin main  
git checkout your-feature-branch  
git rebase main  # or use 'git merge main'  
Push Your Branch to the Remote Repository

Push your branch for review:

git push origin your-feature-branch  

Submit a Pull Request

Once your work is ready, submit a pull request to merge your branch back into main.


Deployment Details:

The frontend is deployed on port 3000.
The backend is deployed on port 8000.
You can also use the DNS URL to access the application.
Going forward, there won’t be any further changes to the port numbers.

Let me know if you have any questions.
