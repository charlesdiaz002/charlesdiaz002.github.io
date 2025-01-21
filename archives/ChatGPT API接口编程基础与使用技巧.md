**总结/朱季谦**

![ChatGPT API](https://developer.qcloudimg.com/http-save/yehe-admin/fd07045035c2f28561d703eead088de7.png)

趁着这周末空闲时间，在研读完OpenAI官网文档的基础上，及时总结了这篇**《ChatGPT API接口编程基础与使用技巧》**。

本文主要围绕编程相关内容，包括ChatGPT模型接口、图像生成接口、敏感数据拦截等，同时也简要介绍了如何通过调整`temperature`参数优化提示技巧。

---

## 一、OpenAI API调用库

OpenAI提供了一系列模型接口API，包括ChatGPT、图像生成、音频处理、文件操作以及敏感数据拦截等功能。

开发者可以通过多种编程语言的HTTP请求与OpenAI API交互。以下是对Java、Go、Python和Node.js四种语言的简单介绍：

### 1.1 Java

官方推荐使用Theo Kanning开源的`openai-java`库。以下是集成到SpringBoot项目的基本步骤：

1. **引入Maven依赖**  
   在项目的`pom.xml`文件中添加以下依赖。

2. **调用示例**  
   使用绑定密钥的方式调用ChatGPT模型。

> **注意**：如果部署在需要“魔法代理”的Linux云服务器上，需对代码进行调整，否则可能会出现访问异常。

### 1.2 Go

官方推荐使用`sashabaranov`开源的`go-gpt3`库：

1. **安装依赖包**  
   使用`go get`命令安装相关依赖。

2. **调用示例**  
   参考官方提供的代码案例，绑定密钥后即可调用。

### 1.3 Python

1. **安装库**  
   使用`pip install openai`安装Python版本的OpenAI库。

2. **调用示例**  
   通过绑定密钥调用ChatGPT模型。

### 1.4 Node.js

1. **安装库**  
   使用`npm install openai`安装Node.js版本的OpenAI库。

2. **调用示例**  
   绑定密钥后调用ChatGPT模型。

---

## 二、密钥认证

OpenAI API需要使用API密钥进行认证访问。密钥获取方式如下：

1. 登录[OpenAI API密钥页面](https://bit.ly/bewildcard)。
2. 点击【Create new secret key】生成密钥。**注意**：密钥生成后需立即保存，后续无法再次查看。

调用API时，需要在HTTP请求报头中包含该API密钥。例如：

bash
curl https://api.openai.com/v1/completions \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -d '{"model": "text-davinci-003", "prompt": "Hello, world!"}'


---

## 三、GPT请求设置

官方提供了一个通过`curl`调用API的示例。以下是请求的基本结构：

- **模型**：如`gpt-3.5-turbo`。
- **提示语**：如“这是一个测试请求！”。
- **响应结果**：返回生成的文本内容。

请求体字段说明如下：

| 字段         | 说明                     |
| ------------ | ------------------------ |
| `model`      | 使用的GPT模型            |
| `prompt`     | 提示语                   |
| `temperature`| 控制生成文本的随机性     |

---

## 四、开发中添加敏捷信息审核层

根据《生成式人工智能服务管理办法（征求意见稿）》的要求，生成式AI服务需遵守法律法规，过滤违规内容。OpenAI提供了免费的内容审核API，开发者可以在输入/输出信息时调用该接口。

### 响应字段说明

- **flagged**：是否违反使用策略。
- **categories**：标记的违规类别。
- **category_scores**：模型对每个类别的置信度评分。

此外，开发者还可以自行构建敏感词过滤系统，对传入和返回的数据进行过滤。

---

## 五、模型调用

### 5.1 模型列表

通过API查询支持的模型类型，例如`gpt-3.5-turbo`是目前性价比最高的模型。

### 5.2 查询模型详情

可以查询指定模型的详细信息，包括基本信息、所有者及权限等。GPT-3.5-turbo是目前推荐使用的模型，具有较低的成本和较高的性能。

---

## 六、图像生成调用

OpenAI的图像生成接口可以根据提示生成图像。例如，输入“画一只胖猫”，模型会返回对应的图像URL。

### 接口参数

| 参数         | 说明                     |
| ------------ | ------------------------ |
| `prompt`     | 提示语                   |
| `size`       | 图像尺寸                 |
| `response_format` | 返回格式             |

---

## 七、ChatGPT使用技巧和注意事项

### 7.1 调整`temperature`参数

`temperature`参数用于控制生成文本的随机性：

- **低温度值**（如0.2）：生成内容更保守，适合摘要、翻译等任务。
- **高温度值**（如0.8）：生成内容更随机，适合创意写作。

例如，询问“如何形容一只胖猫？”时：

- 温度值为0.5：生成简短描述。
- 温度值为1.0：生成详细描述。
- 温度值为1.5：生成更具创意的描述。

### 7.2 数据存储

自2025年1月1日起，OpenAI保留API数据30天，但不会使用这些数据改进模型。建议避免传输涉及隐私或敏感信息。

---

👉 [WildCard | 一分钟注册，轻松订阅海外线上服务](https://bit.ly/bewildcard)
