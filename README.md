[README.md](https://github.com/user-attachments/files/35454334/README.md)
# Resume｜Snow 的個人履歷與作品集

這是我的個人履歷網站。在同一個網站可以查看我的學經歷、技能、結訓證書和網頁作品。

**[開啟線上履歷](https://snow-bo.github.io/Resume/)**

## 網站內容

- **關於 Snow**：個人介紹、學歷和經歷。學歷欄可開啟義守大學畢業證書與產業新尖兵結訓證書。
- **聯絡方式**：完整履歷、技能專長與聯絡資訊。
- **日本旅遊網站**：日本旅遊介紹與景點推薦。
- **圍棋網站**：圍棋的基本介紹與各地圍棋資訊。
- **Python 個人理財網站**：展示資產表格、圓餅圖、現金表單和股票表單。Flask 與 SQLite 的本機版放在[個人理財專案儲存庫](https://github.com/Snow-Bo/python-personal-finance)。

## 開發架構

打開首頁時，瀏覽器先讀取 `index.html`，再載入 `styles` 裡的樣式和程式。點導覽列上的日本旅遊、圍棋或理財作品，瀏覽器就會開啟對應資料夾裡的 HTML。證書也各有一頁，可以從學歷欄開啟。

## 使用技術

- **HTML** 放網頁內容，例如履歷表、導覽列和作品頁。
- **CSS、SCSS** 管理版面、顏色和字型。瀏覽器載入編譯好的 CSS。
- **JavaScript** 處理捲動時的導覽列陰影。
- **Bootstrap、Font Awesome** 提供部分排版、按鈕與圖示。
- **GitHub Pages** 發布網站，讓訪客可以用公開網址瀏覽。

## API 串接

[Python 個人理財完整版](https://github.com/Snow-Bo/python-personal-finance)使用 Flask 和 Requests 查詢兩個外部 API。查回來的資料會參與資產計算。

- **全球即時匯率 API** 取得美元兌台幣的匯率。程式把美金現金換算成台幣，再與台幣現金加總。
- **臺灣證券交易所 API** 依股票代號查詢最近可取得的收盤價。程式用收盤價乘上持有股數，計算持倉市值。

資料由 Flask 查詢與計算，履歷裡的靜態理財頁呈現匯出當時的結果。 [查看 API 串接程式](https://github.com/Snow-Bo/python-personal-finance/blob/main/index.py#L41)

## 主要檔案

| 檔案或資料夾 | 用途 |
| --- | --- |
| `index.html` | 網站首頁、個人介紹和作品導覽 |
| `contact.html` | 履歷詳細資訊與聯絡方式 |
| `certificates/` | 兩個證書頁和已遮蔽個資的圖片 |
| `styles/` | 首頁和履歷的樣式及 JavaScript |
| `img/`、`ICONS/` | 網站使用的圖片和圖示 |
| `japan/`、`Project of Go/` | 日本旅遊與圍棋作品 |
| `python-personal-finance/` | 個人理財的靜態展示 |

## 下載與使用

1. 在 [GitHub 儲存庫](https://github.com/Snow-Bo/Resume)點綠色 **Code → Download ZIP**，也可以[直接下載 ZIP](https://github.com/Snow-Bo/Resume/archive/refs/heads/main.zip)。
2. 解壓縮後，保留原本的資料夾結構。
3. 雙擊最外層的 `index.html`，用瀏覽器開啟首頁，再從導覽列開啟各個作品。

## 更新線上履歷

GitHub Pages 從 `main` 分支的最外層 `/(root)` 發布網站。修改頁面後，把新版檔案提交到 `main`，等 GitHub Pages 部署完成，就能在原本的網址看到更新。
