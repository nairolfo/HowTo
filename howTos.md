# Regex search in visual studio
return occurences where any any text is in between bla and bla: bla.*bla

# Access bitbucket
https://bitbucket.org/

# install different versions of arangoDB
https://download.arangodb.com/Windows7/x86_64/index.html

# NUGET: Restore packages for all projects in the solution
In the Package Manager Console type: Update-Package -reinstall
-reinstall argument is what instructs Update-Package to RESTORE packages to their currently installed versions 
rather than UPDATING any of those versions.

# Install PipelineManager and KitKatHost as windows service
open CMD as an admin then
C:\Users\fchaumeil\Documents\centro\kit-sp-debug\KitKatHostService\bin\Debug  KitKatHostService.exe install
C:\Users\fchaumeil\Documents\centro\kit-sp-debug\PipelineManager\bin\Debug  PipelineManager.exe install
Note: 
THE SERVICES NEED TO BE UNINSTALLED BEFORE REBUILDING THE APP
otherwise use 
sc delete CentroPipelineManager (CentroPipelineHost, CentroPipelineManager)
to delete uninstallable service
or
(
Remove <service-name> from Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services key in the registry editor
and
End Pipeline Manager (resp KitKat Host Service) process in process explorer
and 
Restart
)
# NUGET:

In VisualSTudio Tools/NuGet package Manager/ NuGet package Manager Console

	PM> dotnet restore
	PM> dotnet restore .\MagnaCasIntegration\MagnaCasIntegration\MagnaCasIntegration.csproj
	PM> dotnet restore .\MagnaCasIntegration\MagnaCasIntegration\MagnaCasIntegration.csproj
	PM> dotnet restore .\MagnaCasIntegration\MagnaCasIntegration\MagnaCasIntegration.csproj -s https://api.nuget.org/api/v3/index.json
	PM> dotnet restore .\MagnaCasIntegration\MagnaCasIntegration\MagnaCasIntegration.csproj -s https://packages.nuget.org/v1/FeedService.svc/
	PM> dotnet restore .\MagnaCasIntegration\MagnaCasIntegration\MagnaCasIntegration.Test.csproj -s https://packages.nuget.org/v1/FeedService.svc/
	PM> dotnet restore .\MagnaCasIntegration\MagnaCasIntegration.Test\MagnaCasIntegration.Test.csproj -s https://packages.nuget.org/v1/FeedService.svc/
	PM> dotnet restore .\MagnaCasBatchJob\MagnaCasBatchJob.csproj -s https://packages.nuget.org/v1/FeedService.svc/
	PM> nuget help restore
	PM> help restore
	PM> ls
	PM> .\.nuget\NuGet.exe help restore
	PM> .\.nuget\NuGet.exe restore
	
	C:\Users\fchaumeil\.nuget
	
# GIT: 

REMOVE ALL local commits from current branch
$ git branch --set-upstream-to mx/master (if no upstream for branch)
$ git reset --hard @{u}

SYNC FORK
$ git merge twixMaster (NOT REBASE)
$ (DON'T D0) git add --all (DON'T D0)
resolve conflict in VS
enter commit msg and commit
$ git push mx HEAD

Clone Repo
$ git clone https://fchaumeil@bitbucket.org/actify-ondemand/magnaex.git
$ git remote add upstream https://fchaumeil@bitbucket.org/actify-ondemand/magnaex.git

Update Remote
$ git remote set-url qm https://fchaumeil@bitbucket.org/actify-ondemand/apm.git

Ignore changes on a particular file
$ git update-index --assume-unchanged KitKatWebApps/Configuration/location.config
$ git update-index --assume-unchanged KitKatWebApps/Configuration/connectionSettingsTemplate.config
$ git update-index --assume-unchanged connectionSettings.config

List of last actions on git (ass saving feature if deleting commit) 
$ git reflog

Navigate to working folder (note : paths are case sensitive)
$ cd ~/Documents/centro/kit

To escape current console query
'ctrl + c'

