++++++
GitHub
++++++


===========================
CentOS 7에 GitHub 환경 구성
===========================

Git을 설치하고 환경을 설정 한다. 자신이 사용하는 이름(user.name)과 이메일(user.email)을 설정하여 사용 한다.

::

 yum -y install git
 
 git config --global user.name "Mountain Lover"
 git config --global user.email consult@jopenbusiness.com
 git config --global push.default simple
 
 git config --global --list
 git config --list
 
 #--- 공인키와 사설키를 생성 한다.
 #---     ~/.ssh/id_rsa (사설키), ~/.ssh/id_rsa.pub (공인키) 
 ssh-keygen -t rsa -b 4096
 chmod 600 ~/.ssh/id_rsa
 chmod 600 ~/.ssh/id_rsa.pub


생성한 공인키를 GitHub에서 "Settings > SSH and GPG keys"에 등록 합니다.


==============
Clone하여 작업
==============

https://github.com/openstack-kr/contributhon-2018-team1 사이트에서 "Fork" 버튼을 선택하여 자신의 GitHub 계정으로 contributhon-2018-team1를 Fork 한다.

여기의 pnuskgh 대신에 자신의 GitHub 아이디를 사용 한다.

::

 mkdir -p /work/devstack
 cd /work/devstack
 git clone git@github.com:pnuskgh/contributhon-2018-team1.git
 cd contributhon-2018-team1
 vim .gitignore
     /.gitignore
     *.swp
 
 #--- 파일 추가
 vim 새파일_이름
 cd /work/devstack/contributhon-2018-team1
 git add *
 git commit
 git push

 #--- 파일 이름 변경
 git mv 원본_파일 새이름_파일
 cd /work/devstack/contributhon-2018-team1
 git add *
 git commit
 git push

 #--- 파일 삭제
 git rm 파일_이름
 cd /work/devstack/contributhon-2018-team1
 git add *
 git commit
 git push


=====================
원격 저장소 추가 관리
=====================

원본 저장소(https://github.com/openstack-kr/contributhon-2018-team1)를 Fork하여 개인 저장소(https://github.com/pnuskgh/contributhon-2018-team1)를 만들어서 관리를 하면 몇가지 문제가 발생 한다.

원본 저장소에 변경 사항이 발생하면 그 변경 사항이 개인 저장소에 반영이 되지 않는 문제 이다. 이는 원격 저장소를 추가하여 관리할 수 있다.
일반적으로 원격저장소 이름은 upstream을 사용하나 여기서는 OpenStack을 사용하겠다.

::
  
 cd /work/devstack/contributhon-2018-team1
 git remote add OpenStack git@github.com:openstack-kr/contributhon-2018-team1.git
 git remote -v                                              #--- 저의 경우 아래와 같이 표시 됩니다.
     OpenStack       git@github.com:openstack-kr/contributhon-2018-team1.git (fetch)
     OpenStack       git@github.com:openstack-kr/contributhon-2018-team1.git (push)
     origin  git@github.com:pnuskgh/contributhon-2018-team1.git (fetch)
     origin  git@github.com:pnuskgh/contributhon-2018-team1.git (push)
  
 git pull OpenStack master                                  #--- OpenStack 저장소의 master branch를 가져 온다.
  
 git add *
 git commit
 git push origin master                                     #--- origin 저장소의 master에 변경 사항을 반영 한다.


=============================
새로운 브랜치를 만들어서 배포
=============================

:: 
 
 git checkout master
 git branch -b obcon201809001                               #--- Local에 obcon201809001 branch를 생성 한다.
 #--- 여기서 수정 작업을 한다.
 git add *
 git commit
 git push --set-upstream origin obcon201809001              #--- Local에만 있는 branch를 push할 때 --set-upstream을 사용 한다.
 #--- Git Hub 사이트에서 Pull Request를 생성할 수 있다.


=====================
충돌 발생시 처리 방법
=====================

여러 리포지토리를 사용하거나 하나의 파일을 여러 사람이 수정하는 경우 충돌이 발생 한다. 이 경우 충돌이
 발생한 파일을 수작업으로 수정하여야 한다.

아래의 코드는 충돌 사례와 처리 방법 이다.

::
 
 git pull OpenStack master                                 #--- Pull 명령시 3개의 파일에서 충돌 발생
     remote: Counting objects: 40, done.
     remote: Compressing objects: 100% (20/20), done.
     remote: Total 40 (delta 15), reused 40 (delta 15), pack-reused 0
     Unpacking objects: 100% (40/40), done.
     From github.com:openstack-kr/contributhon-2018-team1
      * branch            master     -> FETCH_HEAD
     Auto-merging Vagrant/Vagrant.rst
     CONFLICT (add/add): Merge conflict in Vagrant/Vagrant.rst
     Auto-merging GitHub/GitHub.rst
     CONFLICT (add/add): Merge conflict in GitHub/GitHub.rst
     Auto-merging DevStack/install.rst
     CONFLICT (add/add): Merge conflict in DevStack/install.rst
     Automatic merge failed; fix conflicts and then commit the result.
 
 vi Vagrant/Vagrant.rst GitHub/GitHub.rst DevStack/install.rst   #--- 충돌이 발생한 파일을 수작업으로 최종본으로 수정
 
 cd /work/devstack/contributhon-2018-team1
 git add *
 git commit
 git push                                                   #--- 최종 수정본을 리포지토리에 반영

