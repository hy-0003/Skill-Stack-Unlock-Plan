# Conda in Linux
建议在 Linux 系统里下载 Miniconda。

### Linux下载Conda
```bash
# 1. 下载安装脚本 (从官网获取链接)
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh

# 2. 运行安装脚本
bash Miniconda3-latest-Linux-x86_64.sh

# 3. 初始化Conda
/root/miniconda3/bin/conda init bash

# 4. 刷新环境变量
source ~/.bashrc

# 5. 验证安装
conda --version
```

## 常见命令行

### 创建环境
> conda create -n 自定义名称 python=指定版本

### 进出环境
> conda activate 名称

> conda deactivate

### 配置环境
先试 conda install，如果没有再用 pip install

**注意**：PyTorch 千万不要直接 pip install torch ，需要去 PyTorch官网 复制带 CUDA 版本的命令

**关于Conda/Pip 混用**

基础包用 Conda，例如：

Python，PyTorch，NumPy

上层包用 Pip，例如

WandB, Einops, Hydra, Gym, HuggingFace Transformers

这些纯 Python 库，Pip 更新最快，版本最全

**注意**：一旦开始在该环境中使用 pip install，就尽量不要再回头用 conda install 去更新或安装核心库了。最忌讳的操作： 用 Conda 装了 NumPy，然后又用 Pip 强制更新了 NumPy，最后又用 Conda 装了依赖旧 NumPy 的库 —— 环境必炸。


### 查看已装包
> conda list

### 导出/复现环境
### 1. environment.yml
```bash
conda env export > environment.yml

conda env export --no-builds > environment.yml

conda env create -f environment.yml
```
### 2. requirements.txt
```bash
pip freeze > requirements.txt

pip install -r requirements.txt
```

### 3. 补充
导出环境前要激活要导出的环境，不然可能导出的是base。文件保存在 pwd：现在在哪文件就在哪。

> --no-builds

去掉臃肿的构建号，跨平台兼容性更好

> conda env export / pip freeze

把环境信息打印在屏幕

### 删除环境
> conda env remove -n 名称

### 清理缓存
> conda clean --all

### 移除源
> conda config --remove-channels defaults