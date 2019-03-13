# Intro to @fa[git]
## August Guang

---

## What is @fa[git]?

@ul

 - open source version control tool written by Linus Torvalds (@fa[linux])
 - **version control:** tracks and manages changes to documents, computer programs, and other collections of information

@ulend

---

## Why use git?

@ul

 * Tracking changes over time
 * Helps with collaboration on the same software
 * Protect stable/production code from bugs

@ulend

---

## Webhosts

@size[3.5em][@fa[gitlab]](https://about.gitlab.com)
*Gitlab*
@size[3.5em][@fa[github]](https://github.com)
*Github*
@size[3.5em][@fa[bitbucket]](https://bitbucket.org)
*Bitbucket*

---

## @fa[git] basics

(stuff about forking)

---

## @fa[git] basics

 * **repository or repo:** where documents, software, etc is stored and the changes are tracked

```text
gitintro
├── img
|   └── images.png
├── PITCHME.md
└── README.md
```

---

![](img/git-local-remotes.png)
@size[0.5em][https://hoantran-it.blogspot.com/2016/06/git-tutorial-1-git-committing-and.html](https://hoantran-it.blogspot.com/2016/06/git-tutorial-1-git-committing-and.html)


---

```bash
# check status of your git repo including what's changed
# and what's not being tracked
git status
# add file contents to be ready to be committed
git add FILE 
# commit file contents to the local repository
git commit FILE
# commit all added/modified/deleted file contents with
# specific message
git commit -a -m "commit message"
# push file contents to the remote (i.e. cloud) repository
git push 
```

+++

`git status` reveals that everything is up to date.

```diff
On branch master
Your branch is up to date with 'origin/master'.
```

```text
Working Directory       | Local                   |	Remote
 ---                    | ---                     |
gitintro				| gitintro				  | gitintro
├── img 				| ├── img 				  | ├── img 	
|   └── images.png 		| |   └── images.png 	  | |   └── images.png
├── PITCHME.md 			| ├── PITCHME.md 		  | ├── PITCHME.md 
└── README.md     		| └── README.md           | └── README.md 
```

+++

Let's add a file.

```bash
echo "test" > test.txt
```

```diff
On branch master
Your branch is up to date with 'origin/master'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	- test.txt
```

```text
Working Directory       | Local                   |	Remote
 ---                    | ---                     |
 gitintro                |  gitintro                |  gitintro 
 ├── img        		|  ├── img        		  |  ├── img
 |   ├── images.png   	|  |   ├── images.png     |  |   ├── images.png
 ├── test.txt		    |  └── README.md          |  └── README.md
 └── README.md          |                         |
```


+++

`git add test.txt` adds the file to the staging area.

```bash
git add test.txt
git status
```

```bash
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:  test.txt/
```

```text
Working Directory       | Local                   |	Remote
 ---                    | ---                     |
 gitintro               |  gitintro               |  gitintro 
 ├── img        		|  ├── img        		  |  ├── img
 |   ├── images.png   	|  |   ├── images.png     |  |   ├── images.png
 ├── test.txt 		    |  └── README.md          |  └── README.md
 └── README.md          |                         |
```

+++

`git commit -a -m "test.txt"` actually commits it to local repo.

```bash
git commit -a -m "test.txt"
git status
```

```text
On branch master
Your branch is up to date with 'origin/master'.
```

```text
Working Directory          | Local                      |	Remote
 ---                       | ---                        |
 gitintro                  |  gitintro                  |  gitintro 
 ├── img           		   |  ├── img           		|  ├── img
 |   ├── images.png        |  |   ├── images.png      	|  |   ├── images.png
 ├── test.txt		       |  ├── test.txt         		|  └── README.md 
 └── README.md             |  └── README.md             |  
```

+++

`git push origin master` pushes everything from the local repository to the remote repository.

```bash
git push origin master
git status
```

```text
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)
```


```text
Working Directory          | Local                      |	Remote
 ---                       | ---                        |
 gitintro                  |  gitintro                  |  gitintro 
 ├── img           		   |  ├── img           		|  ├── img
 |   ├── images.png        |  |   ├── images.png      	|  |   ├── images.png
 ├── test.txt     	       |  ├── test.txt         		|  ├── test.txt 
 └── README.md             |  └── README.md             |  └── README.md
```

---

![](img/git-local-remotes.png)

---

```bash
# pull data from remote repo into local repo
git fetch
# merges data from local repo into working directory
git merge
# used to navigate between examplees on the local repo
# need to run git fetch first to pull in examplees
git checkout example
# used to create a new example
git checkout -b NEW_example
# tells you what examplees you have locally and what
# example your working directory is on
git example
# combines fetch & merge all at once
git pull
```

+++

Original structure

```diff
+ remote
master                 | example                   
 ---                   | ---                       
 gitintro              |  gitintro                  
 ├── img       		   |  ├── img           
 |   ├── images.png    |  |   ├── images.png 
 ├── test.txt 	       |  ├── newfile
 └── README.md         |  └── README.md                                           
     

- local
master
 ---                                          
 gitintro                                 
 ├── img                 
 |   ├── images.png
 ├── test.txt                                      
 └── README.md          

- working directory
master
 ---                                          
 gitintro                                 
 ├── img                 
 |   ├── images.png 
 ├── test.txt                              
 └── README.md                
```


+++

`git fetch` pulls data from remote repo into local repo.

```diff
+ remote
master                 | example                    
 ---                   | ---                       
 gitintro              |  gitintro                  
 ├── img       		   |  ├── img           
 |   ├── images.png    |  |   ├── images.png 
 ├── test.txt          |  ├── newfile    
 └── README.md 		   |  └── README.md                                       

- local
master                 | example                    
 ---                   | ---                       
 gitintro              |  gitintro                  
 ├── img       		   |  ├── img           
 |   ├── images.png    |  |   ├── images.png 
 ├── test.txt     	   |  ├── newfile                                         
 └── README.md         |  └── README.md  

- working directory
master
 ---                                          
 gitintro                                 
 ├── img                 
 |   ├── images.png                              
 └── README.md                
```

+++

`git merge` merges everything from local current example into working directory.

```diff
+ remote
master                 | example                    
 ---                   | ---                       
 gitintro              |  gitintro                  
 ├── img       		   |  ├── img           
 |   ├── images.png    |  |   ├── images.png 
 ├── test.txt          |  ├── newfile                                         
 └── README.md         |  └── README.md   

- local
master                 | example                    
 ---                   | ---                       
 gitintro              |  gitintro                  
 ├── img       		   |  ├── img           
 |   ├── images.png    |  |   ├── images.png 
 ├── test.txt          |  ├── newfile                                           
 └── README.md         |  └── README.md 

- working directory
master
 ---                                          
 gitintro                                 
 ├── img                 
 |   ├── images.png
 ├── newfile
 ├── test.txt                                       
 └── README.md # but updated with the one from example!
```

+++

`git checkout example` now pulls in an exact copy from local.

```diff
+ remote
master                 | example                    
 ---                   | ---                       
 gitintro              |  gitintro                  
 ├── img       		   |  ├── img           
 |   ├── images.png    |  |   ├── images.png 
 ├── test.txt          |  ├── newfile                                          
 └── README.md         |  └── README.md 

- local
master                 | example                    
 ---                   | ---                       
 gitintro              |  gitintro                  
 ├── img       		   |  ├── img           
 |   ├── images.png    |  |   ├── images.png 
 ├── test.txt     	   |  ├── newfile                                           
 └── README.md         |  └── README.md 

- working directory
example
 ---                                          
 gitintro                                 
 ├── img                 
 |   ├── images.png
 ├── newfile                           
 └── README.md
```

+++

`git checkout -b NEW_BRANCH` creates a new branch locally and switches the working directory over.

```diff
+ remote
master                 | example                    
 ---                   | ---                       
 gitintro              |  gitintro                  
 ├── img       		   |  ├── img           
 |   ├── images.png    |  |   ├── images.png 
 ├── test.txt     	   |  ├── newfile                                           
 └── README.md         |  └── README.md

- local
master                 | example                 | NEW_BRANCH   
 ---                   | ---                     | ---   
 gitintro              |  gitintro               | gitintro   
 ├── img       		   |  ├── img       		 | ├── img      
 |   ├── images.png    |  |   ├── images.png     | |   ├── images.png
 ├── test.txt          |  ├── newfile            | ├── newfile                 
 └── README.md         |  └── README.md 		 | └── README.md

- working directory
NEW_BRANCH
 ---                                          
 gitintro                                 
 ├── img                 
 |   ├── images.png
 ├── newfile                           
 └── README.md                
```

+++

`git branch` tells you what branch you are on

```bash
git branch
* NEW_BRANCH
  master
```

+++

Note: when pushing changes from `NEW_BRANCH` to remote for first time, you must use `git push origin NEW_BRANCH` in order to set a new (upstream) remote example. Otherwise you will get this error:

```diff
git push
fatal: The current branch NEW_BRANCH has no upstream example.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin NEW_example
```

---

# @fa[git] workflows

---

## gitflow

+++

![](img/gitflow_master_develop.png)
@size[0.5em][https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)

+++

![](img/gitflow_feature.png)

+++

![](img/gitflow_release.png)

+++

![](img/gitflow_hotfix.png)

---

## github flow

[https://guides.github.com/introduction/flow/](https://guides.github.com/introduction/flow/)

---

# fun things

---

## Slack @fa[slack] integration

@ul

 * Can subscribe a channel to a Github repository so everyone in the channel sees commits, pushes, etc and can comment on them
 * Useful for individual projects

@ulend

---?code=src/gitpitch.md

---

## Other integrations: travis, codecov, notebooks

[http://github.com/aguang/transmissim](http://github.com/aguang/transmissim)

---

# Learn more

 * Generally @fa[stack-overflow](http://www.stackoverflow.com) is where I have acquired all of my git knowledge.
 * Atlassian also has [great explanations of everything](https://www.atlassian.com/git/tutorials/using-examplees/git-checkout)