Add repository to the list of "remotes"
$ git remote add cf git@bitbucket.org:actify-ondemand/creativefoam-dashboard.git
Change repository
$ git remote set-url upstream git@bitbucket.org:actify-ondemand/challenge.git

Open Help webpage
$ git help branch
$ git help checkout

Show repositories or "remotes" whose branches are tracked.
$ git remote -v

List local branches
$ git branch
List all branches remote and local. 
$ git branch -a
Display the Head of each local branch
$ git branch -v
Filter branches by name like
$ git branch --list *notification*


Import all remote branches (e.g. for reviewing code committed on remote repository)
$ git fetch
$ git checkout <branchName>

Switch to branch Master
$ git checkout master

Start working on the Issue Nr #### / creates new branch
$ git checkout -b KIT-#### 

Copy branch
git checkout -b new_branch old_branch

Note:
'git pull' always merges into the current branch

Rename branch (to uppercase)
$ git branch -m kit-#### tmp
$ git branch -m tmp KIT-####

Compare local branch to upstream to test if rebase necessary
$ git status

If changes have been made (two weeks sitting)
Pull upstream master
Rebase


Check commit history
$ git log
display summary of last 10 commit 
$ git log -10 --oneline

Cancel failed pull upstream master
$ git merge --abort

Finds best common ancestor(s) between two commits
$ git merge-base KIT-#### master

Modify commits message
$ git commit -–amend
Undo last commit but keep changes
$ git reset HEAD~
Undo commits after commit-id but keep changes
git reset <commit-id>  
  
Manage (delete, cherry pick, squash ...) commits since <target commit>
$ git rebase -i <target commit>

Checkout/switch/revert code to a specific commit (without creating any new branch, ie in 'detached HEAD' state)
$ git log -10 --oneline
	ddb2cc7 KIT-3709 display a placeholder image when no geometry in a file
	9ac4606 Merged in KIT-3705 (pull request #2954)
$ git checkout ddb2cc7
Performing another checkout in this state will discard all commits.
to retain commits, a new branch  must be created using  $ git checkout -b <new-branch-name>


Apply current changes on top of master 
$ git rebase master 


Send commit changes of branch KIT-#### of local repo to branch KIT-#### of remote repositories
to shared code base
$ git push upstream KIT-####
to personnal fork
$ git push origin KIT-####

Delete KIT-#### from the remote repository   
$ git push --delete upstream KIT-####
alternative commande      
$ git push upstream :KIT-####

use stash
$ git stash
$ git stash list
$ git stash apply stash@{0}
$ git stash drop (drops the top stash, stash@{0}) 
$ git stash drop stash@{n}
$ git stash pop stash@{n} (apply and drop)
$ git stash save 'test snackbar error'


Find what commit broke the code
$ git bisect ( https://git-scm.com/book/fr/v1/Utilitaires-Git-Deboguer-avec-Git )

Patch changes from one branch ( or repo ) to another
get differences into a file patch.diff

$ git diff 719c797..HEAD (if files added stage everything and use --staged here)> patch.diff
copy in windows explorer the file patch.diff
$ cd ../Jvis/
$ git apply patch.diff
$ git status

???
$ git am -3 < patch.diff
$  rm patch.diff
get the merged PRs during the last month
$ git log --merges --after='2018-06-17' --pretty=format:'%h : %s' --graph > log.log

Find the most recent common ancestor of two branches 
$ git merge-base branch2 branch3
$ gitk MAGNAEX-83 MAGNAEX-89

# Angular

Generate new component
>\src\apps\QuoteManWebApp\ClientApp\src\app> ng g c workflow/task-assignment --module <<Specify module eg: ./app>>

Update translation/message.xlf file
>\src\apps\QuoteManWebApp\ClientApp> ng xi18n --output-path locale
	
# VS Code

Move line up or down alt+arrow
Copy line up or down alt+shift+arrow
Box selection shift+alt+mouse select
Cursor on all occurences of a selected string ctrl+shift+l
delete entire line ctrl+shift+k
Comment selection alt+shift+a
F2 rename symbol where the cursor is
format file alt+shift
Customize keyboard shortcuts ctrl k ctrl s







