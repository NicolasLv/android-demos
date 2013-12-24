# ��Ŀ�е�Git��������


һЩ�淶
--------------------------
1. ��Ŀ���������̶���֧master��development
2. ��������ֻ��¡development��֧, ֻ����Ҫrelase����hotfixʱ��Ż��ڱ��ؿ�¡master���������кϲ�
3. ���п���ʱ����ӵ�feature�������޸���bug��ֻ��ֱ�Ӻϲ���development��֧��


ʵ�ʿ�������
--------------------------
###  1. ��¡Զ�˵�development��֧

```bash
git clone -b development <remote-repository-name>
```

###  2. �����µķ�֧
��ʼʵ��һ��feature���߽��һ��bug֮ǰ�������л���development��֧��

```bash
git checkout development
```

����feature����bug�ķ�֧,�����л����÷�֧

```bash
git checkout -b <feature-branch-name> development
```

###  3. ��ɿ����Ĺ���
�޸�һЩ�ļ�������޸ĵ��ļ����ݴ���(staging area)

```bash
git add .
```

���޸ĺ���ļ��ύ�����صİ汾����

```bash
git commit -am 'Add a new feature'
```

### 4. �ύ��Ĵ��뵽����汾����
�ύ֮ǰ��֤�㱾�ص�development��֧�Ĵ��������µ�

```bash
git checkout development
git pull origin development
```

������branch����ɵĴ����޸ĺϲ���development��֧��

```bash
git merge <feature-branch-name>
```

**or**

```bash
git rebase -i <feature-branch-name>
```

�ύ���뵽����汾��

```bash
git push
```

*ɾ�����ش����ķ�֧����ѡ��

```bash
git branch -d <feature-branch-name>
```


��Windows��ʹ��Gitflow�淶����
--------------------------
### 1. ��Gitflow��¡������

```bash
git clone -recursive git://github.com/nvie/gitflow.git
```

### 2. ������msysgit����Bin�ļ�
[util-linux-ng-2.14.1-bin](http://sourceforge.net/projects/gnuwin32/files/util-linux/2.14.1/util-linux-ng-2.14.1-bin.zip/download)

[util-linux-ng-2.14.1-dep](http://sourceforge.net/projects/gnuwin32/files/util-linux/2.14.1/util-linux-ng-2.14.1-dep.zip/download)
### 3. ��Bin�ļ�������msysgit��binĿ¼��
������ɺ�ֱ�����ѹ������ѹ�ļ���binĿ¼�е�getopt.exe��libintl3.dll��libiconv2.dll�ļ�������msysgit��װĿ¼�µ�binĿ¼��
### 4. ��װGitflow����
��cmd�����У������Ѿ���¡�õ�gitflow contribĿ¼��ִ������

```bash
D:\gitflow contrib>msysgit-install.cmd "C:\Program Files\Git".
```

### 5. ��ʼ��console��ʹ��Gitflow

```bash
usage: git flow <subcommand>

Available subcommands are:
   init      Initialize a new git repo with support for the branching model.
   feature   Manage your feature branches.
   release   Manage your release branches.
   hotfix    Manage your hotfix branches.
   support   Manage your support branches.
   version   Shows version information.

Try 'git flow <subcommand> help' for details.
```

��ϸ��Gitflowʹ�÷����ο�[Git Flow Cheatsheet](http://danielkummer.github.io/git-flow-cheatsheet/index.zh_CN.html)


ʹ��Gitflow֮��Ŀ�������
--------------------------
### 1. Ϊ���ش�������Git flow����

```bash
git flow init
```

ʹ��Ĭ��ֵ���г�ʼ���趨
### 2. ��ʼ����������/�޸�bug

```bash
git flow feature start <feature-branch-name>
```

###  3. ��ɿ����Ĺ���
�޸�һЩ�ļ�������޸ĵ��ļ����ݴ���(staging area)

```bash
git add .
```

���޸ĺ���ļ��ύ�����صİ汾����

```bash
git commit -am 'Add a new feature'
```

###  4. ���������/�޸�bug

```bash
git flow feature finish <feature-branch-name>
```

###  5. ͬ������������

```bash
git flow feature publish <feature-branch-name>
```

[��ϸ˵���ο�](http://danielkummer.github.io/git-flow-cheatsheet/index.zh_CN.html/#features)


׼��release
--------------------------
### 1. ����release��֧

```bash
git checkout -b <release-branch-name> development
```

### 2. ���relase����ع���

```bash
git add .
git commit -am 'Finish release related work'
```

### 3. ��relase��֧�ϲ���master��development��֧������ͬ��������汾��

```bash
git checkout master
git merge <release-branch-name>
git push
git checkout development
git merge <release-branch-name>
git push
git branch -d <release-branch-name>
```

### 4. ������֧�����tag������ͬ�������������

```bash
git tag -a <version-number> -m 'Create 0.1 version release' master
git push --tags
```

[ʹ��Gitflow׼��release](http://danielkummer.github.io/git-flow-cheatsheet/index.zh_CN.html/#release)


����hotfix
--------------------------
### 1. ��master��֧�ϴ���һ��hotfix���·�֧

```bash
git checkout -b <hotifx-branch-name> master
```

### 2. �޸�����

```bash
git add .
git commit -am 'Fix the crash bug'
```

### 3. ��relase��֧�ϲ���master��development��֧������ͬ��������汾��

```bash
git checkout master
git merge <hotifx-branch-name>
git push
git checkout development
git merge <hotifx-branch-name>
git push
git branch -d <hotifx-branch-name>
```

[ʹ��Gitflow����hotfix](http://danielkummer.github.io/git-flow-cheatsheet/index.zh_CN.html#hotfixes)


�ο�
--------------------------
[Gitflow������Ӣ�İ�](https://www.atlassian.com/git/workflows#!workflow-gitflow)

[���ٿ�ʼ](http://rogerdudler.github.io/git-guide/)

[���ʹ��Gitflow���](http://danielkummer.github.io/git-flow-cheatsheet/index.zh_CN.html)

[Git�ĵ�](http://git-scm.com/book/en)

[�ҵ�Github������](https://github.com/vincenthou/vincenthou.github.io/issues/1)