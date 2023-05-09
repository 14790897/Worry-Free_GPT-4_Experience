# Worry-Free GPT-4 Experience
Project Overview: The purpose of this project is to create a free platform that allows users who do not have direct access to GPT-4 to experience the power of GPT-4.

How it works: GPT-4's free usage quota is limited to a maximum of 25 requests every three hours. Since account holders need to rest at night, there are about 75 credits that cannot be used, so we can collect users' questions during the day and then use the unused GPT-4 credits to process them at night. User submitted questions will be temporarily stored in the Redis database with the key name "{username}:data". A thread in the project will listen to the time, and when it reaches 0:00 am, it will start the processors, read the user-submitted questions, process them and store the results in the Redis database along with the original questions, with the key name "f"{username}:results". This data will be stored for a long time so that users can see the history of their conversations with GPT-4 when they visit the homepage later.

As for how to interact with the web version of ChatGPT, please refer to [pengzhile/pandora: Pandora, a ChatGPT that helps you breathe smoothly. (github.com)](https:// github.com/pengzhile/pandora), this project requires building Pandora on your own server.

Usage: modify .env.template to .env and fill in the corresponding parameters, SECRET_KEY can be generated at will, the URL is your own server domain name, you need to run Pandora on your own server, this step is difficult for whites, please be sure to master the server knowledge before considering using this project.

Note: This project cannot be deployed on Vercel platform because Vercel does not support long running background threads.



项目概述：本项目旨在创建一个免费平台，让无法直接使用 GPT-4 的用户能够体验到 GPT-4 的强大功能。

工作原理：GPT-4 的免费使用额度限制为每三小时最多25条请求。由于账号持有者晚上需要休息，有大约75条的额度无法使用，因此我们可以在白天收集用户的问题，然后在晚上利用闲置的GPT-4额度进行处理。用户提交的问题将被暂存到Redis数据库中，键名为"{username}:data"。项目中的线程会监听时间，当到达凌晨0点后，启动处理程序，读取用户提交的问题，处理后将结果连同原始问题一起存入Redis数据库，键名为"f"{username}:results"。这些数据将被长期保存，以便用户在后续访问主页时能看到与GPT-4的历史对话记录。

至于如何与网页版ChatGPT进行交互，请参考[pengzhile/pandora: 潘多拉，一个让你呼吸顺畅的ChatGPT。Pandora, a ChatGPT that helps you breathe smoothly. (github.com)](https://github.com/pengzhile/pandora)，本项目需要在自己的服务器上搭建Pandora。

使用方法：将.env.template修改为.env并填入相应参数，SECRET_KEY可以随意生成，URL为自己的服务器域名，需要在自己的服务器上运行Pandora，这一步对小白来说很难，请务必掌握服务器知识再考虑使用此项目。

注意事项：本项目无法在Vercel平台部署，因为Vercel不支持长期运行的后台线程。