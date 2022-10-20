# compsoc-git-giag

## Generating your ssh key

Creating an ssh key and adding it to your github account means your computer will have access to your account's repositories.

#### Generating ssh keys
```bash
ssh-keygen -t rsa -b 2048
```

From here, you will be given some prompts, one for the file location (at university the `.ssh` folder will have to go in your /u drive, on personal computers, the `.ssh` folder will generally live in the /c drive), the next two will be to add a passphrase; the passphrase doesn't need to be added.

<br>

You then want to copy the public key and add that to your github.

#### Output your public key
```bash
cat <path-to-.ssh>/id_rsa.pub
```

## Configure your git

Now you've got the ssh key set up, you just need to configure your git on your machine. This just includes setting the name and email address that match your github account.

```
git config --global user.name "<your-username>"
git config --global user.email <your@email.com>
```

Note that there are quotation marks around the username and not the email.

## Create your first repo
If you create the repo with a README, you can simply clone the repo, rather than going through the trouble of initialising them.

#### Cloning the repo
```bash
git clone <ssh-repo-code>
```

<br>

## Your first commit
To commit changes to a repository, you need to go through 3 stages. You first stage your changes (add), then commit your changes locally (commit), and then push it to the remote (push).

<br>

First step is to create a text file as an example.

#### Add the file to the staging area
```bash
git add file-name.txt
```
#### Alternatively, add everything in the current directory
```bash
git add .
```

#### Check that all your changes are staged
```bash
git status
```
If the changes have been staged, the file will show in green, if not, it will be red.

#### Commit your changes
```bash
git commit -m "your message."
```
NOTE: adding a commit message is important, make sure it is informative and makes clear what was changed with the commit.

#### Push your changes
```bash
git push
```


## What do I do if someone else made a change?
To get the changes somebody else has made to the repo onto your local machine, simply use

```bash
git pull
```

If there are conflicts here, you can stash your changes. You may also want to just reset your repository to what it is currently if there are conflicts (given you haven't contributed anything of value) using

```bash
git checkout -- .
```

<br>

To stash your commit use

```bash
git stash
```

to put the stashed changes back in, you can use

```bash
git stash apply
```

## What do I do if I broke something?
Go into github and find the commit that you want to go back to. Copy the commit hash, now you can get everything back to this stage.

#### Checkout at that commit
```bash
git checkout <commit-hash> .
```

NOTE: Don't forget the `.`!! If you miss this, the HEAD will become detatched, and you will no longer be on a branch.

<br>

After doing this, you can stage, commit, and push your changes.

<br>

## Committed something you want to get fix up?
To solve this problem, just make a new commit, but don't push yet!

<br>

After committing, you need to rebase. This means changing the record of your commit history. You only need to change the last commit.

```bash
git rebase -i HEAD~2
```

From here, just replace `pick` with `f` and then save and quit.

<br>

Because you have now diverged from the general course of the branch, you will have to force push your changes.

```bash
git push --force-with-lease
```

is the safer option, but equally, when working on a project on your own

```bash
git push -f
```

also works.

<br>

## Branches

#### Create a new branch

```bash
git checkout -b <branch-name>
```

To push to the branch, you will have to set the upstream:

```bash
git push --set-upstream origin <branch-name>
```

To switch back to the main branch simply

```bash
git checkout <branch-name>
```

To list all the branches you have created
```bash
git branch
```

To see all of the ones (including on remote)

```bash
git branch -a
```

#### Merge the other branch in

```bash
git merge <other-branch>
```