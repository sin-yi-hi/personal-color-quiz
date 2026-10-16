# Color Muse — Personal Color Quiz

用 20 題探索個人色彩，提供四季、12 型／16 型結果與日常搭配靈感。

正式網站：[https://sin-yi-hi.github.io/personal-color-quiz/](https://sin-yi-hi.github.io/personal-color-quiz/)

GitHub Pages 已於 2026-10-16 發布成功，並完成公開網址的完整操作驗收。

## 開始使用

直接在瀏覽器開啟 `index.html` 即可。網站完整整合 HTML、CSS、JavaScript 與 Canvas，不需要安裝套件、啟動伺服器、後端、資料庫或 API。沒有外部圖片、字型或程式依賴，離線也能操作。

## 已完成功能

- 首頁、測驗說明、20 題互動測驗、計算狀態與結果頁。
- 新手觀察模式：14 題色卡比較、2 題外觀觀察、3 題滑桿與 1 題四組配色情境。
- 每題提供「現在做／看哪裡」；多數題目不需回想過往穿搭經驗。
- 可選用自己的照片做本機並排比色；彩度與明度滑桿會即時改變預覽色框。
- 區分「比較過、兩邊差不多」與「不確定」，不強迫初學者猜測。
- 未作答不能進下一題；滑桿須拖動或確認中間值才算作答。
- 上一題保留選擇；結果頁可回去修改答案。
- 依最後的答案重新計算冷暖、明度、彩度，沒有累計重複加分。
- 四季相對接近度、12 型、16 型、判定解釋與三維度視覺化。
- 6 色代表色票；穿搭、中性色、慎用色、彩妝、髮色與金屬建議。
- 1200 × 1600 PNG 圖卡下載，包含分類、6 色色票、四季分數與穿搭色彩。
- 下載後附圖片預覽與儲存連結，可供手機長按儲存。
- 重新測驗會清除答案及結果，回到測驗說明。
- 支援桌機、平板與手機；手機色卡改為單欄。

## 本測驗的分類規則

這是為本專案設計的透明、可重現的探索演算法，沒有宣稱經過專業診斷驗證。

1. 每個選項帶有 `[Temperature, Value, Chroma]` 權重，正向分別為暖、淺、亮，負向為冷、深、柔。
2. 中間值為有效觀察，分數為 0；「不確定」不提供分數，也不納入該題正規化上限。
3. 每個維度以有效題目的最大可能權重正規化到 −1～1。
4. 與四個季節的參考向量比較加權距離，換算成總和為 100% 的相對接近度。這些數字不是診斷機率。
5. 四季選定後，以最突出、符合該季節的特徵挑選細分類；三項強度差距小於 0.18 時，16 型為 True。
6. 12 型中的 True 合併了 16 型的 Warm／Cool 與 True。例如：12 型 True Autumn，可對應 16 型 Warm Autumn 或 True Autumn。
7. 有效觀察少於 4 題、缺少任一維度線索，或三個維度都接近中間（絕對值小於 0.12）時，結果會顯示「尚待探索」，不強行指定季型與專屬建議。

不同個人色彩系統的名稱與邊界可能不同。完整題目、權重與分類資料都可直接在 `index.html` 的 `QUESTIONS`、`SEASONS`、`SUBTYPES` 與 `analyze()` 中檢視及修改。

## GitHub Pages

目標 Repository：`sin-yi-hi/personal-color-quiz`。

1. 將 `index.html` 放在 `main` 分支根目錄。
2. Repository → **Settings → Pages**。
3. **Build and deployment → Source** 選 **Deploy from a branch**。
4. Branch 選 **main**，資料夾選 **/ (root)**，按 **Save**。
5. 等 GitHub 的 Pages 建置完成，再開啟 `https://sin-yi-hi.github.io/personal-color-quiz/`。

此專案已從 main 根目錄發布成功。後續更新 index.html 並推送 main 後，GitHub Pages 會重新建置；建置後應再檢查完整測驗、上一題修改、下載、重新測驗及手機顯示。

設定步驟參考 [GitHub Pages 官方文件](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)。

## 隱私與限制

- 不需要登入、不傳送答案、不使用追蹤程式或持久儲存。
- 照片為選用功能：使用者自行選擇 JPG／PNG／WebP（10 MB 以下），僅以本機 Blob 和 Canvas 顯示，不上傳、不自動辨識、不加入下載圖卡。
- 照片可隨時移除，重新測驗或重新整理會清除。載入或移除照片不會更動既有答案。
- 螢幕色框只提供視覺對照，不能模擬實際布料對膚色的反光；也可不放照片，改以鏡子與相近顏色的衣物觀察。
- 答案只存在目前頁面的記憶體，重新整理或關閉後不會保留。
- 不確定或特徵接近時，會顯示提示與其他季型的相對接近度。
- 螢幕、照明與主觀感受會影響色彩判斷；請以實物搭配作參考。
- 本作品僅供趣味與自我探索，不作為專業 Personal Color 診斷。

## 開發與驗證

開發日期：2026-10-16（Asia/Taipei）。規格整理見 `SPEC.md`，實測修正紀錄見 `CHANGELOG.md`。

網站執行本身僅需要 `index.html`；其他 Markdown 文件與預覽圖片都是說明素材，不是網站的執行依賴。
