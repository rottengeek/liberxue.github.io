---
layout: blog
book: false
background-image: https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=4218016970,2585188894&fm=11&gp=0.jpg
category: 系统
title: 常用命令
tags:
- 命令
- linux
date:   2020-04-27 00:13:54
redirect_from:
  - /2020/04/linuxCommand/
---

## Linux命令

### mac免秘钥登陆服务器

```shell
# mac
cd ~/.ssh
ssh-keygen -t rsa
## 将生成的id_rsa.pub copy到服务器

scp ~/.ssh/id_rsa.pub daituodi@10.10.14.120:/home/daituodi/.ssh/

# linux
cd ~/.ssh
cat -n /home/daituodi/.ssh/id_rsa.pub >> authorized_keys #将公钥内容加入到authorized_keys文件，没有则新建一个就行


git config --global credential.helper store  保存免密
```

从服务器copy文件到本地

```shell
# mac
scp daituodi@10.10.14.120:/home/daituodi/kafka.log /Users/rottengeek/Desktop
```

### grep

```shell
统计某文件夹下文件的个数　

ls -l |grep "^-"|wc -l 

统计某文件夹下目录的个数　　

ls -l |grep "^ｄ"|wc -l

统计文件夹下文件的个数，包括子文件夹里的　　

ls -lR|grep "^-"|wc -l
```



### VI命令

```shell
按I进入插入模式，按V进入视图模式

## 删除
命令行模式
	:3,4d 删除3到4行

普通模式 光标所在行
	Ndd  包括光标所在的N行

## 复制粘贴
普通模式：
	2yy 复制2行  p粘贴

## 撤销
命令行模式
	输入u

## 查找
命令行模式
	:/  要查找的词 或者正则 用n来继续查找下一个

## 定位
G:文章末尾
3G:第3行
gg:文章开头

## 翻页
ctrl + f 下翻
ctrl + b 上翻
```

## Anaconda

### Jupyter notebook

```shell
安装主题
# Kill and exit the Notebook server
# Make sure you are in the base conda environment
conda activate base 
# install jupyterthemes
pip install jupyterthemes

# upgrade to latest version
pip install --upgrade jupyterthemes

# Enable Dark Mode
jt -t onedork -fs 95 -altp -tfs 11 -nfs 115 -cellw 88% -T


安装插件
# Stop and exit your Jupyter Notebook server 
# Make sure you are in the base environment
conda activate base
# Install the nbextensions 
pip install jupyter_contrib_nbextensions
# Install the necessary JS and CSS files 
jupyter contrib nbextension install --system
```

### conda换源

```shell
将以上配置文件写在 ~/.condarc 中

vim ~/.condarc

channels:
  - https://mirrors.ustc.edu.cn/anaconda/pkgs/main/
  - https://mirrors.ustc.edu.cn/anaconda/cloud/conda-forge/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
  - defaults
show_channel_urls: true
```

### conda设置默认路径

```shell
# 输入
jupyter notebook --generate-config  # 会将配置重写

vi /Users/rottengeek/.jupyter/jupyter_notebook_config.py

c.NotebookApp.notebook_dir = '期望的默认目录'
```



### conda虚拟环境

```shell
conda create -n nlp python  
source activate nlp
pip install scikit-learn -i https://pypi.douban.com/simple
pip install ipykernel
python -m ipykernel install --user --name=nlp

conda remove -n your_env_name(虚拟环境名称) --all
```

```shell
conda update conda
conda update --all
```
###  删除anaconda

```shell
conda install anaconda-clean
anaconda-clean

rm -r /Users/rottengeek/.anaconda_backup/2019...

rm -rf /opt/anaconda3

vim ~/.bash_profile  打开环境变量删除anaconda的环境变量

rm -rf ~/.condarc ~/.conda ~/.continuum
```


## virtualenv 虚拟环境

```shell
# 一定要加sudo
sudo pip install virtualenv
sudo pip install virtualenvwrapper


 vim ~/.bash_profile 或者 ~/.zshrc

# virtualenvwrapper
export WORKON_HOME='~/.virtualenvs'
export VIRTUALENVWRAPPER_PYTHON='/Users/rottengeek/anaconda3/bin/python3'
source /Users/rottengeek/anaconda3/bin/virtualenvwrapper.sh


创建基本环境：mkvirtualenv [环境名]

删除环境：rmvirtualenv [环境名]

激活环境：workon [环境名]

退出环境：deactivate

列出所有环境：workon或者lsvirtualenv -b
```








## coursera无法播放视频

```shell
sudo vi /etc/hosts

52.84.246.90    d3c33hcgiwev3.cloudfront.net
52.84.246.252   d3c33hcgiwev3.cloudfront.net
52.84.246.144   d3c33hcgiwev3.cloudfront.net
52.84.246.72    d3c33hcgiwev3.cloudfront.net
52.84.246.106   d3c33hcgiwev3.cloudfront.net
52.84.246.135   d3c33hcgiwev3.cloudfront.net
52.84.246.114   d3c33hcgiwev3.cloudfront.net
52.84.246.90    d3c33hcgiwev3.cloudfront.net
52.84.246.227   d3c33hcgiwev3.cloudfront.net


sudo killall -HUP mDNSResponder # 刷新DNS
```

## redis安装

```python
To have launchd start redis now and restart at login:
brew services start redis

Or, if you don't want/need a background service you can just run:
redis-server /usr/local/etc/redis.conf

# 退出redis
ps aux|grep redis
kill -15 pid

或者
redis-cli SHUTDOWN
```
