# .git 目录解析

首先我们可以进入项目的目录下，然后通过`$ cd .git`进入.git 目录，以下就是我们查看.git 目录下的文件和文件夹内容

```
phoebe@phoebedeMacBook-Pro .git % ls -l
total 80
-rw-r--r-- 1 phoebe staff 5 5 5 19:26 COMMIT_EDITMSG
-rw-r--r-- 1 phoebe staff 23 5 5 18:53 HEAD
-rw-r--r-- 1 phoebe staff 41 5 5 19:26 ORIG_HEAD
-rw-r--r-- 1 phoebe staff 41 5 5 18:53 REBASE_HEAD
-rw-r--r-- 1 phoebe staff 359 5 5 19:21 config
-rw-r--r-- 1 phoebe staff 73 4 29 10:35 description
drwxr-xr-x 15 phoebe staff 480 4 29 10:35 hooks
-rw-r--r-- 1 phoebe staff 10738 5 5 19:26 index
drwxr-xr-x 3 phoebe staff 96 4 29 10:35 info
drwxr-xr-x 4 phoebe staff 128 4 29 10:35 logs
drwxr-xr-x 63 phoebe staff 2016 5 5 19:26 objects
-rw-r--r-- 1 phoebe staff 250 4 29 10:35 packed-refs
drwxr-xr-x 5 phoebe staff 160 4 29 10:35 refs
```

#### HEAD

文件 HEAD 保存了当前工作分支的引用，当切换分支后，HEAD 的内容也会相应的发生变化。

可通过 `$ cat HEAD` 查看当前分支的引用，可通过 `$ git checkout xxx`后再查看 HEAD 内容

```
phoebe@phoebedeMacBook-Pro .git % cat HEAD
ref: refs/heads/master
phoebe@phoebedeMacBook-Pro .git % cd ../
phoebe@phoebedeMacBook-Pro knowledge % git checkout newbranchName
Switched to branch 'newbranchName'
phoebe@phoebedeMacBook-Pro .git % cat HEAD
ref: refs/heads/newbranchName
```

#### config

文件 config 保存了当前仓库的本地配置信息，使用--local 设置或者查看都与 config 息息相关。

config 查看命令`$ cat config`，通过`$ git config 参数`等命令变更配置信息后，都会在此文件中体现。

关于 config 配置的命令，在[Git 配置](git-two.md)一讲中已经说了，此处不再举例

#### refs

在 refs 目录下保存了 heads 和 tags 目录，前者保存了所有的分支文件，后者保存了所有的标签文件。

```
phoebe@phoebedeMacBook-Pro .git % cd refs
phoebe@phoebedeMacBook-Pro refs % ls
heads   remotes tags
```

heads 目录下的分支文件保存了各个分支最新的提交的 ID。

```
phoebe@phoebedeMacBook-Pro heads % ls
master
phoebe@phoebedeMacBook-Pro heads % cat master
2ddf0cb361557e12f0138e3181e810074d26a875
```

tags 目录下的标签文件中保存了各自 tag 的哈希值，该值的内容包含对应的提交信息。

```
phoebe@phoebedeMacBook-Pro refs % cd tags
phoebe@phoebedeMacBook-Pro tags % ls
newtag
phoebe@phoebedeMacBook-Pro tags % cat newtag
2ddf0cb361557e12f0138e3181e810074d26a875
```

#### object

.git 目录下的 object 包含很多以两个数字字母组合的文件夹，如果这些目录过多，就会打包保存到 pack 目录下。

```
phoebe@phoebedeMacBook-Pro .git % cd objects
phoebe@phoebedeMacBook-Pro objects % ls
05      18      2d      36      3f      4c      63      69      7b      83      8c      a6      c2      dc      ea      pack
0b      24      2e      37      46      55      64      76      7d      84      95      ac      cb      de      f9
0d      25      2f      3a      47      57      65      78      80      88      9a      ad      d4      df      fa
0e      2c      31      3d      4b      5c      66      7a      82      89      9b      b8      db      e9      info
```

object 下目录的字符，加上其内部的文件的名称，组合起来就构成一个新的哈希值，这个哈希值可能是 git 中的 tag、commit、tree 等类型。

```
phoebe@phoebedeMacBook-Pro objects % cd 05
phoebe@phoebedeMacBook-Pro 05 % ls
546220a2e73bb2165b91d6e068e21902a0a25c
phoebe@phoebedeMacBook-Pro 05 % cd ../
phoebe@phoebedeMacBook-Pro objects % git cat-file -t 05546220a2e73bb2165b91d6e068e21902a0a25c
blob
```
