作为一名热爱插画的用户，及时获取自己关注的画师在 Pixiv 上的最新作品是一种重要的生活习惯。然而，每天手动检查新图不仅费时费力，如何更高效地推送这些喜爱的图片，让每一张图都有机会展现它的光彩呢？

我想到了一种常用的资讯订阅方式：RSS。幸运的是，我在 RSSHub 的文档中找到了针对 Pixiv 关注画师新图的订阅接口。单纯的 RSS 订阅虽然可以，但还需要一个阅读器，直接将这些资讯推送至通讯工具上显然更为方便。

之前我尝试过基于 IFTTT 的解决方案，将 RSSHub 生成的内容推送至 Telegram 频道。但由于 IFTTT 的使用策略更改，非付费用户仅能创建三个小程序，这让我不得不寻找其他方案。作为开发者，我决定自己编写一个功能相似的处理工具，这不仅能锻炼我的代码能力，还能提高可自定义性。

在研究各种 API 接口后，我的思路很简单：通过 RSS 收集数据，整理后通过 Bot 的 API 接口发送至 Telegram 频道。由于我习惯使用 Node.js 进行开发，这次也选择了它作为开发与部署的平台。

## 第一步：RSS 采集

首先进行 RSS 的采集。为了避免手动分析 XML 文件的繁琐，我使用了一个现成的组件：`rss-parser`。该组件可以获取 RSS 资讯，并将其转化为对象，方便后续处理。

安装组件的命令如下：

bash
npm i rss-parser --save


使用完成后的参数调用方式也非常简洁。我选择了直接传递参数的方式，而不是使用官方样例中的 async 和 await 异步函数处理。

在测试时，可以将获取的 feed 信息输出，以 RSSHub 生成的数据为例，我们不难发现其内部其实是一个对象数组，因此可以直接使用相关字段进行内容处理。

## 第二步：数据处理

由于 RSSHub 设计的初衷是为了方便阅读，因此生成的内容格式仍以可读性为主，主要由 pixiv.cat 的图片传递接口组成。不过，获取的内容中包含了我们需要的所有信息，因此可以使用正则表达式进行提取。

对于单张图片的内容，RSSHub 将其处理成形如 `https://pixiv.cat/*ArtworkID*.jpg` 的链接；而对于多图内容，ArtworkID 后的 `-PicID` 也是我们关注的关键。可以使用以下正则表达式进行处理：

javascript
const picIdReg = /https:\/\/pixiv\.cat\/(\d+)-?(\d+)?\.(jpg|png|gif)/gi;


结合这条正则表达式，可以直接生成内容数组：

javascript
const artworks = [...item.content.matchAll(picIdReg)];


对于单图的输入，我们将得到形如：


> Array ["https://pixiv.cat/*ArtworkID*-1.jpg", "*ArtworkID*", "1", "jpg"]


考虑到 Telegram 对于图片大小的限制，我们选择使用预览图发送，并将完整图下载。通过查看pixiv前端页面的源码，预览图的地址由前缀、发布时间（UTC+9）、作品 ID 和一些固定元素组合而成。发布时间可以由 RSS item 中的 isoDate 手动计算获取，我们可以编写一个整合表达式来完成预览图地址的装配工作。

## 第三步：消息发送

之前在 IFTTT 中使用的是直接推送订阅内容，让 Telegram 自动获取的方式，这导致了大图片（≥5MB）无法有效获取、图片缓存请求限制等问题。因此，这次我们加入请求缓冲队列和预览图片，尝试解决以上问题。

本来打算使用 Telegraf 作为推送框架，但考虑到只有一个请求信息，因此直接使用 got 进行 POST 请求的发送。根据 Telegram 的 Bot API 文档，可以整理出如下的请求样式：

javascript
const apiBaseUrl = `https://api.telegram.org/bot${confData.bot.token}`;

got('sendPhoto', {
    method: 'POST',
    prefixUrl: apiBaseUrl,
    json: {
        chat_id: confData.bot.chat,
        photo: picItem.preview,
        caption: picItem.text,
        reply_markup: {
            inline_keyboard: [
                [{
                    text: '🌏',
                    url: picItem.url
                }, {
                    text: '⤵',
                    url: picItem.pic
                }]
            ]
        }
    }
});


这里直接调用了 Telegram 的 sendPhoto 接口发送图片请求数据，加入了消息下的内联小键盘 `inline_keyboard`，为用户提供了图片的原始链接按钮和直接下载按钮，以方便操作。

为了避免每次启动时将所有图片加入队列等待发送，并考虑到项目提供的所有数据都是按照时间排序的，我们维护一个时间戳，初始化为当前时间。每次将待发送的图片时间记录最晚值，之后查询时仅发送更新的内容并更新时间戳标记即可。

为了进一步为用户提供方便，我们还加入了前端的 js-yaml 组件来读取 yml 配置文件。最终整合的版本已经发布到了 GitHub 的 [PhanDream](https://github.com/Candinya/PhanDream) 仓库中；您可以使用诸如 pm2 等方式进行运行：

bash
pm2 start bot.js --name phandream


当一切准备完成后，您将能在频道中发现新的图片啦！

👉 [野卡 | 一分钟注册，轻松订阅海外线上服务](https://bit.ly/bewildcard)