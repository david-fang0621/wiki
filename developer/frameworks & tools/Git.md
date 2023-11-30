---

# Get Started

## VCS (Version Control System)

- CVCS
- DVCS

## History

- Patch & Single compression in Linux Kennel (1991 - 2002)
- BitKeeper (2002)
- Git (2005)

## Concept

- stream of Snapshot
  ![Monosnap Git - Git 기초 2023-04-03 03-39-24.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/77b657c4-5a12-4eda-8112-0133463ebeae/Monosnap_Git_-_Git_%E1%84%80%E1%85%B5%E1%84%8E%E1%85%A9_2023-04-03_03-39-24.png)
  ![Monosnap Git - Git 기초 2023-04-03 03-39-43.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/987b207a-9ee5-4a9c-96c2-da493ea89c1c/Monosnap_Git_-_Git_%E1%84%80%E1%85%B5%E1%84%8E%E1%85%A9_2023-04-03_03-39-43.png)
- Status - Committed, Modified, Staged (to commit)
  ![Monosnap Git - Git 기초 2023-04-03 03-42-23.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ab4db0d5-bf34-45ef-86b8-d20f9ed5f0cb/Monosnap_Git_-_Git_%E1%84%80%E1%85%B5%E1%84%8E%E1%85%A9_2023-04-03_03-42-23.png)
- Basic workflow
  - Change files in working tree
  - Make snapshots to be committed by staging files in Staging Area
  - Store snapshots to Git directory by committing the files in staging area

## Git installation

- Linux
  sudo apt install git-all
- Mac
  brew install git
- Windows
  https://git-scm.com/download/win

## Git basic configuration

1. Git는 3개의 config화일들을 제공한다.

- /etc/gitconfig: for all users and all repos → git config —system
- ~/.gitconfig, ~/.config/git/config: for current user → git config —global
- .git/config: for current repo → git config —local

2. config화일들의 우선권순위

.git/config > /etc/gitconfig

3. User info

```jsx
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```

4. Check configuration

```jsx
$ git config --list
```

## Help

명령어에 대한 도움말을 보는 방법은 두가지가 있다.

```jsx
$ git help <verb>
$ man git-<verb>
```

Git명령 `option` 에 대한 설명

```jsx
$ git add -h
```

# Git Repository

## Git의 기초 - 저장소

Git 저장소를 만드는 방법은 2가지가 있다.

1. 처음부터

   ```jsx
   $ git init

   $ git add *.c
   $ git add LICENSE
   $ git commit -m 'initial project version'
   ```

2. Clone

   ```jsx
   $ git clone https://github.com/libgit2/libgit2

   # 등록부이름을 다른이름으로 Clone
   $ git clone https://github.com/libgit2/libgit2 mylibgit

   # Clone을 위한 Protocols
   1. https://
   2. git://
   3. user@server:path/to/repo.git (SSH)
   ```

## Git의 기초 - 수정, 저장

1. Working tree 에 두가지 상태의 화일들이 존재한다.
1. Tracked

   - Unmodified
   - Modified
   - Staged

   2. Untracked

   ![Monosnap Git - 수정하고 저장소에 저장하기 2023-04-03 17-00-16.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ccf1ab36-984f-4a05-a699-af2afc1d5ea0/Monosnap_Git_-_%E1%84%89%E1%85%AE%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%92%E1%85%A1%E1%84%80%E1%85%A9_%E1%84%8C%E1%85%A5%E1%84%8C%E1%85%A1%E1%86%BC%E1%84%89%E1%85%A9%E1%84%8B%E1%85%A6_%E1%84%8C%E1%85%A5%E1%84%8C%E1%85%A1%E1%86%BC%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5_2023-04-03_17-00-16.png)

1. 화일의 상태 확인

   ```jsx
   $ **git status**
   On branch master
   Your branch is up-to-date with 'origin/master'.
   nothing to commit, working directory clean

   $ echo 'My Project' > README
   $ git status
   On branch master
   Your branch is up-to-date with 'origin/master'.
   Untracked files:
     (use "git add <file>..." to include in what will be committed)

       README

   nothing added to commit but untracked files present (use "git add" to track)
   ```

