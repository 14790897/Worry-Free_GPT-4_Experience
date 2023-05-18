# Worry-Free GPT-4 Experience
## Project Overview

The purpose of this project is to create a platform that allows users who do not have direct access to GPT-4 to experience the power of GPT-4 through the plus account holder's share.

## How it works

GPT-4's free usage is limited to a maximum of 25 requests every three hours. Since account holders need to rest at night, there are about 75 credits that cannot be used, so we can collect users' questions during the day and then use the unused GPT-4 credits to process them at night. User submitted questions will be temporarily stored in the Redis database with the key name "{username}:data". A thread in the project will listen to the time, and when it reaches 0:00 am, it will start the processors, read the user-submitted questions, process them and store the results in the Redis database along with the original questions, with the key name "f"{username}:results". This data will be stored for a long time so that users can see the history of their conversations with GPT-4 when they visit the homepage later.

As for how to interact with the web version of ChatGPT, please refer to [pengzhile/pandora: Pandora, a ChatGPT that helps you breathe smoothly. (github.com)](https:// github.com/pengzhile/pandora), this project requires building Pandora on your own server.

## Usage

modify .env.template to .env and fill in the appropriate parameters, SECRET_KEY can be generated at will, the URL is your own server domain name, you need to run Pandora on your own server, this step is difficult for whites, please be sure to master the server knowledge before considering using this project.

**Caution:** This project cannot be deployed in Vercel platform because Vercel does not support long running background threads.


## 项目概述

本项目旨在创建一个平台，让无法直接使用 GPT-4 的用户能够通过plus账号持有者的共享体验到 GPT-4 的强大功能。

## 工作原理

GPT-4 的免费使用额度限制为每三小时最多25条请求。由于账号持有者晚上需要休息，有大约75条的额度无法使用，因此我们可以在白天收集用户的问题，然后在晚上利用闲置的GPT-4额度进行处理。用户提交的问题将被暂存到Redis数据库中，键名为"{username}:data"。项目中的线程会监听时间，当到达凌晨0点后，启动处理程序，读取用户提交的问题，处理后将结果连同原始问题一起存入Redis数据库，键名为"f"{username}:results"。这些数据将被长期保存，以便用户在后续访问主页时能看到与GPT-4的历史对话记录。

本项目如何与网页版ChatGPT进行交互？其实是用了[pengzhile/pandora: 潘多拉，一个让你呼吸顺畅的ChatGPT。Pandora, a ChatGPT that helps you breathe smoothly. (github.com)](https://github.com/pengzhile/pandora)，所以本项目还需要在自己的服务器上搭建Pandora。

## 使用方法

将.env.template修改为.env并填入相应参数，SECRET_KEY可以随意生成，URL为自己的服务器Pandora项目域名，或者不会配置域名，用运行的Pandora项目的IP:端口替换也可以。

### 具体步骤：

假设你的vps是Ubuntu系统，

在/home/ubuntu目录，下载我的GitHub项目



```
sudo -i
```

输入以下命令

```
pip install -r requirements.txt
```

```
vim /etc/systemd/system/myapp.service
```

按i进入插入模式，复制以下内容，ctrl+shift+v粘贴，这样可以使项目后台运行

```
[Unit]
Description=My Python App
After=network.target

[Service]
User=ubuntu
WorkingDirectory=/home/ubuntu/app
ExecStart=/usr/local/bin/gunicorn --bind 127.0.0.1:5000 app:app
Restart=always

[Install]
WantedBy=multi-user.target
```

按下esc，输入:wq回车，保存并退出编辑器

开始运行命令

```
systemctl start myapp
```



命令行输入以下命令，使其开机自启动

```
systemctl enable myapp
```



#### 安装Pandora

下载Pandora项目



然后使项目后台运行

```
vim /etc/systemd/system/pandora.service
```

和之前一样，将以下内容复制进去

```
[Unit]
Description=Pandora Service
After=network.target

[Service]
ExecStart=/usr/local/bin/pandora -t t.json -s 127.0.0.1:8008
Restart=always
# 需要根据实际路径替换
WorkingDirectory=/home/ubuntu

[Install]
WantedBy=multi-user.target
```

开始运行命令

```
systemctl start myapp
```

开机启动命令

```
systemctl enable myapp
```

在/home/ubuntu目录下创建t.json文件，输入破解得到的账号token

根据需求，进行nginx配置，可以使用域名访问（本教程就不教了），也可以IP:端口直接访问以上两个项目。

