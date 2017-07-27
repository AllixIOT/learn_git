# INSTALLAZIONE GIT

[GIT download](https://git-scm.com/downloads) - Software GIT ufficiale. 

## Configurazione e setup primo utilizzo: git config 

Da shell configura git digitando i comandi:
```
git config --global user.name "John Smith" 
git config --global user.email john@example.com
```
## Plugin per Visual Studio

[Plugin VisualStudio](PluginVisualStudio.md) - plugin per abilitare _GIT_ per _Visual Studio 2008_. Da _Visual Studio 2015_ esiste un plugin ufficile Microsoft. 

# CREAZIONE DI UN REPOSITORY LOCALE: git init

Richiama la _git bash_ e all'interno della shell, crea una directory (es: _learn_git_)

`mkdir learn_git`

`cd learn_git`

Per inizializzare il repository locale, dall'interno quindi della directory di progetto:

`git init`

viene inizializzato così il repository locale. 
Eseguendo il comando all'interno della repository `ls -la` si notano la directory nascosta _.git_ che contiene le informazioni del repository.


Esiste anche il comando `git init <repo_name>` per creare il repository: ammettiamo di essere in una directory chiamato _worksapce_, da qui digito il comando `git init mio_repo`; viene così creato il repository _mio_repo_ sotto la directory _workspace_.

Vedi anche [git clone](#clonazione-di-un-repository-remoto-git-clone)

# ANALISI REPOSITORY: git status

Comando `git status`

```
cam@DESKTOP-6FO16O4 MINGW64 /d/ALLIX/learn_git (master)
$ git status
On branch master

Initial commit

nothing to commit (create/copy files and use "git add" to track)
```
# SALVARE I CAMBIAMENTI AL REPOSITORY: git add e git commit

Per salvare nel repository un file o più file della working area è necessario:
1. aggiungere le risorse da salvare nel repository all'area di staging: `git add`
1. eseguire la commit: `git commit`

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
Per salvare nel repository locale le modifiche dell'area di _staging_, eseguire `git commit` 

```
$ git commit
[master (root-commit) e0194cd]  Initial commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 pippo.txt

cam@DESKTOP-6FO16O4 MINGW64 /d/ALLIX/learn_git (master)
```
esegui il comando `git log` per vedere lo storico delle commit o _commit history_

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
Vedi per approfondire [Commit history](COMMIT_HISTORY.md).

# .gitignore

Se vogliamo che alcuni tipi di file siano ignorati da git, vanno inseriti nel file _.gitignore_ da creare nella directory di progetto. Anche questo file in genere viene salvato nel repository.

Ad esempio in genere non vengono salvati gli eseguibili e quindi in _.gitignore_ si nette una riga:

```

#.gitignore esempio

*.exe

```

In genere in file _.gitignore_ si specificano directory e pattern di file. 

\# è usato per il commento su linea.

[Qui esempio](VisualStudio.gitignore) di un template di _.gitignore_ per ambiente Visual Studio.

I file _.gitignore_ si possono creare anche in sottodirectory e vengono in genere inseriti in caso si voglia creare una directory vuota che venga salvata nel repository; le directory vuote non vengono salvate da git, allora nella directory si crea un file _.gitignore_ che essendo un file fa si che l'operazione commit salvi anche la directory vuota.

Es tipico, la directory di log: si vuole che la directory dei log sia presente sul repository ma non il contenuto, i file di log, che non devono essere salvati su repository. 

# CREAZIONE DI UN REPOSITORY REMOTO 

Creazione account su GitHub https://github.com

Crea un repository public con un nome.

![repo start](https://raw.githubusercontent.com/AllixIOT/learn_git/master/new_repo1.PNG)

![repo conf](https://raw.githubusercontent.com/AllixIOT/learn_git/master/new_repo2.PNG)



# Aggiunta al REPOSITORY LOCALE del REPOSITORY REMOTO: git remote add

Una volta creato un repository remoto, è necessario agganciarlo al repository locale:

`git remote add <remote_name> <remote_repo_url>`

_<remote_name>_ in genere _origin_ per convenzione

_<remote_repo_url>_, url del repository remoto


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
# REPOSITORY to REPOSITORY COLLABORATION: git push

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
# CLONAZIONE DI UN REPOSITORY REMOTO: git clone

Se un progetto è già presente su un repository centrale, è possibile con `git clone <repo_url>` 
ottenere una copia locale.

_<repo_url>_ è l'indirizzo della repository remoto che si vuole clonare.

![repo_clone](https://raw.githubusercontent.com/MassimoCappellano/learn_git/master/clone_repo.PNG)

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
## git init vs git clone

`git init` e `git clone` possono essere facilmente confusi. Ad alto livello, entrambi possono essere utilizzati per inizializzare un repository. Tuttavia, `git clone` è dipendente da `git init`. `git clone` è usato per creare una copia di un repositoty esistente. Al suo interno `git clone` prima chiama `git init` per creare un nuovo repository, poi copia i dati dal repository esistente.

## ESERVIZI DA SVOLGERE: 1° lezione

### ESERCIZIO UNO 

* creare un repository locale;

* committare delle risorse sul repository locale;

* eseguire anche in diversi step più operazioni di `add` e di `commit` sul repository locale;

* verificare con `git log` il contenuto;

* creare un repository remoto su github (pubblico o privato non fa differenza);

* pubblicare il contenuto del repository locale sul repository remoto;

* verificare il contenuto da interfaccia web di github;

* eseguire in un' altra directory l'operazione di `clone` del repository remoto;

## TUTORIALS

https://www.atlassian.com/git/tutorials completare _Getting Start_

poi la parte _Collaborating_ per lavorare con repositori remoti.

## REFERENZE

https://www.atlassian.com/git

[Pro Git](https://git-scm.com/book/it/v2) Book








