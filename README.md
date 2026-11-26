[README.md](https://github.com/user-attachments/files/35454571/README.md)
# Python 個人理財網站

用 Python、Flask 和 SQLite 製作的個人理財網站，可在本機記錄現金及台股持倉，並查看資產分布。可以先從履歷上的[靜態展示頁](https://snow-bo.github.io/Resume/python-personal-finance/)瀏覽畫面。

## 功能

- 新增台幣、美金現金紀錄，並刪除單筆現金紀錄。
- 新增台股買入資料，記錄股數、成交價、手續費和交易稅。
- 依美元兌台幣匯率換算現金總額，依最近收盤價計算持倉市值、平均成本和報酬率。
- 以圓餅圖顯示股票庫存占比，以及台幣、美金與股票的資產占比。

## 開發架構

假設你在「現金庫存表單」新增一筆台幣 1,000 元，這筆資料會這樣走。

1. 你在瀏覽器填好金額，再按「提交表單」。
2. Flask 收到金額。`index.py` 把這筆紀錄存進 SQLite 的 `datafile.db`，然後帶你回首頁。
3. 首頁從資料庫重新讀取現金紀錄，算出加上這筆紀錄後的現金總額。匯率和股票收盤價則是由程式向外部服務查詢。
4. Jinja2 把算好的金額和紀錄填進首頁的 HTML。程式也會用 Matplotlib 畫出資產比例圖。

## 使用技術

- **Python** 是撰寫後端程式的語言。
- **Flask** 處理瀏覽器的請求，例如開啟首頁或接收表單。
- **SQLite** 保存現金和股票紀錄。Python 透過內建的 `sqlite3` 讀寫 `datafile.db`。
- **HTML、Jinja2、Bootstrap** 分別負責網頁內容、把後端資料放進網頁，以及表格和按鈕的樣式。
- **Requests** 讓 Python 查詢匯率和台股收盤價。
- **Matplotlib** 把計算結果畫成圓餅圖。

## 專案結構

```text
python-personal-finance/
├─ index.py          Flask 路由、資產計算、外部 API 與繪圖
├─ db_setting.py     建立 SQLite 資料庫和資料表
├─ templates/
│  ├─ base.html      共用版型與導覽
│  ├─ index.html     資產總覽
│  ├─ cash.html      現金表單
│  └─ stock.html     股票表單
├─ static/           本機圖表輸出目錄
└─ datafile.db       首次初始化後在本機產生
```

## 下載與本機啟動

1. 在 [GitHub 儲存庫](https://github.com/Snow-Bo/python-personal-finance)按綠色 **Code → Download ZIP**，或[直接下載 ZIP](https://github.com/Snow-Bo/python-personal-finance/archive/refs/heads/main.zip)。
2. 解壓縮後，用 VS Code 開啟包含 `index.py` 的資料夾，並在那個資料夾開啟終端機。請先安裝 Python 3。
3. 安裝專案用到的套件。

   ```powershell
   python -m pip install flask requests matplotlib
   ```

4. 如果專案資料夾裡還沒有 `static`，先建立它，讓程式可以存放圖表。

   ```powershell
   mkdir static
   ```

5. 第一次執行、尚未有 `datafile.db` 時，建立空的資料庫。

   ```powershell
   python db_setting.py
   ```

6. 啟動 Flask，然後用瀏覽器開啟[本機理財網站](http://127.0.0.1:5000/)。

   ```powershell
   python index.py
   ```

## 操作方式

1. 從首頁上方點「現金庫存表單」，輸入金額、備註和日期後提交。
2. 點「股票庫存表單」，輸入股票代號、股數、買入價及費用後提交。
3. 回首頁查看現金、股票庫存與資產比例。現金紀錄可以從首頁刪除。

首頁會連線查詢匯率，有股票庫存時也會查詢臺灣證券交易所的收盤價。`datafile.db` 會儲存這台電腦的紀錄，重新啟動程式後仍可以讀取。