1. Basic commands

   ```jsx
   # add to stage
   $ git add README

   # check git status in shortly
   $ git status -s
   A: add
   M: modified
   ??: new

   # 상태정보는 두가지정보를 보여준다. 왼쪽에는 Staging에서의 상태를, 오른쪽에는 Working Tree에서의 상태를 표시한다.
   ```

1. gitignore

   ```jsx
   $ cat .gitignore
   *.[oa] # 확장자가 o나 a인 화일들을 무시
   *~ # `~`로 끝나는 모든 화일들을 무시
   ```

   > `.gitignore` 화일은 처음에 만드는것이 원칙이다.

   <aside>
   ℹ️ Rules in gitignore
   - 아무것도 없는 행이나 #로 사작하는 행은 무시한다.
   - 표준 Glob패턴을 리용한다.
   - “/”로 시작하면 하위 등록부에 적용되지 않는다.
   - 등록부는 “/”를 끝에 리용하는것이로 표현한다.
   - “!”로 시작하는 패턴의 화일은 무시하지 않는다.

   </aside>

   <aside>
   ℹ️ Glob패턴
   * : 문자가 하나도 없거나 하나 이상을 의미
   [abc]:  괄호안에 있는 문자중 하나를 의미
   ? : 문자하나를 의미
   [0-9]: 괄호안에 “-”를 리용하면 그 문자사이에 있는 문자 하나를 의미

   </aside>

   > https://github.com/github/gitignore 에서 매 프로젝트에 따르는 표준 gitignore화일을 찾을수 있다.

1. git diff

   이 명령은 Working tree와 Staging Area에 있는 화일들을 비교한다.

   ```jsx
   $ git diff : Unstaged와 Committed사이 비교

   --staged: committed와 staged를 비교
   --cached: Staged상태의 화일들을 확인한다.
   ```

1. git commit

   ```jsx
   -v 편집기에 diff내용도 추가된다.
   -a Tracked상태의 화일들을 자동으로 Staging에 추가한다. (git add명령을 생략)
   ```

1. git rm
   - 이 명령으로 Tracked상태의 화일을 삭제한 후에 commit해야 한다.
   - Modified와 Staged상태를 가지는 화일들은 -f 로 강제로 삭제한다.
1. git mv

   ```jsx
   이 명령은 다애의 명령들을 실행한것과 같다.
   $ mv README.md README
   $ git rm README.md
   $ git add README
   ```

1. git log

   ```jsx
   매 commit의 diff결과를 보여준다.
   $ git log -p

   최근 2개의 결과만 보여준다.
   $ git log -p -2

   매 commit의 통계정보를 보여준다.
   $ git log --stat

   리력을 여러형식에서 보여준다.
   $ git log --pretty=oneline (short, full, fuller)

   리력을 Custom형식에서 보여준다.
   $ git log --pretty=format:"%h - %an, %ar : %s"

   지난 2주동안 만들어진 commits
   $ git log --since=2.weeks

   Other
   --after
   --until
   --before
   --author
   --committer
   --grep
   --all-match

   어떤 문자렬이 추가되거나 제거된 commit을 찾을수 있다.
   $ git log -S text
   ```

1. Undo
   - `--amend` 이전의 commit을 완전히 새로 고쳐서 commit을 변경한다. 기본사용은 마지막 commit에서 뭔가 추가하지 못했거나 변경하지 못한 경우 하나의 commit으로 처리하기 위해서이다.
   - 화일상태를 Unstage로 변경하기
     ```jsx
     $ git reset HEAD CONTRIBUTING.md
     ```
   - Modified화일을 되돌리기
     ```jsx
     $ git checkout -- CONTRIBUTING.md
     ```

## Git의 기초 - 원격저장소

```jsx
# 원격저장소 확인
$ git remote -v

# 원격저장소 추가
$ git remote add <단축이름> <url>

# 원격저장소로부터 자료가져오기
$ git fetch <remote>
!! fetch명령은 원격저장소로부터 자료를 가져오지만 Merge하지 않는다.
$ git pull

# 원격저장소에 Push하기
$ git push <remote repo name> <branch name>

# 원격저장소 살펴보기
$ git remote show origin

# 원격저장소 이름변경, 원격저장소 삭제
$ git remote rename pb paul
```

