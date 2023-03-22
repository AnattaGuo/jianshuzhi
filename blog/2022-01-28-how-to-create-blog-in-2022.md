---
slug: how-to-create-blog-in-2022
title: 如何搭建个人博客 (2022)
tags: [博客, docusaurus, 文档]
---

## 1. 为什么要建个人博客

其实有这个念头已经有很多年了，博客刚刚兴起那会就在网上写一些碎碎念的东西，平台从博客中国、到博客大巴、到新浪微博、到简书、到微信公众号，没有哪一个是持续且持久的，而且在别人的平台上，有些内容不知哪里违禁，给我撤下来了。前几日，无意间刷到一个[个人网站](https://www.bmpi.dev/)，又激发了我建立个人独立博客的念头，当机立断，决定着手建立一个个人独立博客，从买域名到部署，总共花了 4 天的时间。

建立个人博客，有一个根本需求，**藉由写这个行为时不时和自己聊一聊，以倒逼自己对自己的记录、整理和输出。** 如果跟自己聊得不错，能构建自己的系统也是极好的，至于其他，都是后话。

## 2. 如何建站

以下步骤大致记录了我的建站过程：

1. 购买一个域名
2. 在本地搭建博客
3. 把本地博客推送到 Github
4. 部署博客网站

<!--truncate-->

### 2.1. 购买一个域名{#buy-domain}

在购买域名之前，可以先想好自己博客的地址，然后再去域名购买网站上查看，这个地址是不是已经被其他买了。

我是在 [GoDaddy](https://godaddy.com/) 上购买的域名，GoDaddy 支持支付宝付款。当然也可以选择去阿里云旗下的[万网](https://wanwang.aliyun.com)购买域名。在下单前可以先去淘宝搜索一下是否有 GoDaddy 的优惠券可用。

选域名这个步骤花费了我大概 6 个小时的时间，一个方面是因为备选的域名不是被人注册了，就是太贵；另一方面，我本人比较纠结。本来想一次性买 10 年，让自己做好 10 年记录的准备，但是又对自己是否能坚持那么就不太确定，就改成了 3 年了。

### 2.2. 在本地搭建博客

#### 2.2.1. 选择搭建个人博客的工具

搭建个人博客或网站的工具有很多，比如 Hugo, Hexo, [Jekyll](/), MkDocs, Gatsby 等等。从众多工具中选择 docusaurus 的原因很简单，它是我在工作使用的工具，公司所有产品的文档网站都是使用这个工具搭建，已经很熟悉了，不想花时间去熟悉其他工具的使用。

[Docusaurus](https://docusaurus.io) 是 Facebook 的开源工具之一，它可以让用户建立自己的文档网站，可以设置为 `blog-only` 的模式。关于 [Docusaurus 和其他工具的比较](https://docusaurus.io/docs#comparison-with-other-tools) 在 Docusaurus 的说明文档可以看到。

#### 2.2.2. 如何用 Docusaurus 建站

Docusaurus 建站比较简单，按照[教程](https://docusaurus.io/docs#fast-track)，几分钟就可以弄好。

1. 新建网站，输入以下命令。命令执行完成后，电脑上会多出一个名字为 `my-website` 的文件夹。

```js
npx create-docusaurus@latest my-website classic //my-website 改成自己网站的名字
```

2. 开启网站，进入网站文件夹目录下，开启本地预览网址。

```js
cd my-website //进入 my-website 目录下
npx docusaurus start //本地预览网站，执行该命令后，用浏览器打开 http://localhost:3000 这个地址，可以预览网站
```

3. 修改 `docusaurus.config.js` 文件里的配置。

```js title="/docusaurus.config.js"
const config = {
  // highlight-start
  title: '简疏志', //博客名字
  tagline: '常精进，勿懈怠', //博客标语
  url: 'https://jianshuzhi.me', //改成自己的域名
  baseUrl: '/',
  //...
  favicon: 'img/favicon.ico',
  organizationName: 'anattaguo', // 更改为自己的名字或者 github 的用户名.
  projectName: 'jianshuzhi', // 改成这个项目的名字，可以写 github 上的仓库名字
  // highlight-end

  presets: [
    [
      'classic',
      /** @type {import('@docusaurus/preset-classic').Options} */
      ({
        // highlight-next-line
        docs: false, //如果不想保留 docs 的功能就设置为 false; 如果想保留文档的功能就删除这一行
        docs: {
          //...
          // highlight-next-line
          editUrl: 'https://github.com/facebook/docusaurus/tree/main/packages/create-docusaurus/templates/shared/', // 删除这一行，这是某个页面下的‘编辑本页面'功能
        },
        blog: {
          routeBasePath: '/', // 将博客设置为网站的根页面
          blogTitle: '简疏志',
        },
        //...
      }),
    ],
  ],

  themeConfig:
   //...
    ({
      navbar: {
        //highlight-start
        title: '简疏志', // 导航条左上角的名字
        logo: {
          alt: 'My Site Logo',
          src: 'img/logo.png', // 导航条左上角的 logo
        },
        items: [
          {to: '/', label: '博客', position: 'left'},
        // highlight-end
          //...

        ],
      },
        // highlight-next-line
        copyright: `Copyright © ${new Date().getFullYear()} 简疏志 Wrote by Mengjun Guo Built with Docusaurus.`, // 页脚底部声明设置
      },
    }),
};

module.exports = config;
```

4. 删除或者将文件重命名 `./src/pages/index.js`，这样就可以删除 landing page，也就是说，一打开网站看到的就是博客样式。

完成以上步骤，一个博客的基本配置算是完成，在配置过程中可以通过 http://localhost:3000 实时预览。

如果想修改博客主题配色，在 `/src/css/custom.css` 文件里修改。可以先通过 Docusaurus 提供的[配色测试工具](https://docusaurus.io/docs/next/styling-layout#styling-your-site-with-infima) 预览配色，然后复制颜色代码到 `/src/css/custom.css` 里。

所有博文放在 `/blog` 文件下，博文撰写时需要注意的格式，可以查阅 [Docusaurs 关于博客的说明](https://docusaurus.io/docs/next/blog#adding-posts)。

## 3. 将本地网站推送到 Github

在 Github 上新建一个仓库，然后根据提示将在本地搭建好的网站推送到 Github 上。

## 4. 部署网站

一开始选择的是 [Netlify](https://www.netlify.com/) 来部署自己的网站，发现国内访问基本上打不开。于是换成了 [Vercel](https://vercel.com/) 进行部署，而且 Vercel 还会自动帮忙弄好 https 的问题。部署步骤比较简单，Vercel 会有提示步骤：

1. 将个人 Github 账号和 Vercel 进行关联
2. 选择个人博客的仓库进行部署

部署完成后，需要将[购买的域名](#buy-domain)和 Vercel 进行绑定：

1. 进入 Vercel 的 **Settings > Domains** (设置 > 域名)
2. 选择 add domain (添加域名)
3. 输入购买的域名
4. 记住 DNS 和 CNAME，示例如下

| Type  | Name | Value                |
| ----- | ---- | -------------------- |
| A     | @    | 70.70.01.01          |
| CNAME | www  | cname.vercel-dns.com |

5. 将 Vercel 上的 DNS 和 CNAME 更新到 GoDaddy **我的域名 > 其他设置 > 管理 DNS** 上。

大功告成！不过实测加载有些慢，后续有时间再[优化国内访问速度](https://yqc.im/vercel-unable-access-to-the-solution-in-china/)。

---

参考文章：

1. [零成本搭建现代博客指南](https://www.bmpi.dev/series/%e9%9b%b6%e6%88%90%e6%9c%ac%e6%90%ad%e5%bb%ba%e7%8e%b0%e4%bb%a3%e5%8d%9a%e5%ae%a2%e6%8c%87%e5%8d%97)
2. [Vercel 国内无法访问解决方案](https://yqc.im/vercel-unable-access-to-the-solution-in-china/)
3. [Docusaurus 官方文档](https://docusaurus.io/docs)
4. [我的配色选择工具](https://htmlcolorcodes.com/colors/)
