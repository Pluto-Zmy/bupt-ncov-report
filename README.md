# BUPT 疫情防控通 自动上报脚本

该脚本可以爬取您在”北邮疫情防控通“中上一次上报的信息，然后自动上报同样的信息。

该脚本既可以部署在任意一台服务器上，也可以部署在 GCP Cloud Function、AWS Lambda 或阿里云云函数等支持 Python 的云函数平台上。



## 使用前提

在使用本脚本前，您需要保证**昨天**~~_（格林威治时间）_~~（北京时间）已经正确填报了信息。如果您尚未填报，需要手动填报后，从**第二天开始**才能使用本脚本。



## 脚本依赖

- Python 3.7 或以上
- requests



## 脚本部署

#### 部署在 VPS 上

1. 通过 `git clone` 或 GitHub 的「下载 zip 文件」功能，将本仓库下载到您的电脑上；
2. 安装 Python 3.7 或以上版本。请注意，在较新的版本上，本脚本可能无法正常运行。
   1. 例如，如果您是 Ubuntu 18.04 LTS 用户，可以在设置 proposed 软件源之后，使用命令`sudo apt install python3.7`来安装。
3. 安装 requests 库：`pip install requests`
4. 如果您需要让该脚本定期自动运行，可以结合下方的”脚本运行“一栏来配置 cron 等工具。



#### 部署在 AWS Lambda 上

由于 AWS Lambda 不会自动下载依赖项，因此需要您手动下载依赖项并打包上传。

1. 配置 Python 3.7 虚拟环境，在虚拟环境中安装 requests；
2. 将虚拟环境下的 `site-packages` 文件夹中的内容，拷贝到与该脚本同一目录下；
3. 在 AWS Lambda 中新建一个函数：
   1. 按照下方”脚本运行（本机）“一节的说明，设置环境变量。
   2. 将所有文件上传；

**注：** 您可以通过 AWS CloudWatch 来自动执行该脚本。



### 部署在 GCP Cloud Function 上

GCP 支持通过 `requirements.txt` 自动下载依赖项，因此将所有文件（包括 `requirements.txt`） 打包上传即可。您需要：

1. 在 Cloud Function 中创建新函数；
2. 按照下方”脚本运行（本机）“一节的说明，设置环境变量。
3. 打包上传本仓库所有文件。

**注：** 建议您将该云函数的触发器设为 Cloud Pub/Sub 触发器，然后可以通过 GCP Cloud Scheduler 来自动执行该函数。





## 脚本运行（本机）

#### 设置环境变量

无论是在云端还是本机运行，运行之前都必须设置如下环境变量：

| 环境变量      | 说明                                                         |
| :------------ | :----------------------------------------------------------- |
| BUPT_SSO_USER | 您登录[北邮门户（https://my.bupt.edu.cn/）](https://my.bupt.edu.cn/)时使用的用户名，通常是您的学工号 |
| BUPT_SSO_PASS | 您登录[北邮门户（https://my.bupt.edu.cn/）](https://my.bupt.edu.cn/)时使用的密码 |
| TG_BOT_TOKEN  | （可选）如果您需要把执行结果通过 Telegram 机器人告知，请将此变量设为您的 Telegram 机器人的 API Token |
| TG_CHAT_ID    | （可选）如果您需要把执行结果通过 Telegram 机器人告知，请将此变量设为您自己的用户 id |

#### 运行

通过 python 命令运行 main.py 即可，无任何参数。



## 版权

使用 MIT 协议发布，著作权由代码的贡献者所有。

