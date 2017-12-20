---
id: 56
title: Learning git
date: 2015-12-27T01:25:00+00:00
author: liu1084
layout: post
guid: http://www.83096146.com/blog/?p=56
permalink: /?p=56
categories:
  - git
---
  1. 什么是git？
  2. 为什么使用git？
  3. git跟svn有什么不同？
  4. 为什么非要从svn转换到git？
  5. 怎么使用git？
  6. git有没有不好的地方？
  7. 如果遇到问题，我怎么获得帮助？

<!--more-->

版本控制系统的历史

你可能有过这样的经历：

  * 在 debug 的时候这里加一句，那里减一句，顺便改改参数，不一会你的程序就从一个 bug 增加到了无数个 bug 。最重要的是，你完全想不起来自己到底改了几个地方，原来的程序到底长什么样子了。经历过几次这样的痛苦，你学乖了，下次 debug 之前先把原文件备份一下——改成 program.c.bak 什么的，然后放开了胆子改。有时候修改的次数多了，就会出现 program\_V1.c.bak， program\_V2.c.bak …… 又有时候需要同时修改多个文件。而需要倒回到之前的版本的时候，又完全想不起来这些 V1, V2 到底改了哪些地方。坑爹呐！难道要手工查不成？难道还要给每个 version 写个描述文件？

想到这里，程序员们应该都中枪了。

  * 如果你不是程序员，那你应该编辑过word文档吧？写论文的时候，你可能这里改一下，那里改一下，改来改去发现还不如原来的初版&#8230;怎么办？Ctrl + Z能救你几次，那万一是关机以后，怎么Ctrl + Z?

想到这里，我们都中枪了。

  * 那有没有办法解决这个问题？当然有了，这又不是一个人中枪的事情。。。

  * 1972年，贝尔实验室的程序员快被这个问题折磨疯了。。。于是有人写出史上第一个版本控制系统（VCS – Version Control System），名字叫SCCS，但是这个软件有个问题就是它是从最初的版本依次做快照开始，然后一直比对你想要哪个版本，当文件的修改逐渐增多后，变得效率就越来越慢，于是。。。
  * 有个大学教授Water，他发现SCCS有问题，正常的修改都是从最近的修改作为源文件，对历史的快照，用的不是太多，就写了另外一个，名字叫RCS，它的效率提高了，但是也有问题，只能监控单个文件，程序员们受不了，于是。。。
  * 终于有一天，CVS横空出世，他的诞生扭转了整个局面。不但效率提高n倍，而且还提出了仓库（repository）的概念，是CS结构的，把代码仓库放在Server端，由客户端向服务器端提出修改，还很好的支持了多用户多文件并行操作。但是CVS也有个问题，它监控的是文件，而不是目录，如果在项目里面创建目录，在里面添加文件，就无法被监控了，于是。。。
  * SVN诞生了，它几乎吸收了CVS的所有优点，而且还添加了更多的功能，直到今天我们依然在用。。。

Git诞生之前，免费的CVS发挥了巨大的作用，同时并存的还有bitkeeper这样的商用版本控制软件。

说到Git，不得不说Linux系统。

那个年代，Linus和全世界很多热心的程序员都在为Linux编写代码，那么Linux的代码是如何管理的？事实上，2002年之前，世界各地的参与者都是把源代码通过diff方式用邮件发给linus，然后手工合并代码。。。那有人会说，前面提到的这些RCS为啥不用呢？

  * 首先是“大神”对这些RCS的不屑；
  * 其次是Linux社区很活跃，参与的人太多，代码提交频繁以至于这些工具都无法胜任；
  * 不过，到了2002年，Linux系统已经发展了十年了，代码库之大让Linus很难继续通过手工方式管理了，社区的弟兄们也对这种方式表达了强烈不满，于是Linus选择了一个商业的版本控制系统BitKeeper，BitKeeper的东家BitMover公司出于人道主义精神，授权Linux社区免费使用这个版本控制系统。
  * 安定团结的大好局面在2005年就被打破了，原因是Linux社区牛人聚集，不免沾染了一些梁山好汉的江湖习气。开发Samba的Andrew试图破解BitKeeper的协议（这么干的其实也不只他一个），被BitMover公司发现了（监控工作做得不错！），于是BitMover公司怒了，要收回Linux社区的免费使用权。
  * Linus可以向BitMover公司道个歉，保证以后严格管教弟兄们，嗯，这是不可能的。实际情况是这样的：
  
    Linus花了两周时间自己用C写了一个分布式版本控制系统，这就是Git！一个月之内，Linux系统的源码已经由Git管理了！牛是怎么定义的呢？大家可以体会一下。
  * Git迅速成为最流行的分布式版本控制系统，尤其是2008年，GitHub网站上线了，它为开源项目免费提供Git存储，无数开源项目开始迁移至GitHub，包括jQuery，PHP，Ruby等等。
  * 历史就是这么偶然，如果不是当年BitMover公司威胁Linux社区，可能现在我们就没有免费而超级好用的Git了。

