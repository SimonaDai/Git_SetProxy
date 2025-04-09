
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
