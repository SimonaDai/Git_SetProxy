
### 1. **拉取远程更改**

* 运行以下命令，将远程的更改拉取到本地：

  ```bash
  git pull origin <branch-name>
  ```

  （将 `<branch-name>` 替换为你的分支名称，比如 `main` 或 `master`）
* 如果有冲突，Git 会提示你解决冲突。解决冲突后，再提交并推送。

### 2. **强制推送（谨慎使用）**

* 如果你确定本地的更改是正确的，可以强制推送：

  ```bash
  git push origin <branch-name> --force
  ```

  （谨慎使用，这会覆盖远程仓库的历史记录）


### 修改远程仓库名称

如果你需要修改远程仓库的名称，可以使用以下命令：

```bash
git remote rename <old-name> <new-name>
```

```bash
git remote rename origin upstream
```

这会将远程仓库名称从 `origin` 改为 `upstream`。


**更新git**

```
 git update-git-for-windows
```

### **检查 Git 配置**

```
 git config --list
```

**验证代理设置:**

```
 git config --global --get http.proxy
 git config --global --get https.proxy
```

**取消代理:**

```
 git config --global --unset http.proxy
 git config --global --unset https.proxy
```

### **检查代理服务是否运行**

**确保你的 Socks5 代理服务（如 Shadowsocks、V2Ray 等）正在运行，并监听 **`127.0.0.1:51837`。可以通过以下命令检查端口是否开放：=Socks端口号根据看自己的配置设置=

```
 netstat -tulnp | grep 51837
```

#### **全局设置用户和邮箱**

```
 # 设置全局用户名
 git config --global user.name "你的名字"
 
 # 设置全局邮箱
 git config --global user.email "你的邮箱地址"
```

1. `git init`：该命令用于在当前目录中初始化一个新的Git仓库。它会创建一个名为 `.git`的隐藏文件夹，用于存储Git仓库的相关信息。
2. `git add README.md`：该命令将名为"README.md"的文件添加到Git的暂存区。暂存区是Git用来跟踪文件更改的一个中间区域。
3. `git config --global user.email "you@example.com"`：该命令用于设置Git的全局配置，其中 `user.email`是你的邮箱地址。这个配置将与你的提交记录相关联。
4. `git config --global user.name "Your Name"`：该命令用于设置Git的全局配置，其中 `user.name`是你的用户名。这个配置将与你的提交记录相关联。
5. `git commit -m "first commit"`：该命令用于将暂存区中的文件提交到Git仓库。`-m`选项后面的内容是提交的描述信息，用于解释本次提交的目的。
6. `git branch -M main`：该命令用于重命名当前分支。这里将当前分支重命名为"main"，这是GitHub默认的主分支名称。
7. `git remote add origin https://github.com/Wang-Phil/test.git`：该命令用于将本地仓库与远程GitHub仓库关联起来。`origin`是远程仓库的别名，`https://github.com/Wang-Phil/test.git`是远程仓库的URL。
8. `git push -u origin main`：该命令用于将本地仓库的内容推送到远程GitHub仓库。`-u`选项表示将本地的"main"分支与远程仓库的"main"分支关联起来。这样，在以后的推送中，你只需要运行 `git push`命令即可。

## 设置https 代理

**Git代理有两种设置方式，分别是全局代理和只对Github代理，建议只对github 代理。**
**代理协议也有两种，分别是使用http代理和使用socks5代理，建议使用socks5代理。**
**注意下面代码的端口号需要根据你自己的代理端口设定，比如我的代理socks端口是51837。**

**全局设置（不推荐）**

```
 #使用http代理 
 git config --global http.proxy http://127.0.0.1:58591
 git config --global https.proxy https://127.0.0.1:58591
 #使用socks5代理
 git config --global http.proxy socks5://127.0.0.1:51837
 git config --global https.proxy socks5://127.0.0.1:51837
```

**只对Github代理（推荐）**

```
 #使用socks5代理（推荐）
 git config --global http.https://github.com.proxy socks5://127.0.0.1:51837
 #使用http代理（不推荐）
 git config --global http.https://github.com.proxy http://127.0.0.1:58591
```

**取消代理**
**当你不需要使用代理时，可以取消之前设置的代理。**

```
 git config --global --unset http.proxy git config --global --unset https.proxy
```

**socks5代理**

## 设置ssh代理（终极解决方案）

**https代理存在一个局限，那就是没有办法做身份验证，每次拉取私库或者推送代码时，都需要输入github的账号和密码，非常痛苦。**
**设置ssh代理前，请确保你已经设置ssh key。可以参考**[在 github 上添加 SSH key](https://link.zhihu.com/?target=https%3A//tjfish.github.io/posts/%E5%9C%A8github%E4%B8%8A%E6%B7%BB%E5%8A%A0SSH-key/) 完成设置**
**更进一步是设置ssh代理。只需要配置一个config就可以了。

```
 # Linux、MacOS
 vi ~/.ssh/config
 # Windows 
 到C:\Users\your_user_name\.ssh目录下，新建一个config文件（无后缀名）
```

**将下面内容加到config文件中即可**

**对于windows用户，代理会用到**[connect.exe](https://zhida.zhihu.com/search?content_id=195148009&content_type=Article&match_order=1&q=connect.exe&zhida_source=entity)，你如果安装了Git都会自带connect.exe，如我的路径为C:\APP\Git\mingw64\bin\connect

```
 #Windows用户，注意替换你的端口号和connect.exe的路径
 ProxyCommand "C:\APP\Git\mingw64\bin\connect" -S 127.0.0.1:51837 -a none %h %p
 
 #MacOS用户用下方这条命令，注意替换你的端口号
 #ProxyCommand nc -v -x 127.0.0.1:51837 %h %p
 
 Host github.com
   User git
   Port 22
   Hostname github.com
   # 注意修改路径为你的路径
   IdentityFile "C:\Users\Your_User_Name\.ssh\id_rsa"
   TCPKeepAlive yes
 
 Host ssh.github.com
   User git
   Port 443
   Hostname ssh.github.com
   # 注意修改路径为你的路径
   IdentityFile "C:\Users\Your_User_Name\.ssh\id_rsa"
   TCPKeepAlive yes
```

**保存后文件后测试方法如下，返回successful之类的就成功了。**

```
 # 测试是否设置成功
 ssh -T git@github.com
```

**之后都推荐走ssh拉取代码，再github 上选择clone地址时，选择ssh地址，入下图。这样** `git push` 与 `git clone` 都可以直接走代理了，并且不需要输入密码。

![img](https://pic4.zhimg.com/v2-0e58a44f513be7005919b320222f2985_1440w.jpg)

## 原理部分

**代理服务器就是你的电脑和互联网的中介。当您访问外网时（如**[http://google.com](https://link.zhihu.com/?target=http%3A//google.com)) , 你的请求首先转发到代理服务器，然后代理服务器替你访问外网，并将结果原封不动的给你的电脑，这样你的电脑就可以看到外网的内容啦。**
**路径如下：

> **你的电脑->代理服务器->外网**
> **外网->代理服务器->你的电脑**
