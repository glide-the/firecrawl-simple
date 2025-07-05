在 Firecrawl Simple 的 API 中，scrapeOptions 是用于配置 /v1/crawl 和 /v1/scrape 接口的参数之一。根据 README.md 的内容，scrapeOptions 至少支持如下配置项：

- formats：指定返回内容的格式，如 "markdown"、"html"。

不过，README.md 只展示了 formats 这个字段。为了更全面地回答你的问题，我会进一步查找源码，看看 scrapeOptions 还支持哪些配置项。

请稍等，我会为你查找 scrapeOptions 的完整配置选项。
Ran tool
Firecrawl Simple 中 scrapeOptions 支持的配置项如下（根据源码 apps/api/src/controllers/v1/types.ts）：

```ts
export const scrapeOptions = z
  .object({
    formats: z
      .enum(["markdown", "rawHtml", "screenshot"])
      .array()
      .optional()
      .default(["markdown", "rawHtml"]),
    headers: z.record(z.string(), z.string()).optional(),
    includeTags: z.string().array().optional(),
    excludeTags: z.string().array().optional(),
    timeout: z.number().int().positive().finite().safe().default(30000),
    waitFor: z.number().int().nonnegative().finite().safe().default(0),
    extract: extractOptions.optional(),
  })
  .strict(strictMessage);
```

### 详细配置项说明

- **formats**：数组，支持 `"markdown"`、`"rawHtml"`、`"screenshot"`，指定返回内容的格式。
- **headers**：对象，形如 `{ "User-Agent": "xxx" }`，自定义请求头。
- **includeTags**：数组，指定只提取哪些 HTML 标签内容。
- **excludeTags**：数组，指定要排除的 HTML 标签内容。
- **timeout**：数字，超时时间（毫秒），默认 30000。
- **waitFor**：数字，页面加载后等待的毫秒数，默认 0。
- **extract**：结构化抽取配置（高级用法，见 extractOptions，通常用于 schema 信息抽取）。
 