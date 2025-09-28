# Yandex 搜索爬虫

[![Promo](https://media.brightdata.com/2025/08/SERP-API-50-off-GitHub-banner_1389_166.png)](https://www.bright.cn/products/serp-api/yandex-search)

本仓库提供两种从 Yandex 搜索结果页（SERP）提取数据的可靠方案：

- 免费版 Yandex 爬虫：适用于小规模的 Yandex 搜索结果抓取
- 企业级 Yandex SERP API：面向高并发、实时数据提取的可扩展生产级方案（隶属 [Bright Data 的 SERP Scraper API](https://www.bright.cn/products/serp-api)）

## 目录
- [免费 Yandex SERP 爬虫](#免费-yandex-serp-爬虫)
  - [环境要求](#环境要求)
  - [快速开始指南](#快速开始指南)
  - [示例输出](#示例输出)
  - [限制](#限制)
- [Yandex SERP 爬虫 API](#yandex-serp-爬虫-api)
  - [关键优势](#关键优势)
  - [开始使用](#开始使用)
- [接入方式](#接入方式)
  - [直接 API 访问](#直接-api-访问)
  - [原生代理访问](#原生代理访问)
- [Yandex 搜索查询参数](#yandex-搜索查询参数)
  - [本地化](#本地化)
  - [分页](#分页)
  - [时间范围](#时间范围)
  - [设备定向](#设备定向)
- [实践示例](#实践示例)
- [支持与资源](#支持与资源)

## 免费 Yandex SERP 爬虫

该免费爬虫可用于小规模收集 Yandex SERP 数据。非常适合需要少量数据的开发者用于个人项目、研究或测试。

<img width="800" alt="free-yandex-serp-scraper" src="https://github.com/bright-cn/yandex-api/blob/main/images/428371413-775c71f6-10cf-4a2d-91b8-6f137db5b171.png" />

### 环境要求

- [Python 3.9+](https://www.python.org/downloads/)
- 依赖包：
  - 用于浏览器自动化的 `playwright`
  - 用于 HTML 解析的 `BeautifulSoup`

```bash
pip install playwright beautifulsoup4
playwright install
```

> 刚接触网络爬取？请查看我们的[Python 爬虫新手指南](https://www.bright.cn/blog/how-tos/web-scraping-with-python)。
>

### 快速开始指南

1. 打开 [yandex-search-results-scraper.py](https://github.com/bright-cn/yandex-api/blob/main/yandex-serp-scraper/yandex-serp-scraper.py)
2. 自定义搜索词与每个词的抓取页数：

```python
PAGES_PER_TERM = {
    "ergonomic office chair": 2,
}
```

3. 运行脚本

### 示例输出
<img width="800" alt="yandex-scraper-output" src="https://github.com/bright-cn/yandex-api/blob/main/images/428371812-dbd6f456-af64-4a4a-8735-f26876ae5fa8.png" />

### 限制
抓取 Yandex 的主要难点之一是其严格的验证码（CAPTCHA）防护：

<img width="800" alt="yandex-captcha-challenge" src="https://github.com/bright-cn/yandex-api/blob/main/images/428371880-309e645f-c043-4231-aeb2-c3417e91b15e.png" />

Yandex 使用严格且不断演进的反爬系统以阻止自动化数据提取。频繁触发验证码会迅速导致 IP 被封，使得长时间、稳定运行的爬虫变得困难。

虽然免费爬虫能完成基础任务，但存在以下重要限制：

- IP 封禁风险高
- 请求量有限
- 验证码频繁打断
- 不适合生产环境

若需可扩展且稳定的方案，请参考下方的 Bright Data 专用 API。👇

## Yandex SERP 爬虫 API

[Yandex 搜索 API](https://www.bright.cn/products/serp-api/yandex-search) 隶属 Bright Data 的 [SERP Scraping API](https://www.bright.cn/products/serp-api) 套件。它利用业内领先的[代理基础设施](https://www.bright.cn/proxy-types)，仅需一次 API 调用即可获取实时的 Yandex 搜索结果。

### 关键优势

- 全球精确度：可针对全球任意位置定制结果
- 按成功付费：仅为成功请求付费
- 实时数据：秒级获取最新结果
- 无限扩展性：轻松应对高并发、大流量
- 成本高效：无需自建昂贵基础设施
- 性能可靠：内置防封锁技术
- 7×24 专家支持：随时获得技术协助

📌 先试后买：在我们的 SERP API 在线演示中免费试用

<img width="800" alt="bright-data-serp-api-playground" src="https://github.com/bright-cn/yandex-api/blob/main/images/428391143-c089343e-50a8-4961-8d11-d312982480df.png" />

### 开始使用

1. 注册 [Bright Data 账号](https://www.bright.cn/)（新用户赠送 $5 额度）
2. 生成你的 [API 密钥](https://docs.brightdata.com/general/account/api-token)
3. 按照我们的[分步指南](https://github.com/bright-cn/yandex-api/blob/main/setup-serp-api-guide.md)配置 SERP API

## 接入方式

### 直接 API 访问

最简单的方式是直接向 Bright Data 的 API 端点发起请求。

cURL 示例：

```bash
curl https://api.brightdata.com/request \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer API_TOKEN" \
  -d '{
        "zone": "ZONE_NAME",
        "url": "https://www.yandex.com/search/?text=apple+watch+series+10+review&lr=95&lang=en",
        "format": "raw"
      }'
```

Python 示例：

```python
import requests
import json

url = "https://api.brightdata.com/request"

headers = {"Content-Type": "application/json", "Authorization": "Bearer API_TOKEN"}

payload = {
    "zone": "ZONE_NAME",
    "url": "https://www.yandex.com/search/?text=apple+watch+series+10+review&lr=95&lang=en",
    "format": "raw",
}

response = requests.post(url, headers=headers, json=payload)

with open("yandex-scraper-api-result.html", "w", encoding="utf-8") as file:
    file.write(response.text)

print("Response saved!")
```

### 原生代理访问

此方式使用代理路由直接访问搜索结果。

cURL 示例：

```bash
curl -i \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<CUSTOMER_ID>-zone-<ZONE_NAME>:<ZONE_PASSWORD> \
  -k \
  "https://www.yandex.com/search/?text=apple+watch+series+10+review&lr=95&lang=en"
```

Python 示例：

```python
import requests
import urllib3

urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)

host = "brd.superproxy.io"
port = 33335
username = "brd-customer-<customer_id>-zone-<zone_name>"
password = "<zone_password>"
proxy_url = f"http://{username}:{password}@{host}:{port}"

proxies = {"http": proxy_url, "https": proxy_url}

url = "https://www.yandex.com/search/?text=apple+watch+series+10+review&lr=95&lang=en"
response = requests.get(url, proxies=proxies, verify=False)

with open("yandex-scraper-api-result.html", "w", encoding="utf-8") as file:
    file.write(response.text)

print("Response saved!")
```

> 注意：使用原生代理方式时，生产环境建议安装 Bright Data 的 SSL 证书。详见我们的 [SSL 证书指南](https://docs.brightdata.com/general/account/ssl-certificate)。
>

👉 查看[完整 HTML 输出](https://github.com/bright-cn/yandex-api/blob/main/yandex-scraper-api-output/yandex-scraper-api-result.html)

*诸如 `lr` 与 `lang` 的查询参数说明见下一节。*

## Yandex 搜索查询参数

### 本地化

#### 区域（`lr`）

该参数用于指定搜索结果所针对的地理区域或国家。

| 区域 | 代码 |
| --- | --- |
| Moscow | 1 |
| Saint-Petersburg | 2 |
| USA | 84 |
| Canada | 95 |
| China | 134 |

示例——查看 “best wireless earbuds” 在美国的排名：

```bash
curl --proxy brd.superproxy.io:33335 \
     --proxy-user brd-customer-<id>-zone-<zone>:<password> \
     "https://www.yandex.com/search/?text=best+wireless+earbuds&lr=84"
```

#### 语言（`lang`）

使用两位语言代码设置语言偏好：

- `lang=en` - 英语
- `lang=es` - 西班牙语
- `lang=fr` - 法语

示例——获取西班牙语的体育新闻：

```bash
https://www.yandex.com/search/?text=local+sports+news&lang=es
```

### 分页

#### 页码（`p`）

控制展示第几页的结果：

- `p=0` - 第一页（默认）
- `p=1` - 第二页
- `p=4` - 第五页

Yandex 的每个 SERP 页面通常返回 10 条结果。

示例——抓取 “nike running shoes” 的第 3 页（第 21–30 条）：

```bash
https://www.yandex.com/search/?text=nike+running+shoes&p=2
```

### 时间范围

#### 时间周期（`within`）

将结果限定在指定时间范围内：

- `within=77` - 最近 24 小时
- `within=1` - 最近 2 周
- `within=[%pm]` - 最近 1 个月

示例——获取最近 24 小时内的 “iPhone 15 review” 结果：

```bash
https://www.yandex.com/search/?text=iphone+15+review&within=77
```

### 设备定向

#### 设备类型（`brd_mobile`）

指定要模拟的设备类型：

- 省略或 `brd_mobile=0` - 随机桌面端 UA
- `brd_mobile=1` - 随机移动端 UA
- `brd_mobile=ios` 或 `brd_mobile=iphone` - iPhone UA
- `brd_mobile=ipad` 或 `brd_mobile=ios_tablet` - iPad UA
- `brd_mobile=android` - 安卓手机 UA
- `brd_mobile=android_tablet` - 安卓平板 UA

示例——模拟 iPhone 进行响应式网站测试搜索：

```bash
https://www.yandex.com/search/?text=responsive+website+testing&brd_mobile=ios
```

#### 浏览器类型（`brd_browser`）

定义要模拟的浏览器：

- 省略（默认） - 随机浏览器
- `brd_browser=chrome` - Google Chrome
- `brd_browser=safari` - Safari
- `brd_browser=firefox` - Mozilla Firefox

示例——模拟 Safari 搜索 Python 教程：

```bash
https://www.yandex.com/search/?text=how+to+learn+python&brd_browser=safari
```

> 注意：请勿将 `brd_browser=firefox` 与 `brd_mobile=1` 组合使用，它们不兼容。
>

## 实践示例

为实现更精细的目标投放，你可以组合多个参数：

```bash
https://www.yandex.com/search/?text=organic+skincare+products
&lr=95
&lang=en
&p=2
&within=1
&brd_mobile=ios
&brd_browser=safari
```

此搜索将：
- 定位到加拿大用户（`lr=95`）
- 显示英文结果（`lang=en`）
- 展示第二页（`p=2`）
- 限定在过去两周（`within=1`）
- 模拟 iPhone 用户（`brd_mobile=ios`）
- 使用 Safari 浏览器（`brd_browser=safari`）

非常适合护肤品牌调研加拿大市场中 iOS 移动用户对有机产品的近期趋势。

## 支持与资源

- 文档：[SERP API 文档](https://docs.brightdata.com/scraping-automation/serp-api/)
- 相关 API：
  - [SERP API](https://github.com/bright-cn/serp-api)
  - [Google 搜索 API](https://github.com/bright-cn/google-search-api)
  - [Google 新闻爬虫](https://github.com/bright-cn/Google-News-Scraper)
  - [Google 趋势 API](https://github.com/bright-cn/google-trends-api)
  - [Google 评论 API](https://github.com/bright-cn/google-reviews-api)
  - [Google 酒店 API](https://github.com/bright-cn/google-hotels-api)
  - [Google 航班 API](https://github.com/bright-cn/google-flights-api)
  - [Web Unlocker API](https://github.com/bright-cn/web-unlocker-api)
- 使用场景：
  - [SEO 与 SERP 监测](https://www.bright.cn/use-cases/serp-tracking)
  - [旅游行业数据](https://www.bright.cn/use-cases/travel)
- 延伸阅读：[最佳 SERP API 盘点](https://www.bright.cn/blog/web-data/best-serp-apis)
- 联系技术支持：[support@brightdata.com](mailto:support@brightdata.com)
