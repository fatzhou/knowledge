# Git 配置

在我们正式使用 git 之前，我们需要配置 git 信息在我们本机

### 配置 user 信息

user 信息主要是包括我们在 git 上注册的用户名和邮箱，接下来可以通过两个命令去配置 user.name 和 user.email。

配置 user.name 的时候，我们只需要将'my_name'替换成你自己的 git 用户名

`$ git config --global user.name 'my_name'`

配置 user.email 的时候，我们只需要将'my_email'替换成注册的 git 邮箱

`$ git config --global user.email 'my_email@demo.com'`

#### config 的三个作用域

##### 缺省等同于 local

- local 表示只对某个仓库有效

`$ git config --local`

- global 表示对当前用户所有仓库有效

`$ git config --global`

- system 表示对系统所有登录的用户有效

`$ git config --system`

##### 显示 config 的配置，加 --list

```
$ git config --list --local

$ git config --list --global

$ git config --list --system
```

## 怎么在一个 system 上配置多个用户

如果我们注册了多个 git 用户，并且需要在同一个 system 上去配置多个用户时，我们需要用以下命令

- 第一步就是添加我们的用户名和邮箱

```
$ git config --global user.name 'newkey'

$ git config --global user.email 'newkey@demo.com'
```

- 第二步就是生成 ssh 密钥，通过以下两个命令

```
$ cd ~/.ssh

$ ssh-keygen -t ed25519 -C "your_email@example.com"
```

然后就可以看到我们生成的 newkey 文件和 newkey.pub 文件，使用一下命令查看内容

`$ cat newkey.pub`

然后拷贝生成的密钥，使用浏览器登录我们的 git 账号，在 setting 处将拷贝的内容配置好

- 最后一步就是将我们生成的 key 添加到我们的系统

`$ ssh-add -K ~/.ssh/newkey`

这样我们的多用户信息就配置好了，接下来我们就可以直接 git push 我们的变更了
