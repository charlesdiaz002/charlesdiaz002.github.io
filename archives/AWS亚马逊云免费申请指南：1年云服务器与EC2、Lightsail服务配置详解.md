## 准备外币信用卡

> 在国外购买服务通常需要外币信用卡。即使拥有国内银行发行的外币卡，有些服务仍可能无法购买。这时可以选择虚拟信用卡平台。以下是几个常见的虚拟信用卡平台：

1. **EASYPAY**  
   曾经支持注册两张虚拟信用卡，但目前已退出中国市场。以下是尝试申请亚马逊云的截图，经过多次信息更新后成功验证。

2. **PokeyPay**  
   可申请前两张无月费的虚拟卡，使用成本较低。

3. **FOMECard**  
   使用方便，是EASYPAY失效后常用的虚拟卡平台之一。

---

## 亚马逊云服务介绍

### 免费试用产品

亚马逊云官网：[AWS 免费套餐](https://aws.amazon.com/cn/free/)  
推荐免费试用的服务包括：

- **Lightsail 服务**：适合轻量级应用，试用期为3个月。
- **EC2 服务**：提供12个月免费试用，适合搭建服务器。

---

## 注册亚马逊云账号

1. 访问 [AWS 免费套餐](https://aws.amazon.com/cn/free/)，点击“创建免费账号”。
2. 按提示填写真实信息，避免因风控导致注册失败。
3. 验证邮箱、设置密码。
4. 填写外币信用卡信息。
5. 验证手机号并选择默认账户计划，完成注册。

---

## 使用AWS控制台

1. 登录控制台：[AWS 控制台](https://console.aws.amazon.com)。
2. 设置区域，选择离自己最近的区域（如日本、新加坡、首尔）。
3. 搜索并进入 **EC2 服务**（通常需要24小时激活）。
4. 搜索并进入 **Lightsail 服务**，试用期为3个月。

---

## EC2服务配置

### 创建实例

1. 输入实例名称，选择操作系统。
2. 选择实例类型，推荐免费套餐。
3. 创建密钥对并下载，用于登录服务器。
4. 设置存储，默认10GB，免费额度为30GB。

### 启动实例

1. 启动实例后，使用私钥或网页直接登录服务器。
2. 默认用户名为 `ec2-user`。
3. 在安全组中开放必要端口。

### 开启Root用户登录

1. 切换到Root用户：
   bash
   sudo -i
   
2. 编辑SSH配置文件：
   bash
   vi /etc/ssh/sshd_config
   
3. 修改以下两项：
   bash
   PermitRootLogin yes
   PasswordAuthentication yes
   
4. 设置Root密码：
   bash
   passwd
   
5. 重启SSH服务：
   bash
   systemctl restart ssh
   

---

## Lightsail服务配置

1. 创建实例时选择位置、平台和操作系统（推荐CentOS 7）。
2. 选择实例计划后完成创建。
3. 实例创建完成后即可使用。

---

## 网络IO测试

运行以下命令测试网络性能：
bash
wget -qO- bench.sh | bash


测试结果示例：

I/O Speed(average): 141.0 MB/s
Upload Speed: 4038.81 Mbps
Download Speed: 4691.55 Mbps


---

## 注意事项

- 免费试用期为12个月（EC2）和3个月（Lightsail），从账号注册日开始计算，请注意避免超时使用。

---

👉 [WildCard | 一分钟注册，轻松订阅海外线上服务](https://bit.ly/bewildcard)