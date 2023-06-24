https://stackoverflow.com/questions/9339429/what-does-cherry-picking-a-commit-with-git-mean

1.  Make sure you are on the branch you want to apply the commit to (e.g. "main")
    ```git
     git switch main
    ```
    
2.  Execute the following:
    ```git
     git cherry-pick <commit-hash>
    ```
What this does mean? Cherry-picking means to take the changes from one branch, and apply it to another branch. (A branch means a single commit here)

Merge and rebase typically move many commits at once, but cherry-pick just moves one.