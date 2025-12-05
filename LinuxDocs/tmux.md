# tmux (Terminal Multiplexer)
终端复用器，Linux/macOS 终端的 “超级管理器” —— 核心作用是打破单个终端窗口的限制。tmux支持的系统：
```bash
Linux、 macOS、 WSL
```
但是不支持原生Windows

## 1.下载

> sudo apt-get install tmux

## 2. 指令
会话是一个独立的运行环境，可以包含多个窗口。即使断开连接，会话也会继续在后台运行。每个会话可以包含多个窗口，类似于浏览器中的标签页。每个窗口可以分割成多个面板，允许同时查看和操作多个终端
### 会话
```bash
tmux new -s <name>	           # 创建名为 name 的新会话

Ctrl+b d	                   # 退出当前会话（后台继续运行）

tmux ls	                       # 列出所有会话

tmux attach -t <name>	       # 加载到指定会话

Ctrl+b $         	           # 重命名当前会话

Ctrl+b s	                   # 切换会话

tmux kill-session -t <name>    # 杀死指定会话

tmux kill-server               # 杀死所有会话 (慎用！)
```

### 窗口
```bash
Ctrl+b c	               # 创建新窗口
Ctrl+b &	               # 删除当前窗口
Ctrl+b n	               # 切换到下一个窗口
Ctrl+b p	               # 切换到上一个窗口
Ctrl+b <number>	           # 切换到指定编号的窗口
Ctrl+b ,	               # 重命名当前窗口
```

### 面板
```bash
Ctrl+b %	               # 垂直分割当前面板
Ctrl+b "	               # 水平分割当前面板
Ctrl+b x	               # 关闭当前面板
Ctrl+b z	               # 最大化/恢复当前面板,再按一次恢复
Ctrl+b Space	           # 切换面板布局
```

### 回滚/滚轮
> Ctrl+b [

q 退出

