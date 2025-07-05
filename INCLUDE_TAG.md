`includeTags` 是 Firecrawl Simple 的 scrapeOptions 配置项之一，用于**指定只提取页面中哪些 HTML 标签的内容**。  
它的业务逻辑是：  
- 你可以传递一个字符串数组（如 `["main", "article", "section"]`），表示只保留这些标签内的内容，其它标签内容会被忽略。
- 这对于只想抓取页面主体、正文、特定结构内容时非常有用，可以过滤掉导航、页脚、广告等无关内容。

### 业务场景举例
- 只想抓取 `<main>`、`<article>` 里的内容，忽略 `<nav>`、`<footer>`、侧边栏等。
- 只提取 `<section>`、`<div class="content">` 里的数据，避免杂乱信息。

### 源码实现逻辑
在抓取和内容处理时，Firecrawl 会遍历页面 DOM，只保留 `includeTags` 指定的标签及其内容，其它标签会被过滤掉。  
如果 `includeTags` 为空或未设置，则默认抓取整个页面内容。

### 示例
```json
{
  "url": "https://example.com",
  "scrapeOptions": {
    "formats": ["markdown"],
    "includeTags": ["main", "article"]
  }
}
```
上例只会返回 `<main>` 和 `<article>` 标签内的内容。

如需进一步了解底层实现或有具体用法问题，欢迎继续提问！