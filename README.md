# INSTALLAZIONE GIT

[GIT download](https://git-scm.com/downloads)

[Plugin VisualStudio](PluginVisualStudio)

# CREAZIONE DI UN REPOSITORY LOCALE

Richiama la _git bash_ e all'interno della shell, crea una directory es: _learn_git_)

`mkdir learn_git`

`cd learn_git`

Per inizializzare il repository locale:

`git init`

## ANALISI REPOSITORY INIZIALE

Comando `git status`

```
cam@DESKTOP-6FO16O4 MINGW64 /d/ALLIX/learn_git (master)
$ git status
On branch master

Initial commit

nothing to commit (create/copy files and use "git add" to track)
```
## FARE UNA COMMIT

Per salvare un file o più file è necessario:
1. aggiungere le risorse da salvare nel repository all'area di staging.
1. eseguire la commit

Aggiungere un file:

`$ touch pippo.txt`

di nuovo git status, cosa notate?

```
$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        pippo.txt

nothing added to commit but untracked files present (use "git add" to track)
```

Uso `git add` per aggiungerlo all'area di _staging_ (o anche detta _index_)

```
$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   pippo.txt


cam@DESKTOP-6FO16O4 MINGW64 /d/ALLIX/learn_git (master)
```
`git log --oneline`

`git commit` 

```
$ git commit
[master (root-commit) e0194cd]  Initial commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 pippo.txt

cam@DESKTOP-6FO16O4 MINGW64 /d/ALLIX/learn_git (master)
```
esegui di nuovo `git log`

Modifica file `pippo` ed esecuzione seconda commit.

```
$ git log
commit e0194cd18b886ffed923d7bce4c5c0fbd4010e62
Author: Massimo Cappellano <Massimo.Cappe@gmail.com>
Date:   Mon Jun 26 20:55:12 2017 +0200

     Initial commit

     Changes to be committed:
            new file:   pippo.txt

cam@DESKTOP-6FO16O4 MINGW64 /d/ALLIX/learn_git (master)
```
```
cam@DESKTOP-6FO16O4 MINGW64 /d/ALLIX/learn_git (master)
$ git log --oneline --all --decorate
e0194cd (HEAD -> master)  Initial commit

cam@DESKTOP-6FO16O4 MINGW64 /d/ALLIX/learn_git (master)
```
Controllo repository remoti.

`git remote -v`

# CREAZIONE DI UN REPOSITORY REMOTO 

Creazione account su GitHub https://github.com

Crea un repository public con un nome.

# Aggiunta al REPOSITORY LOCALE del REPOSITORY REMOTO

```
cam@DESKTOP-6FO16O4 MINGW64 /d/ALLIX/learn_git (master)
$ git remote add origin https://github.com/MassimoCappellano/try_git_example.git

cam@DESKTOP-6FO16O4 MINGW64 /d/ALLIX/learn_git (master)
$ git push -u origin master
Counting objects: 3, done.
Writing objects: 100% (3/3), 252 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
Branch master set up to track remote branch master from origin.
To https://github.com/MassimoCappellano/try_git_example.git
 * [new branch]      master -> master

cam@DESKTOP-6FO16O4 MINGW64 /d/ALLIX/learn_git (master)
```
Ora controlla `git remote`

```
cam@DESKTOP-6FO16O4 MINGW64 /d/ALLIX/learn_git (master)
$ git remote -v
origin  https://github.com/MassimoCappellano/try_git_example.git (fetch)
origin  https://github.com/MassimoCappellano/try_git_example.git (push)

cam@DESKTOP-6FO16O4 MINGW64 /d/ALLIX/learn_git (master)
```
# MODIFICA REPOSITORY LOCALE

modifica file _pippo.txt_

```
cam@DESKTOP-6FO16O4 MINGW64 /d/ALLIX/learn_git (master)
$ vim pippo.txt

cam@DESKTOP-6FO16O4 MINGW64 /d/ALLIX/learn_git (master)
$

cam@DESKTOP-6FO16O4 MINGW64 /d/ALLIX/learn_git (master)
$

cam@DESKTOP-6FO16O4 MINGW64 /d/ALLIX/learn_git (master)
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   pippo.txt

no changes added to commit (use "git add" and/or "git commit -a")

cam@DESKTOP-6FO16O4 MINGW64 /d/ALLIX/learn_git (master)
$ git commit -a -m "modified pippo"
[master 38039f5] modified pippo
 1 file changed, 2 insertions(+)
warning: LF will be replaced by CRLF in pippo.txt.
The file will have its original line endings in your working directory.

cam@DESKTOP-6FO16O4 MINGW64 /d/ALLIX/learn_git (master)
$ git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)
nothing to commit, working tree clean

cam@DESKTOP-6FO16O4 MINGW64 /d/ALLIX/learn_git (master)
```
Ora dice che il branch _master_ è avanti di una commit rispetto a _origin/master_

Esecuzione `git push` 

```
cam@DESKTOP-6FO16O4 MINGW64 /d/ALLIX/learn_git (master)
$ git push origin master
Counting objects: 3, done.
Writing objects: 100% (3/3), 254 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/MassimoCappellano/try_git_example.git
   e0194cd..38039f5  master -> master

cam@DESKTOP-6FO16O4 MINGW64 /d/ALLIX/learn_git (master)

```
# CLONAZIONE DI UN REPOSITORY REMOTO

Per collaborare.

```
cam@DESKTOP-6FO16O4 MINGW64 /d/TEST
$ git clone https://github.com/MassimoCappellano/try_git_example.git
Cloning into 'try_git_example'...
remote: Counting objects: 6, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 6 (delta 0), reused 6 (delta 0), pack-reused 0
Unpacking objects: 100% (6/6), done.

cam@DESKTOP-6FO16O4 MINGW64 /d/TEST
```
Possiblilità di clonare il progetto specificando una directory (da _git help clone_):

```
git clone [--template=<template_directory>]
	  [-l] [-s] [--no-hardlinks] [-q] [-n] [--bare] [--mirror]
	  [-o <name>] [-b <name>] [-u <upload-pack>] [--reference <repository>]
	  [--dissociate] [--separate-git-dir <git dir>]
	  [--depth <depth>] [--[no-]single-branch]
	  [--recursive | --recurse-submodules] [--[no-]shallow-submodules]
	  [--jobs <n>] [--] <repository> [<directory>]
```

## ESERCIZI

https://www.atlassian.com/git/tutorials completare _Getting Start_