一句话回答

  1. 什么是git？ –  Git是一个免费且开源、支持分布式的版本控制系统，可以快速有效的管理大大小小的项目。
  2. 为什么使用git？ – Git的好处多、速度快，使用简单方便，为了跟国际接轨（因为我们是global的嘛。。。）
  3. git跟svn有什么不同？ –  (分布式、效率高、简单方便、强大的分支和合并、完整性、无需网络也可以提交代码)
  4. 为什么非要从svn转换到git？ – 请看问题2、问题3
  5. 怎么使用git？ – 下面会讲到。。。
  6. git有没有不好的地方？ –  应该有吧，添加文件夹貌似不行
  7. 如果遇到问题，我怎么获得帮助？ – （google->stackoverflow – 懒人、git  help <verb> – 勤快且英语比较好的人）
  8. 还有什么问题？ google 或者可以阅读它们的使用帮助（如果你的E文还可以），方法有三： <pre class="lang:sh decode:true ">$ git help &lt;verb&gt;
$ git &lt;verb&gt; --help
$ man git-&lt;verb&gt;</pre>
    
    比如，要学习 config 命令可以怎么用，运行：</li> </ol> 
    
    <pre class="lang:sh decode:true">$ git help config</pre>
    
    安装配置
    
      * Download
    
    http://git-scm.com/downloads 目前最稳定版本是2.6.4
    
      * Installation
  
        <table class="confluenceTable">
          <tr>
            <th class="confluenceTh">
              OS
            </th>
            
            <th class="confluenceTh" colspan="2">
              How to install
            </th>
          </tr>
          
          <tr>
            <td class="confluenceTd">
              Windows
            </td>
            
            <td class="confluenceTd" colspan="2">
              Git-1.9.5.exe(<a href="#">download</a>)</p> 
              
              <p>
                <a class="external-link" href="http://msysgit.github.io/" rel="nofollow">http://msysgit.github.io/</a></td> </tr> 
                
                <tr>
                  <td class="confluenceTd" colspan="1">
                    Linux
                  </td>
                  
                  <td class="confluenceTd" colspan="2">
                    <div class="code panel pdl">
                      <div class="codeContent panelContent pdl">
                        <div id="highlighter_607654" class="syntaxhighlighter bash">
                          <pre class="lang:sh decode:true">$ yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel
$ apt-get install libcurl4-gnutls-dev libexpat1-dev gettext libz-dev libssl-dev
$ wget https://www.kernel.org/pub/software/scm/git/git-2.4.0.tar.gz 
$ tar -zvxf git-2.4.0.tar.gz
$ cd git-2.4.0
$ make prefix=/usr/local all
$ sudo make prefix=/usr/local install 
$ sudo ln -s /usr/local/git-2.4.0/bin/git /usr/bin/git
$ git --version
git version 2.4.0</pre>
                        </div>
                      </div>
                    </div>
                  </td>
                </tr>
                
                <tr>
                  <td class="confluenceTd" colspan="1">
                    Mac
                  </td>
                  
                  <td class="confluenceTd" colspan="2">
                    <div class="code panel pdl">
                      <div class="codeContent panelContent pdl">
                        <div id="highlighter_951215" class="syntaxhighlighter bash">
                          <pre class="lang:sh decode:true">sudo port install git-core +svn +doc +bash_completion +gitweb</pre>
                        </div>
                      </div>
                    </div>
                  </td>
                </tr></tbody> </table> </li> </ul> 
                
                <p>
                  Git-GUI（option）
                </p>
                
                <p>
                  TortoiseGit(<a class="external-link" href="https://download.tortoisegit.org/tgit/" rel="nofollow">donwload</a>)
                </p>
                
                <p>
                  Eclipse <a class="external-link" href="http://eclipse.org/egit/" rel="nofollow">egit</a>
                </p>
                
                <ul>
                  <li>
                    检查git版本
                  </li>
                </ul>
                
                <pre class="lang:sh decode:true">$ git --version
git version 2.6.4</pre>
                
                <ul>
                  <li>
                    配置
                  </li>
                </ul>
                
                <p>
                  查看已有配置项 &#8211; display git config key & value
                </p>
                
                <pre class="lang:sh decode:true">$ git config -l
core.symlinks=false
core.autocrlf=true
color.diff=auto
color.status=auto
color.branch=auto
color.interactive=true
pack.packsizelimit=2g
help.format=html
http.sslcainfo=/bin/curl-ca-bundle.crt
sendemail.smtpserver=/bin/msmtp.exe
diff.astextplain.textconv=astextplain
rebase.autosquash=true</pre>
                
                <p>
                  查看某个配置项 &#8211;  display a config item
                </p>
                
                <pre class="lang:sh decode:true">$ git config merge.tool</pre>
                
                <p>
                  添加新的配置项 &#8211; add a new config item
                </p>
                
                <pre class="lang:sh decode:true">$ git config --global user.name &lt;name&gt;
