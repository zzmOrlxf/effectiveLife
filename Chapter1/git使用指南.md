# 第2节:git使用指南

If you start a project in the GitHub, these following word would be show:

### …or create a new repository on the command line

```
echo "# Simple-IDEA" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/zzmOrlxf/Simple-IDEA.git
git push -u origin master
```

### …or push an existing repository from the command line

```
git remote add origin https://github.com/zzmOrlxf/Simple-IDEA.git
git push -u origin master
```

### …or import code from another repository

You can initialize this repository with code from a Subversion, Mercurial, or TFS project.



### Your Identity](https://git-scm.com/book/en/v1/Getting-Started-First-Time-Git-Setup#Your-Identity)

The first thing you should do when you install Git is to set your user name and e-mail address. This is important because every Git commit uses this information, and it’s immutably baked into the commits you pass around:

```
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```

Again, you need to do this only once if you pass the `--global` option, because then Git will always use that information for anything you do on that system. If you want to override this with a different name or e-mail address for specific projects, you can run the command without the `--global` option when you’re in that project.

### [Initializing a Repository in an Existing Directory](https://git-scm.com/book/en/v1/Git-Basics-Getting-a-Git-Repository#Initializing-a-Repository-in-an-Existing-Directory)

If you’re starting to track an existing project in Git, you need to go to the project’s directory and type

```
$ git init
```

This creates a new subdirectory named `.git` that contains all of your necessary repository files — a Git repository skeleton. At this point, nothing in your project is tracked yet. (See *Chapter 9* for more information about exactly what files are contained in the `.git` directory you just created.)

If you want to start version-controlling existing files (as opposed to an empty directory), you should probably begin tracking those files and do an initial commit. You can accomplish that with a few `git add` commands that specify the files you want to track, followed by a commit:

```
$ git add *.c
$ git add README
$ git commit -m 'initial project version'
```

We’ll go over what these commands do in just a minute. At this point, you have a Git repository with tracked files and an initial commit.

### Adding Remote Repositories

We’ve mentioned and given some demonstrations of how the `git clone` command implicitly adds the `origin` remote for you. Here’s how to add a new remote explicitly. To add a new remote Git repository as a shortname you can reference easily, run `git remote add <shortname> <url>`:

```console
$ git remote
origin
$ git remote add pb https://github.com/paulboone/ticgit
$ git remote -v
origin	https://github.com/schacon/ticgit (fetch)
origin	https://github.com/schacon/ticgit (push)
pb	https://github.com/paulboone/ticgit (fetch)
pb	https://github.com/paulboone/ticgit (push)
```

Now you can use the string `pb` on the command line in lieu of the whole URL. For example, if you want to fetch all the information that Paul has but that you don’t yet have in your repository, you can run `git fetch pb`:

```console
$ git fetch pb
remote: Counting objects: 43, done.
remote: Compressing objects: 100% (36/36), done.
remote: Total 43 (delta 10), reused 31 (delta 5)
Unpacking objects: 100% (43/43), done.
From https://github.com/paulboone/ticgit
 * [new branch]      master     -> pb/master
 * [new branch]      ticgit     -> pb/ticgit
```

