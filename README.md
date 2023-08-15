# multiple-github-acc-local
How to use multiple accounts on your local

### 1. Generate ssh key
```bash
$ ssh-keygen -t rsa -C "your@email.com" -f "accOne"
$ ssh-keygen -t rsa -C "your-sencond@email.com" -f "accTwo"
```

### 2. Add both ssh keys into ssh agent.
```bash
$ ssh-add ~/.ssh/accOne
$ ssh-add ~/.ssh/accTwo
```

### 3. Create ssh configuration.
```bash
$ touch ~/.ssh/config
```
```config
#account One
Host github.com-accOne
	HostName github.com
	User git
	IdentityFile ~/.ssh/accOne

#account Two
Host github.com-accTwo
	HostName github.com
	User git
	IdentityFile ~/.ssh/accTwo
```
note: Host github.com-accOne or github.com-accTwo is custom host aliases.

### 4. Setting ssh public key into Github ssh key setting.
Copy ssh public key command below.
```
$ cat ~/.ssh/accOne.pub
$ cat ~/.ssh/accTwo.pub
```

### Clone repo
change the url repo.
example if your repo ssh url is `git@github.com:accOne/repo.git` change host after `@` to host aliases. 
```bash
$ git clone git@github.com-accOne:accOne/repo.git
```
### Already clone the repo
then use this command to set new remote url instead.
```
$ git remote set-url origin git@github.com-accOne:accOne/repo.git
```
### Commit And Push
1. config your git commit user emil and username
```bash
$ git config user.email "you@email.com"
$ git config user.name "username"
```
```bash
$ git add .
$ git commit ...
$ git push
```
