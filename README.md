# 香港公司查冊 MCP

透過 Model Context Protocol (MCP)，將你嘅 AI 助手駁去 [The Company Atlas](https://thecompanyatlas.com)，直接喺對話入面查香港公司註冊處嘅資料。

呢個 listing 專門用嚟：

- 查香港公司註冊處登記緊、仲生效嘅公司
- 用英文名或者中文名搵公司（例如「Swire」或者「太古」都得）
- 用商業登記號碼（BRN）睇公司資料：公司類別、註冊辦事處地址、成立日期同以前用過嘅名

MCP 連線由 The Company Atlas 提供，呢個 repo 本身唔會行另一個 server。

## 點樣連接

```
https://thecompanyatlas.com/mcp/hong-kong
```

喺 Claude、Cursor 或者任何支援 MCP 嘅 client 度，將呢條 URL 加做自訂連接器（custom connector），跟住提示用 Google 登入就得。

- 傳輸方式：Streamable HTTP
- 驗證：Google OAuth（登入一次，之後一直有效）
- 說明文件：[thecompanyatlas.com/tools/hong-kong-company-registry](https://thecompanyatlas.com/tools/hong-kong-company-registry)

## 工具

### `HongKong_search_companies`

用公司名同其他條件搵香港公司。所有條件係「同時符合」（AND），最少要填一個。

| 參數 | 類型 | 說明 |
|---|---|---|
| `q` | 字串，可選 | 公司名入面嘅字，英文或者中文都得，2 至 120 個字元。會同時對英文名同中文名 |
| `entityType` | 字串，可選 | 公司類別入面嘅字，例如 `guarantee`（擔保有限公司） |
| `address` | 字串，可選 | 註冊辦事處地址入面嘅字，例如 `Mong Kok` 或者 `旺角` |
| `incorporatedFrom` / `incorporatedTo` | 日期，可選 | 成立日期範圍（YYYY-MM-DD） |
| `page` / `limit` | 整數，可選 | 分頁，`limit` 最多 50（預設 20） |

有啲註冊非香港公司冇英文名，所以搜尋一定會連中文名一齊對。

### `HongKong_get_company`

用 8 位數字嘅商業登記號碼（例如 `35932210`，前面加唔加 `HK` 都得）睇一間公司嘅完整資料，包括以前用過嘅公司名。

## 試吓咁問

- 搵吓中文名有「銀行」嘅香港公司
- 2024 年之後喺旺角成立嘅擔保有限公司有邊啲？
- 幫我查吓商業登記號碼 35932210 係邊間公司

## 資料來源

香港公司註冊處嘅公司名冊（只包括仲生效嘅公司）。董事、股東同埋入咗檔嘅文件唔包括喺入面，要查呢啲請去[公司註冊處](https://www.cr.gov.hk/)。用之前，記得喺公司註冊處再核實一次。
