**README.md**

```markdown
# Notion 出貨撿貨表轉換工具

一個免安裝、可直接在瀏覽器執行的 Notion CSV 轉 Excel 工具。

工具會將 Notion 匯出的出貨單 CSV 整理成商品分列的 Excel 撿貨表，並支援「順豐到付」與「順豐寄付」兩種格式。

所有資料都只在瀏覽器本機處理，不會上傳至任何伺服器。

## 功能

- 讀取 Notion 匯出的 CSV
- 支援點擊選擇或拖曳匯入 CSV
- 依照「商品資訊」中的換行拆分商品
- 每項商品獨立顯示在不同 Excel 列
- 自動從商品資訊擷取 `x1`、`x2`、`x3` 等數量
- 保留數量後方的商品備註
- 依原始 CSV 的出貨編號由小到大排序
- 排序時整筆訂單一起移動，避免收件人、商品、電話或地址錯置
- 支援「順豐到付」與「順豐寄付」兩種輸出格式
- 同人、加固、重量及尺寸依訂單範圍縱向合併
- 每筆訂單使用粗黑外框區隔
- 未合併的儲存格使用完整黑色細框線
- 出貨編號使用灰色底
- 所有 Excel 內容使用粗體
- 商品資訊中的 `[豎排]` 會將「豎排」兩字標示為紅色
- 直接輸出標準 `.xlsx`
- 輸出檔名沿用原始 CSV 檔名
- 不需要安裝套件或啟動伺服器
- 不使用外部 CDN 或網路資源

## 匯出格式

### 順豐到付

輸出以下 10 個欄位：

1. 出貨編號
2. 收件人
3. 同人
4. 加固
5. 商品資訊
6. 數量
7. 撿貨員
8. 打包員
9. 電話
10. 地址

### 順豐寄付

輸出以下 12 個欄位：

1. 出貨編號
2. 收件人
3. 同人
4. 加固
5. 商品資訊
6. 數量
7. 重量
8. 尺寸
9. 撿貨員
10. 打包員
11. 電話
12. 地址

重量與尺寸預設為空白，每筆訂單各保留一個合併儲存格，方便後續人工填寫。

## CSV 必要欄位

工具會依照欄位名稱讀取資料。原始 CSV 必須包含：

- `出貨編號`
- `收件人`
- `加固`
- `商品資訊`
- `電話`
- `地址`

其他欄位不會輸出到整理後的 Excel。

## 商品拆分範例

原始商品資訊：

```text
[旭儒][二刷][無立牌]江醫生他懷了死對頭的崽1-2(書籍) x1
[北美][預售][特簽版][第1-3集]這該死的求生欲(書籍) x2
```

整理後：

| 商品資訊 | 數量 |
|---|---:|
| `[旭儒][二刷][無立牌]江醫生他懷了死對頭的崽1-2(書籍)` | 1 |
| `[北美][預售][特簽版][第1-3集]這該死的求生欲(書籍)` | 2 |

如果商品結尾沒有可辨識的數量，工具會預設數量為 `1`，並在頁面上顯示「未辨識數量」統計。


範例
工具:
<img width="1020" height="671" alt="image" src="https://github.com/user-attachments/assets/ac4202f3-e3ef-46c8-a0d9-7a2f528f6285" />

整理前csv:
<img width="1494" height="1053" alt="image" src="https://github.com/user-attachments/assets/e790cdee-3b87-4d43-af4f-27b01c6d3e6c" />

整理後excel畫面：
<img width="2929" height="1510" alt="螢幕擷取畫面 2026-07-21 230405" src="https://github.com/user-attachments/assets/9232c237-07d9-449b-8ca7-f82f169d84f4" />


## 使用方式

1. 下載 `notion-shipping-tool.html`
2. 使用 Chrome、Edge、Firefox 或其他現代瀏覽器開啟
3. 選擇「順豐到付」或「順豐寄付」
4. 點擊上傳區選擇 Notion CSV，或將 CSV 拖入頁面
5. 確認預覽、訂單數及商品數
6. 點擊「下載 XLSX 出貨表」
7. 使用 Microsoft Excel 開啟下載的 `.xlsx`

## 線上使用

如果已啟用 GitHub Pages，可透過以下網址開啟：

```text
https://vthree.github.io/notion-shipping-tool/
```

> GitHub Pages 預設會尋找 `index.html`。如果儲存庫中只有 `notion-shipping-tool.html`，請將它複製或重新命名為 `index.html`，才能直接使用上方網址。

若保留原檔名，也可嘗試透過以下路徑開啟：

```text
https://vthree.github.io/notion-shipping-tool/notion-shipping-tool.html
```

## 本機資料與隱私

本工具是純前端單檔網頁：

- CSV 不會上傳到 GitHub
- CSV 不會上傳到任何伺服器
- 地址、電話及訂單內容只存在於目前瀏覽器分頁
- 關閉或重新整理頁面後，已匯入的資料不會被工具保存
- 產生 Excel 的工作全部在瀏覽器本機完成

請勿將包含客戶姓名、電話、地址或訂單內容的 CSV、XLSX 上傳到公開 GitHub 儲存庫。

## 支援格式

- UTF-8 CSV
- UTF-8 BOM CSV
- UTF-16LE BOM CSV
- Microsoft Excel `.xlsx`

CSV 支援：

- 雙引號欄位
- 欄位內逗號
- 欄位內換行
- 兩個雙引號代表一個雙引號

## 專案檔案

```text
notion-shipping-tool/
├─ notion-shipping-tool.html
├─ README.md
└─ .gitignore
```

若要使用 GitHub Pages，建議增加：

```text
index.html
```

`index.html` 的內容可以與 `notion-shipping-tool.html` 完全相同。

## 瀏覽器需求

建議使用最新版：

- Microsoft Edge
- Google Chrome
- Mozilla Firefox

舊版瀏覽器可能不支援 `TextDecoder`、`Blob`、拖曳上傳或其他必要的瀏覽器 API。

## 注意事項

- 出貨編號直接讀取原始 CSV，不會自行產生或重新編號
- 沒有出貨編號的訂單會排列在有編號的訂單後方
- 出貨編號相同時，會保留原始 CSV 順序
- 相同商品若在原始資料中出現多次，工具會保留多列
- 商品、收件人、電話及地址會以原始 CSV 的同一列綁定處理
- 請在下載後抽查幾筆訂單，確認原始 CSV 資料是否完整
- 請勿將客戶個人資料提交到公開儲存庫

## 授權

本專案僅供出貨單與撿貨表整理使用。

如需公開散布、商業使用或加入開源授權，可再新增 `LICENSE` 檔案。
```