$ git config --global user.email &lt;email&gt;
$ git config --global http.sslVerify false (option)</pre>
                
                <p>
                  <strong><em><a href="http://blog.83096146.com/?p=53">跟github一起工作 &#8212; work with github</a></em></strong>
                </p>
                
                <p>
                  git base workflow
                </p>
                
                <ul>
                  <li>
                    建立一个新的资源库 &#8211; create a new repository
                  </li>
                </ul>
                
                <pre class="lang:sh decode:true">$ cd my-project
$ git init</pre>
                
                <ul>
                  <li>
                    通过git从服务器下载一个资源 &#8211; clone a repository from remote
                  </li>
                </ul>
                
                <pre class="lang:sh decode:true">$ git clone
git clone ~/existing/repo ~/new/repo
git clone git://host.org/project.git
git clone ssh://you@host.org/proj.git

实例：
$ git clone https://github.com/growthy/frontend.git
Cloning into 'frontend'...
Username for 'https://github.com': root
Password for 'https://root@github.com':
remote: Counting objects: 253, done.
remote: Compressing objects: 100% (173/173), done.
Receiving objects:  66% (1), reused 124 (delta 27) eceiving objects:  65% (165/253)
Receiving objects: 100% (253/253), 746.95 KiB | 0 bytes/s, done.
Resolving deltas: 100% (73/73), done.
Checking connectivity... done.
</pre>
                
                <ul>
                  <li>
                    查看当前的工作分支和所有分支 &#8211; display current branch and all branch
                  </li>
                </ul>
                
                <pre class="lang:sh decode:true">$ git branch
* master
</pre>
                
                <ul>
                  <li>
                    建立一个新的分支并在新分支上开发新的功能 &#8211; create a new branch & switch to it
                  </li>
                </ul>
                
                <pre class="lang:sh decode:true ">$ git checkout -b worldmap
Switched to a new branch 'worldmap'
$ git status
On branch worldmap
nothing to commit, working directory clean
$ git branch
  develop
  master
* worldmap
$ vim package.json
$ git add package.json
$ git commit -m "modify repository of package.json"
[worldmap bcd196f] modify repository of package.json
 1 file changed, 4 insertions(+), 1 deletion(-)
</pre>
                
                <ul>
                  <li>
                    合并新分支到开发的主分支 &#8211; merge new branch to main branch
                  </li>
                </ul>
                
                <pre class="lang:sh decode:true ">$ git checkout develop
Switched to branch 'develop'
$ git merge worldmap
Updating 73b5cfd..bcd196f
Fast-forward
 package.json | 5 ++++-
 1 file changed, 4 insertions(+), 1 deletion(-)
</pre>
                
                <ul>
                  <li>
                    推送内容到服务器 &#8211; Update remote refs along with associated objects
                  </li>
                </ul>
                
                <pre class="lang:sh decode:true ">$ git push origin develop
Username for 'https://github.com': root
Password for 'https://root@github.com':
Counting objects: 5, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 388 bytes | 0 bytes/s, done.
Total 3 (delta 2), reused 0 (delta 0)
To https://github.com/growthy/frontend.git
   73b5cfd..bcd196f  develop -&gt; develop
</pre>
                
                <ul>
                  <li>
                    删除分支 &#8211; remove a branch
                  </li>
                </ul>
                
                <pre class="lang:sh decode:true">$ git branch -d worldmap
Deleted branch worldmap (was bcd196f).

$ git branch
* develop
  master
</pre>
                
                <ul>
                  <li>
                    添加新文件到工作区
                  </li>
                </ul>
                
                <pre class="lang:sh decode:true ">$ git branch
* develop
  master

$ git checkout -b test
Switched to a new branch 'test'

$ touch
.git/         .gitignore    LICENSE       README.md     generators/   package.json

$ touch test.txt
$ echo "test" &gt; test.txt
$ git status
On branch test
Untracked files:
  (use "git add ..." to include in what will be committed)
        test.txt
nothing added to commit but untracked files present (use "git add" to track)

$ git status
On branch test
Changes to be committed:
  (use "git reset HEAD ..." to unstage)
        new file:   test.txt


$ git add test.txt
$ git commit -m "add test.txt"
[test 9cbfff7] add test.txt
 1 file changed, 1 insertion(+)
 create mode 100644 test.txt

$ git status
On branch test
nothing to commit, working directory clean
</pre>
                
                <ul>
                  <li>
                    从工作区删除或者移动文件
                  </li>
                </ul>
                
                <pre class="lang:sh decode:true ">git log
