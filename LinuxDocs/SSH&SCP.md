# VScode-SSH

**第一步：** 云服务器实例化，安全配置好（防火墙打开）。保证本地已安装 OpenSSH 客户端，一般现在的都会自动配有。

**下一步：** 第一次要自己本地生成密钥和公钥，以后可以直接用这个公钥。

> ssh-keygen -t rsa -b 4096

一路回车即可

<br>

**第二步：** 上传公钥
> ssh-copy-id username@服务器公网IP

只要输入一次密码以后就可以直接连接了

<br>

**第三步：** VScode-SSH打开, 命令行为：

> ssh username@服务器公网IP -p 端口号(SSH默认为22) -i 私钥路径

<br>

**第四步：** 本地的.ssh\config（你所选择的ssh\config），写入配置：（示例）

    Host ali-ecs
        HostName 39.104.28.219      # ECS公网IP
        User root                   # 登录用户名
        Port 22                     # SSH端口（默认22）
        IdentityFile ~/.ssh/id_rsa  # 本地私钥路径

        # --- 以下是可选配置 ---
        ServerAliveInterval 30      # 30秒发一次心跳，避免连接断开
        Compression yes             # 启用压缩，加快传输

<br>

**第五步：SSH连接**


**部分解惑答疑：** SSH 非对称加密的身份验证逻辑决定的 —— 私钥由身份持有者保密，公钥用于公开验证。也就是自己本地要有一对密钥公钥，将公钥发送给其它机构，其它机构就可以承认/录入你的身份，这样你配置好config后申请进入服务器时，服务器会根据你的公钥匹配你的密钥，匹配成功就放你通过。

<br>

## *25.12.4* 服务器被黑客暴力破解

**原因：** 安全组/防火墙允许 SSH(22)，IP任意 进行远程连接且设置了弱密码

### 安全加固
第一步：进入服务器，加载进入 SSH 服务端的主配置文件  
> vim  /etc/ssh/sshd_config

<br>

第二步：修改 SSH 配置：将密码登录禁止
> i / o （进入编辑模式）

修改添加： PasswordAuthentication no 后

> ESC + :wq

**注意**：i 代表在光标处开始编辑，o代表从末尾开始编辑。:wq 分别意为：write，写入/保存，quit，退出。如果不想保存并退出写入 :q! 强制退出，不保存

<br>

第三步：语法检查
> sudo sshd -t

<br>

第四步：重启使得修改生效
> sudo service ssh restart

**最后：检查**

在执行重启命令后，千万不要关闭当前终端窗口。应该立即新建一个终端尝试 ssh username@ip 。可以直接登录后再放心关闭原终端，若报错则证明公钥没配好，先把密码登录权限打开。

<br>

<br>

# SCP = SSH + Copy
## scp [源] [目标]

### 1. 传送
scp [本地文件] [远程账号]@[远程IP]:[远程路径]

本地文件可以是 image.png 也可以是 main.py... ，远程账号是指在服务器的名字

远程路径大概率是 /home/远程账号/ ，可以用 ~ 代替

示例：
> scp ./main.py student@128.32.xx.xx:~/

### 2. 下载
scp [远程账号]@[远程IP]:[远程文件] [本地路径]

### 3. 文件夹
传输文件夹时需要在 scp 后添加参数 -r
> scp -r image student@128.32.xx.xx:home/student/

### 4. SSH Config
合理修改 SSH Config 使得命令行变简便：
```bash
Host abc
    HostName 128.32.xx.xx       # ECS公网IP
    User student                # 登录用户名
    Port 22                     # SSH端口（默认22）
    IdentityFile ~/.ssh/id_rsa  # 本地私钥路径

    # --- 以下是可选配置 ---
    ServerAliveInterval 30      # 30秒发一次心跳，避免连接断开
    Compression yes             # 启用压缩，加快传输
```
设置之后，之前的命令行: student@128.32.xx.xx 可以用abc来代替，示例：
> scp main.py abc:~/

> ssh abc

### 5. 大文件传输 rsync
> rsync -avP [源大文件] [远程账号]@[远程IP]:[远程路径]

**补充**：rsync 支持断点续传（断了连上接着传）而且速度更快，需要添加参数 -avP