**.gitignore**

```gitignore
# Customer and order data
*.csv
*.xlsx
*.xls
*.xlsm
*.xlsb
*.ods
*.numbers

# Exported archives
*.zip
*.7z
*.rar

# Temporary Office files
~$*.xlsx
~$*.xls
~$*.xlsm
*.tmp
*.temp

# Windows
Thumbs.db
Thumbs.db:encryptable
Desktop.ini
$RECYCLE.BIN/

# macOS
.DS_Store
.AppleDouble
.LSOverride
._*

# Linux
*~
.directory
.Trash-*

# Visual Studio Code
.vscode/
*.code-workspace

# JetBrains editors
.idea/
*.iml

# Vim
*.swp
*.swo
*.swn

# Node.js, if tooling is added later
node_modules/
npm-debug.log*
yarn-debug.log*
yarn-error.log*
pnpm-debug.log*

# Build and coverage output
dist/
build/
coverage/

# Local environment and secrets
.env
.env.*
!.env.example
*.pem
*.key
*.p12
*.pfx

# Local test and backup files
*.bak
*.backup
*.old
*.orig
```

手動上傳到 GitHub 時，儲存庫根目錄建議放置：

```text
notion-shipping-tool.html
README.md
.gitignore
```

如果要啟用 GitHub Pages，另外複製一份相同工具並命名為：

```text
index.html
```

請特別確認不要上傳任何包含客戶姓名、電話及地址的 `.csv` 或 `.xlsx`；上述 `.gitignore` 只會防止 Git 指令誤加入檔案，無法阻止你在 GitHub 網頁上手動上傳敏感資料。
