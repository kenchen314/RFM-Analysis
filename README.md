🛒 顧客價值解密：利用 RFM 與 K-Means 演算法玩轉客群分群
「誰是我們的超級 VIP？誰又正悄悄流失？」

本專案透過經典的 RFM 模型 與 K-Means 非監督式機器學習，將交易數據轉化為具體的顧客畫像，協助行銷團隊告別「盲目群發」，實現精準行銷與資源最優化！

📌 專案亮點與核心特色
📊 指標量化 (RFM)：從交易紀錄提煉「最近消費 (R)」、「消費頻率 (F)」與「消費金額 (M)」。

⚖️ 特徵正規化：使用 MinMaxScaler 消除不同尺度的影響，讓模型訓練更客觀。

📐 科學定群 (Elbow Method)：透過手肘法繪製 WCSS 曲線，找出最佳分群數 k=4。

🎯 顧客貼標 (Labeling)：為數字群標賦予商業意義（High、Medium、Low、Missing）。

🎨 立體視覺化：繪製多維度成對散布圖（Pair Plot），並產出高解析度去背成果圖檔。

🛠️ 分析流程大公開
本專案依照標準資料科學流程進行，步驟清晰直觀：

[原始交易資料] ➔ [RFM 計算] ➔ [MinMaxScaler 正規化] ➔ [手肘法尋找最佳 K]
                                                                ↓
[成果 CSV / PNG 匯出] ⬅ [顧客畫像貼標] ⬅ [Pair Plot 視覺化] ⬅ [K-Means 分群 (k=4)]
1. 資料準備與指標檢視
載入彙總後的顧客 RFM 資料表（RFM_DATA.csv），欄位包含：

R (Recency)：離最近一次消費的天數（天數越少代表越活躍）。

F (Frequency)：累積購買次數。

M (Monetary)：累積消費總額。

2. 特徵尺度標準化
由於消費金額（M）動輒破萬，而購買頻率（F）僅數次到數十次，直接分群會使金額佔據過大權重。

我們使用 MinMaxScaler 將三項指標全部壓縮到 [0, 1] 區間，產生標準化資料表 nrfm。

3. 手肘法評估（Elbow Method）
計算 k=1∼10 的群內誤差平方和（WCSS / Inertia）：

k=1: 86.45

k=2: 29.86

k=3: 20.40

k=4: 14.33

k=5: 11.91

<img width="686" height="470" alt="下載" src="https://github.com/user-attachments/assets/146cc414-5e28-4012-b22f-b67c71bf47bc" />

觀察折線圖斜率趨緩的拐點，確認以 k=4 作為最佳分群數。

👥 四大顧客畫像與行銷對策
透過演算法將 732 位顧客精準分類，各群體的行為特徵如下：

群組代號	標籤名稱 (Group)	客戶數	平均購買頻率 (F)	平均消費金額 (M)	最近購買天數 (R)	建議行銷策略
Cluster 1	High	221	19.3 次	$45,268	17.7 天	主力優質客：穩定消費群，適合推薦新品與定期回購優惠。
Cluster 3	Medium	114	26.4 次	$76,632	15.3 天	頂級黃金 VIP：貢獻度最高的核心客群，提供專屬尊榮服務與封館特惠。
Cluster 2	Low	321	5.7 次	$14,127	44.5 天	潛力新客 / 低頻客：近期曾來訪，提供滿額折抵券以刺激二次購買。
Cluster 0	Missing	76	3.7 次	$8,570	182.7 天	沉睡 / 流失客：極久未回購，適合主打「好久不見」喚醒折扣或問卷調查。
📈 視覺化分析成果
藉由 Seaborn 繪製成對散布圖（Pair Plot），清楚呈現四個客群在三維空間中的分佈情形：

F vs M：呈現強烈正相關，VIP 客群集中在右上角高頻、高消費區。

R 軸分佈：Missing 客群在 R 軸出現明顯長尾高峰，清楚被模型孤立出來。

成果圖檔已儲存為透明背景高解析度圖檔：RFM_Pairplot.png。

<img width="2580" height="2301" alt="RFM_Pairplot" src="https://github.com/user-attachments/assets/d61a244c-8b20-44a5-a416-0f42e8ba13ed" />

📂 專案檔案結構
Plaintext
├── 練習檔.csv           # 原始交易明細資料
├── RFM_DATA.csv         # 整理後顧客 RFM 指標檔
├── RFM_result.csv       # 合併 Cluster 與 Group 標籤的最終交易檔
├── RFM_Pairplot.png     # 成對散布圖視覺化圖檔 (透明背景, 300 DPI)
├── rfm_analysis.ipynb   # 完整 Python / Jupyter 分析腳本
└── README.md            # 專案說明文件
🚀 快速上手 (Quick Start)
環境需求
Bash
pip install pandas numpy scikit-learn matplotlib seaborn
執行分析
下載專案資料夾並確認包含 練習檔.csv。

啟動 Jupyter Notebook / Google Colab 開啟分析腳本。

依序執行儲存格即可產出分群標籤與視覺化圖檔。
