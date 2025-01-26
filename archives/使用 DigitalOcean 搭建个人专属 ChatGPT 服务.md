本教程将指导您如何使用 DigitalOcean 服务器和开源项目 [Chatgpt-web](https://github.com/Chanzhaoyu/chatgpt-web) 搭建私人 ChatGPT 服务，整个过程简单可靠。

## 费用说明

- DigitalOcean 服务器：4美元/月（新用户可获得200美元免费额度，有效期2个月）
- OpenAI API 费用：每10万 token 约0.04美元（约5万汉字）

👉 [野卡 | 一分钟注册，轻松订阅海外线上服务](https://bit.ly/bewildcard)

## 准备工作

1. DigitalOcean 账号
2. OpenAI API Key
   - OpenAI 仅支持国际信用卡支付
   - 需要非中国区手机号验证
   - 可使用 野卡 服务，费率3%（邀请码：ACCPAY）

## 详细步骤

### 一、创建 DigitalOcean 服务器

1. 选择新加坡数据中心
2. 操作系统选择 CentOS 8
3. 配置选择基础版（4美元/月）
4. 身份验证方式选择 SSH Key（按照控制台指引配置）
5. 创建完成后保存服务器 IP 地址

### 二、安装 Docker

1. 更新 yum
bash
yum update


2. 下载 docker-ce 仓库
bash
curl https://download.docker.com/linux/centos/docker-ce.repo -o /etc/yum.repos.d/docker-ce.repo


3. 安装依赖
bash
yum install https://download.docker.com/linux/fedora/30/x86_64/stable/Packages/containerd.io-1.2.6-3.3.fc30.x86_64.rpm


4. 安装并配置 Docker
bash
yum install docker-ce
systemctl start docker
systemctl enable docker


5. 安装 Docker Compose
bash
yum -y install wget
sudo wget https://github.com/docker/compose/releases/download/1.25.4/docker-compose-$(uname -s)-$(uname -m) -O /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose


### 三、部署 ChatGPT

1. 创建项目目录和配置文件
bash
mkdir chatgpt_web && cd chatgpt_web
yum -y install vim*
vim docker-compose.yml


2. 配置文件内容
yaml
version: '3'
services:
  app:
    image: chenzhaoyu94/chatgpt-web:latest
    ports:
      - 3002:3002
    environment:
      OPENAI_API_KEY: sk-xxx
      TIMEOUT_MS: 60000


3. 启动服务
bash
docker-compose up -d


4. 访问服务
- 浏览器访问：`http://服务器IP:3002`

### 常见问题

- 如遇到 fetch failed，可点击刷新按钮重试
- 如刷新无效，重启 Docker 服务后重新启动应用

至此，您的私人 ChatGPT 服务已经搭建完成！

👉 [野卡 | 一分钟注册，轻松订阅海外线上服务](https://bit.ly/bewildcard)