git reset sha-1
git checkout -- filname

</pre>
                
                <ul>
                  <li>
                    删除没用合并的分支
                  </li>
                </ul>
                
                <pre class="lang:sh decode:true ">$ git checkout develop
Switched to branch 'develop'

$ git branch -d test
error: The branch 'test' is not fully merged.
If you are sure you want to delete it, run 'git branch -D test'.

$ git branch -D test
Deleted branch test (was fc20997).

$ git log
commit bcd196f501738da34c1746ec0f1f6d18b9fd778b
Author: liujun &lt;liu.jun@nhn.com&gt;
Date:   Thu Mar 19 11:30:33 2015 +0800
    modify repository of package.json

</pre>
                
                <ul>
                  <li>
                    修改新建的文件
                  </li>
                </ul>
                
                <pre class="lang:sh decode:true ">//准备修改license的内容
$ vim LICENSE
$ git status
On branch license
Changes not staged for commit:
  (use "git add ..." to update what will be committed)
  (use "git checkout -- ..." to discard changes in working directory)
        modified:   LICENSE
no changes added to commit (use "git add" and/or "git commit -a")
//放弃修改
$ git checkout -- LICENSE

//确认修改
$ git add LICENSE

</pre>
                
                <ul>
                  <li>
                    提交到本地
                  </li>
                </ul>
                
                <pre class="lang:sh decode:true ">$ git add LICENSE
$ git status
On branch license
Changes to be committed:
  (use "git reset HEAD ..." to unstage)
        modified:   LICENSE

</pre>
                
                <ul>
                  <li>
                    废弃本地修改
                  </li>
                </ul>
                
                <pre class="lang:sh decode:true ">git checkout --

</pre>
                
                <ul>
                  <li>
                    将添加到索引区的文件还原为未添加
                  </li>
                </ul>
                
                <pre class="lang:sh decode:true ">$ git reset HEAD LICENSE
Unstaged changes after reset:
M       LICENSE

</pre>
                
                <ul>
                  <li>
                    返回到历史
                  </li>
                </ul>
                
                <pre class="lang:sh decode:true ">$ git commit -m "update LICENSE"
[license 2881fbc] update LICENSE
 1 file changed, 8 insertions(+)

$ git status
On branch license
nothing to commit, working directory clean

$ git log
commit 2881fbc404483487d04093cc639a0d5ddc60585e
Author: liujun &lt;liu.jun@nhn.com&gt;
Date:   Thu Mar 19 15:20:21 2015 +0800
    update LICENSE
$ git revert 2881fbc404483487d04093cc639a0d5ddc60585e
[license b28b13b] Revert "update LICENSE"
 1 file changed, 8 deletions(-)
CN40309-D-1@CN40309-D-1 /D/work/cli/generator-gdc-web-
$ git status
On branch license
nothing to commit, working directory clean

$ cat LICENSE

</pre>
                
                <ul>
                  <li>
                    推送已经提交到本地的修改到服务器
                  </li>
                </ul>
                
                <pre class="lang:sh decode:true ">//推送你的改动到远端的任意一个分支上去
$ git push orgin

//如果你事先没有clone仓库，但是想将你的仓库连接到某个远端仓库，可以使用
$ git remote add origin
//然后再进行推送

</pre>
                
                <ul>
                  <li>
                    查看文件的修改
                  </li>
                </ul>
                
                <pre class="lang:sh decode:true ">git diff [filename]

</pre>
                
                <ul>
                  <li>
                    从服务器拖拽文件到本地，并且尝试合并
                  </li>
                </ul>
                
                <pre class="lang:sh decode:true ">git pull

</pre>
                
                <ul>
                  <li>
                    建立新的tag
                  </li>
                </ul>
                
                <pre class="lang:sh decode:true ">//在软件发布或者打版本的时候创建标签，是推荐的做法
//创建一个1.0.0的标签
$ git checkout my_feature

$ git log
commit feaa0131231818272229f0074527e57470b0ce5d
Author: cn40309 &lt;liu.jun@nhn.com&gt;
Date:   Thu Jan 29 15:01:29 2015 +0800
        new file:   pom.xml
commit 490b91494502d590053418230cec6b06358fbf2a
Author: cn40309 &lt;liu.jun@nhn.com&gt;
Date:   Thu Jan 29 14:58:55 2015 +0800
        new file:   MainController.java

$ git tag 1.0.0 feaa01312318182
</pre>
                
                <ul>
                  <li>
                    删除tag
                  </li>
                </ul>
                
                <pre class="lang:sh decode:true ">git tag -d v1.0

</pre>
                
                <p>
                  <em><strong><a href="https://try.github.io/levels/1/challenges/1" target="_blank">I want to try git online</a></strong></em>
                </p>