Paul’s master branch is now accessible locally as `pb/master` — you can merge it into one of your branches, or you can check out a local branch at that point if you want to inspect it. (We’ll go over what branches are and how to use them in much more detail in [Git Branching](https://git-scm.com/book/en/v2/ch00/ch03-git-branching).)

  

### [Cloning an Existing Repository](https://git-scm.com/book/en/v1/Git-Basics-Getting-a-Git-Repository#Cloning-an-Existing-Repository)

If you want to get a copy of an existing Git repository — for example, a project you’d like to contribute to — the command you need is `git clone`. If you’re familiar with other VCS systems such as Subversion, you’ll notice that the command is `clone` and not `checkout`. This is an important distinction — Git receives a copy of nearly all data that the server has. Every version of every file for the history of the project is pulled down when you run `git clone`. In fact, if your server disk gets corrupted, you can use any of the clones on any client to set the server back to the state it was in when it was cloned (you may lose some server-side hooks and such, but all the versioned data would be there — see *Chapter 4* for more details).

You clone a repository with `git clone [url]`. For example, if you want to clone the Ruby Git library called Grit, you can do so like this:

```
$ git clone git://github.com/schacon/grit.git
```

That creates a directory named `grit`, initializes a `.git` directory inside it, pulls down all the data for that repository, and checks out a working copy of the latest version. If you go into the new `grit`directory, you’ll see the project files in there, ready to be worked on or used. If you want to clone the repository into a directory named something other than grit, you can specify that as the next command-line option:

```
$ git clone git://github.com/schacon/grit.git mygrit
```

That command does the same thing as the previous one, but the target directory is called `mygrit`.

Git has a number of different transfer protocols you can use. The previous example uses the `git://`protocol, but you may also see `http(s)://` or `user@server:/path.git`, which uses the SSH transfer protocol. *Chapter 4* will introduce all of the available options the server can set up to access your Git repository and the pros and cons of each.



## !!If add a remote repository, you should add URL start with https:// , care abut the protocol, cause clone use git://



## Generating Your SSH Public Key

Many Git servers authenticate using SSH public keys. In order to provide a public key, each user in your system must generate one if they don’t already have one. This process is similar across all operating systems. First, you should check to make sure you don’t already have a key. By default, a user’s SSH keys are stored in that user’s `~/.ssh` directory. You can easily check to see if you have a key already by going to that directory and listing the contents:

```console
$ cd ~/.ssh
$ ls
authorized_keys2  id_dsa       known_hosts
config            id_dsa.pub
```

You’re looking for a pair of files named something like `id_dsa` or `id_rsa` and a matching file with a `.pub` extension. The `.pub` file is your public key, and the other file is the corresponding private key. If you don’t have these files (or you don’t even have a `.ssh` directory), you can create them by running a program called `ssh-keygen`, which is provided with the SSH package on Linux/macOS systems and comes with Git for Windows:

```console
$ ssh-keygen -o
Generating public/private rsa key pair.
Enter file in which to save the key (/home/schacon/.ssh/id_rsa):
Created directory '/home/schacon/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/schacon/.ssh/id_rsa.
Your public key has been saved in /home/schacon/.ssh/id_rsa.pub.
The key fingerprint is:
d0:82:24:8e:d7:f1:bb:9b:33:53:96:93:49:da:9b:e3 schacon@mylaptop.local
```

First it confirms where you want to save the key (`.ssh/id_rsa`), and then it asks twice for a passphrase, which you can leave empty if you don’t want to type a password when you use the key. However, if you do use a password, make sure to add the `-o` option; it saves the private key in a format that is more resistant to brute-force password cracking than is the default format. You can also use the `ssh-agent` tool to prevent having to enter the password each time.

Now, each user that does this has to send their public key to you or whoever is administrating the Git server (assuming you’re using an SSH server setup that requires public keys). All they have to do is copy the contents of the `.pub` file and email it. The public keys look something like this:

```console
$ cat ~/.ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAklOUpkDHrfHY17SbrmTIpNLTGK9Tjom/BWDSU
GPl+nafzlHDTYW7hdI4yZ5ew18JH4JW9jbhUFrviQzM7xlELEVf4h9lFX5QVkbPppSwg0cda3
Pbv7kOdJ/MTyBlWXFCR+HAo3FXRitBqxiX1nKhXpHAZsMciLq8V6RjsNAQwdsdMFvSlVK/7XA
t3FaoJoAsncM1Q9x5+3V0Ww68/eIFmb1zuUFljQJKprrX88XypNDvjYNby6vw/Pb0rwert/En
mZ+AW4OZPnTPI89ZPmVMLuayrD2cE86Z/il8b+gw3r3+1nKatmIkjn2so1d01QraTlMqVSsbx
NrRFi9wrf+M7Q== schacon@mylaptop.local
```

For a more in-depth tutorial on creating an SSH key on multiple operating systems, see the GitHub guide on SSH keys at <https://help.github.com/articles/generating-ssh-keys>.