## Git의 기초 - Tags

1. 태그 조회하기

   ```jsx
   # 태그 조회하기
   $ git tag

   # 특정한 태그가지고 조회하기
   $ git tag -l "v1.8.5*"
   ```

2. 태그 붙이기

   > Git의 태그는 Lightweight와 Annotated 두 종류의 태그가 있다.

   ```jsx
   Annotated태그 붙이기
   $ git tag -a v1.4 -m "my version 1.4"

   Lightweight태그 붙이기
   $ git tag v1.4-lw

   후에 태그 붙이기
   $ git tag -a v1.2 9fceb02

   태그를 원격저장소와 공유하기
   $ git push origin v1.5
   $ git push origin --tags

   ```

## Git의 기초 - Alias

```jsx
$ git config --global alias.co checkout
$ git config --global alias.br branch
$ git config --global alias.ci commit
$ git config --global alias.st status

$ git config --global alias.unstage 'reset HEAD --'

$ git config --global alias.last 'log -1 HEAD'
```

# Git Branch

## Basic

```jsx
# create a branch
$ git branch <Branch name>

# Move to branch
$ git checkout <Branch name>
$ git checkout -b <Branch name>

# Merge branch
$ git merge hotfix

# Delete branch
$ git branch -d <Branch name>
$ git branch -D <Branch name> // Merge하지 않은 Branch를 강제로 삭제

# show branches
$ git branch // *기호가 붙어있는 가지가 현재 작업하는 가지이다.
$ git branch -v // 가지마다 마지막 commit까지 함께 보여준다.
$ git branch --merged
$ git branch --no-merged
```

- fast-forward: A가지에서 다른 B가지로 통합할때 B가지가 A가지이후의 commit을 가리키고 있으면 A가지가 B가지와 동일한 commit을 가리키도록 한다.
- 3-way: 현재 가지가 가리키는 commit이 통합할 가지의 조상이 아닌 경우이며 새로운 commit을 만든다.
- conflict
  ```jsx
  $ git status
  Unmerged상태를 보여준다.

  $ git add
  $ git commit
  ```

## Workflow

- Long-Running Branch
  ![Monosnap Git - 브랜치 워크플로 2023-04-10 17-14-16.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/20f6c125-19a3-4685-8c52-744336cba8b1/Monosnap_Git_-_%E1%84%87%E1%85%B3%E1%84%85%E1%85%A2%E1%86%AB%E1%84%8E%E1%85%B5_%E1%84%8B%E1%85%AF%E1%84%8F%E1%85%B3%E1%84%91%E1%85%B3%E1%86%AF%E1%84%85%E1%85%A9_2023-04-10_17-14-16.png)
- Topic branch

## Remote Branch

## Rebase

> Git에서 Branch들을 합치는 방법은 Merge와 Rebase가 있다.

비슷한 결과를 만드는 다른 방식으로, `C3`에서 변경된 사항을 Patch로 만들고 이를 다시 `C4`
에 적용시키는 방법이 있다. Git에서는 이런 방식을 **_Rebase_** 라고 한다. `rebase`명령으로 한 브랜치에서 변경된 사항을 다른 브랜치에 적용할 수 있다.

```jsx
$ git checkout experiment
$ git rebase master
First, rewinding head to replay your work on top of it...
Applying: added staged command
```

실제로 일어나는 일을 설명하자면 일단 두 브랜치가 나뉘기 전인 공통 커밋으로 이동하고 나서 그 커밋부터 지금 Checkout 한 브랜치가 가리키는 커밋까지 diff를 차례로 만들어 어딘가에 임시로 저장해 놓는다. Rebase 할 브랜치(역주 - experiment)가 합칠 브랜치(역주 - master)가 가리키는 커밋을 가리키게 하고 아까 저장해 놓았던 변경사항을 차례대로 적용한다. 그리고 나서 `master`브랜치를 Fast-forward 시킨다.

```jsx
$ git checkout master
$ git merge experiment
```

