---
description: Document of all minor bug I have resolved
---

# Minor bug resolved

Problem: The \`git push\` get **authorization deny** because my laptop use the credential of my old Github account

Solution:&#x20;

#### 1. Set git credential to be empty

`git config --local credential.helper ""`

However, this would require you to enter credential for every push

#### 2. Erase the git credential&#x20;

```
$ git credential-osxkeychain erase ⏎
 host=github.com  ⏎
 protocol=https
```

Once you enter the new credential, it will be stored in osxkeychain for future operation



### References

[How do you reset the stored credentials in 'git credential-osxkeychain'?](https://stackoverflow.com/questions/11067818/how-do-you-reset-the-stored-credentials-in-git-credential-osxkeychain)

[Storing Git Credentials with Git Credential Helper](https://techexpertise.medium.com/storing-git-credentials-with-git-credential-helper-33d22a6b5ce7)