Merge 이든 Rebase 든 둘 다 합치는 관점에서는 서로 다를 게 없다. 하지만, Rebase가 좀 더 깨끗한 히스토리를 만든다. Rebase 한 브랜치의 Log를 살펴보면 히스토리가 선형이다. 일을 병렬로 동시에 진행해도 Rebase 하고 나면 모든 작업이 차례대로 수행된 것처럼 보인다.

```jsx
$ git rebase --onto master server client
$ git rebase master server
$ git checkout master
$ git merge server
$ git branch -d client
$ git branch -d server
```

이 명령은 `master` 브랜치부터 `server` 브랜치와 `client` 브랜치의 공통 조상까지의 커밋을 `client`
 브랜치에서 없애고 싶을 때 사용한다. `client` 브랜치에서만 변경된 패치를 만들어 `master` 브랜치에서 `client`브랜치를 기반으로 새로 만들어 적용한다.

> **이미 공개 저장소에 Push 한 커밋을 Rebase 하지 마라**

# Git Server

## Protocol

- Local
  ```jsx
  $ git clone /srv/git/project.git
  $ git clone file:///srv/git/project.git
  ```
  - Pros
    - Simple
    - Push-Pull없이 다른 사람의 코드를 가져올수 있다. `git pull /home/john/project`
  - Cons
    - 다양한 상황에서 접근할수 있도록하는것이 어렵다.
    - 저장소에 대한 보안취약성
- HTTP
  - SSH와는 달리 보안열쇠를 생성하지 않고도 HTTP는 사용자이름과 암호만으로 인증한다.
- SSH
  ```jsx
  $ git clone ssh://[user@]server/project.git

  $ git clone [user@]server:project.git
  ```
- Git

## Git Server

> Bare repo: Working Directory가 없는 저장소.

```jsx
$ git clone --bare my_project my_project.git

$ scp -r my_project.git user@git.example.com:/srv/git
```

Bare저장소를 만들고 SSH로 접근할수 있는 봉사기에 올리면 된다.

## Generating SSH public key

```jsx
# confirm if already key
$ cd ~/.ssh
$ ls

# generate key
$ ssh-keygen -o
```

## Setup Server

- Create `git` user and `.ssh` directory for that user.
  ```jsx
  $ sudo adduser git
  $ su git
  $ cd
  $ mkdir .ssh && chmod 700 .ssh
  $ touch .ssh/authorized_keys && chmod 600 .ssh/authorized_keys
  ```
- pub key to authroized_keys
  ```jsx
  $ cat /tmp/id_rsa.john.pub >> ~/.ssh/authorized_keys
  ```
- setup an empty repository
  ```jsx
  $ cd /srv/git
  $ mkdir project.git
  $ cd project.git
  $ git init --bare

  # on John's computer
  $ cd myproject
  $ git init
  $ git add .
  $ git commit -m 'Initial commit'
  $ git remote add origin git@gitserver:/srv/git/project.git
  $ git push origin master
  ```
- Git Daemon
  ```jsx
  # Run Git Daemon
  $ git daemon --reuseaddr --base-path=/srv/git/ /srv/git/

  # Register Git Daemon
  /etc/systemd/system/git-daemon.service

  [Unit]
  Description=Start Git Daemon

  [Service]
  ExecStart=/usr/bin/git daemon --reuseaddr --base-path=/srv/git/ /srv/git/

  Restart=always
  RestartSec=500ms

  StandardOutput=syslog
  StandardError=syslog
  SyslogIdentifier=git-daemon

  User=git
  Group=git

  [Install]
  WantedBy=multi-user.target

  # Enable, start, stop git daemon
  systemctl enable git-daemon
  systemctl start git-daemon
  systemctl stop git-daemon

  # Serve the project without authentication
  $ cd /path/to/project.git
  $ touch git-daemon-export-ok
  ```
- HTTP Serve
  ```jsx
  # CGI server with Apache
  $ sudo apt-get install apache2 apache2-utils
  $ a2enmod cgi alias env

  # Set Unix user group /srv/git directories to www-data
  $ chgrp -R www-data /srv/git

  # Apache configuration
  SetEnv GIT_PROJECT_ROOT /srv/git
  SetEnv GIT_HTTP_EXPORT_ALL
  ScriptAlias /git/ /usr/lib/git-core/git-http-backend/

  # Apache to allow requests
  <Files "git-http-backend">
      AuthType Basic
      AuthName "Git Access"
      AuthUserFile /srv/git/.htpasswd
      Require expr !(%{QUERY_STRING} -strmatch '*service=git-receive-pack*' || %{REQUEST_URI} =~ m#/git-receive-pack$#)
      Require valid-user
  </Files>

  # add user to `.htpasswd`
  $ htpasswd -c /srv/git/.htpasswd schacon

  ```

## GitWeb & GitLab

1. GitWeb

   ```jsx
   # GitWeb Run
   $ git instaweb --httpd=webrick

   # GitWeb stop
   $ git instaweb --httpd=webrick --stop

   # Install GitWeb
   $ git clone https://git.kernel.org/pub/scm/git/git.git
   $ cd git/
   $ make GITWEB_PROJECTROOT="/srv/git" prefix=/usr gitweb
       SUBDIR gitweb
       SUBDIR ../
   make[2]: `GIT-VERSION-FILE' is up to date.
       GEN gitweb.cgi
       GEN static/gitweb.js
   $ sudo cp -Rf gitweb /var/www/

   # Apache Configuration
   <VirtualHost *:80>
       ServerName gitserver
       DocumentRoot /var/www/gitweb
       <Directory /var/www/gitweb>
           Options +ExecCGI +FollowSymLinks +SymLinksIfOwnerMatch
           AllowOverride All
           order allow,deny
           Allow from all
           AddHandler cgi-script cgi
           DirectoryIndex gitweb.cgi
       </Directory>
   </VirtualHost>
   ```

2. GitLab

   > default username : admin@local.host
   > default password: 5iveL!fe

# Advanced Git

## Merge

```jsx
# Merge하기전으로 되돌리기
$ git merge --abort

# 공백을 무시하고  Merge하기
$ git merge -Xignore-space-change whitespace

# 현재 무엇이 변화되였는지 알기 위해서.
$ git diff --ours
$ git diff --theirs
$ git diff --base

# 필요없는 화일들  지우기
$ git clean -f

# HEAD 옳기기
git reset --hard HEAD~

# Commit되돌리기
$ git revert SHA-1
```

## Bundle

```jsx
Git에는 “Bundle” 이란 것이 있다. 자료를 한 화일로 묶는 방법이다. 이 방법은 다양한 경우 유용하게 사용할수 있다. 례를 들어 망상태가 좋지 못한 경우 변경사항을 동료에게 보낼때, 출장을 나갔는데 보안상의 리유로 극부망에 접속하지 못할때, 통신장비가 고장났을때, 갑자기 중앙봉사기에 접근하지 못할때, 누군가에게 수정사항을 메일로 보내야 하는데 40개 씩이나 되는 커밋을 format-patch로 보내고 싶지 않을때 쓸수 있다.

# packing
$ git bundle create repo.bundle HEAD master

# unpacking
$ git clone repo.bundle repo

# only packing for specific commits
$ git bundle create commits.bundle master ^9a466c5

# verify the bundle file
$ git bundle verify ../commits.bundle
```

# Customizing Git

## Config

- commit.template
  commit할 때 Git가 보여주는 commit통보문은 이 선택항목에 설정한 template화일이다. 이것은 commit통보문을 작성할때 일정한 형식을 유지할수 있게 한다.
  ```jsx
  $ git config --global commit.template ~/.gitmessage.txt

  # ~/.gitmessage.txt
  Subject line (try to keep under 50 characters)

  Multi-line description of commit,
  feel free to be detailed.

  [Ticket: X]
  ```
- core.excludesfile
  한 저장소안에서뿐 아니라 어디에서라도 Git에 포함하지 않을 화일을 설정할 수 있다. 례를 들어 Mac을 쓰는 사람이라면 `.DS_Store` 화일을 자주 보았을것이다. Emacs나 Vim를 쓰다 보면 이름 끝에 `~`, `.swp` 붙여둔 림시화일도 있다.
  ```jsx
  # ~/.gitignore_global
  *~
  .*.swp
  .DS_Store

  $ git config --global core.excludesfile ~/.gitignore_global
  ```
