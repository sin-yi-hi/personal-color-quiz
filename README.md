# Color Muse — Personal Color Quiz

用 20 題探索個人色彩，提供四季、12 型／16 型結果與日常搭配靈感。

正式網站：[https://sin-yi-hi.github.io/personal-color-quiz/](https://sin-yi-hi.github.io/personal-color-quiz/)

GitHub Pages 已於 2026-10-16 發布成功，並完成公開網址的完整操作驗收。

## 開始使用

網站核心整合在單一 `index.html`，不需要安裝套件、啟動後端、資料庫或推論 API。測驗、照片比色與結果下載可直接在瀏覽器使用；選用的「自動去背」會在第一次點擊時從 CDN 載入程式、WASM 與模型，因此此功能需要網路與支援的瀏覽器，建議從正式 HTTPS 網站使用。照片仍在本機處理，不傳送至外部服務。沒有使用去背時，不會載入這些工具。

## 已完成功能

- 首頁、測驗說明、20 題互動測驗、計算狀態與結果頁。
- 新手觀察模式：17 題色卡比較（含 3 題換序複核）與 3 題滑桿。
- 每題提供「現在做／看哪裡」；多數題目不需回想過往穿搭經驗。
- 可選用自己的照片做本機並排比色；冷暖、彩度與明度滑桿會即時改變預覽色框。
- 選用的本機去背與中性遮髮；可切回保留頭髮、原照。三種模式幾何尺寸相同，操作保留答案。
- Oklch 控制配對色票，單次只改主要測量屬性；暖冷為本站相對色相設計，非標準物理冷暖刻度。
- A／B 排序依維度交替並在每次新測驗隨機翻轉；換序複核與原題相反，前後返回保持排序。
- 可在並排比色與固定位置 A／B／中性灰切換之間選擇；預覽不會自動作答。
- 手機、平板與桌機皆保留照片比例，透明 PNG 會保留透明背景，不再補上白底。
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
3. 每個維度排除 3 題複核，以有效題目的最大可能權重正規化到 −1～1。
4. 與四個季節的參考向量比較三個維度等權重的平方距離，換算成總和為 100% 的相對接近度。這些數字不是診斷機率。
5. 四季選定後，以最突出、符合該季節的特徵挑選細分類；三項強度差距小於 0.18 時，16 型為 True。
6. 12 型中的 True 合併了 16 型的 Warm／Cool 與 True。例如：12 型 True Autumn，可對應 16 型 Warm Autumn 或 True Autumn。
7. 任一軸有效觀察少於 3 次、冷暖絕對值小於 0.2、明度和彩度都小於 0.2、第一二名差距小於 8 個百分點，或換序複核出現相反方向時，暫不分類。
8. 17 題計分、3 題複核。顯示各軸正向／負向／差不多／未判斷次數；複核不重複加分。沒有真人效度資料，門檻與 12／16 型映射都是網站規則。

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
- 照片為選用功能：使用者自行選擇 JPG／PNG／WebP（10 MB 以下），僅以本機 Blob 和 Canvas 顯示，不上傳、不辨識身分、不分析膚色、不加入下載圖卡。
- 自動去背僅在使用者點擊時載入 MediaPipe；模型在瀏覽器內分離人物與背景，沒有將照片、答案或遮罩傳至 CDN。首次需下載約 16 MB 模型及程式執行工具。
- 已透明的 PNG 可直接比色；若要遮髮，也可另外執行模型。遮髮將頭髮與衣服覆為中性灰，保留臉、頸部與配件；有色眼鏡或飾物建議拍照前取下。髮絲、耳環和複雜背景可能有殘留或誤刪，請用「還原原照」比對，必要時換背景較單純的頭肩近照。
- 照片可隨時移除，重新測驗或重新整理會清除。載入或移除照片不會更動既有答案。
- 螢幕色框只提供視覺對照，不能模擬實際布料對膚色的反光；也可不放照片，改以鏡子與相近顏色的衣物觀察。
- 答案只存在目前頁面的記憶體，重新整理或關閉後不會保留。
- 不確定或特徵接近時，會顯示提示與其他季型的相對接近度。
- 螢幕、照明與主觀感受會影響色彩判斷；請以實物搭配作參考。
- 本作品僅供趣味與自我探索，不作為專業 Personal Color 診斷。

## 開發與驗證

開發日期：2026-10-16（Asia/Taipei）。規格整理見 `SPEC.md`，實測修正紀錄見 `CHANGELOG.md`。

網站應用程式僅需 `index.html`；其他 Markdown 文件與預覽圖片是說明素材。選用的自動去背會額外載入以下固定版本資源：

- `@mediapipe/tasks-vision@0.10.32` 程式與 WASM：jsDelivr CDN。
- `SelfieMulticlass (256 × 256), float32/1` 模型：Google 官方模型儲存空間。
- 官方說明與模型類別：[MediaPipe Image Segmenter](https://developers.google.com/edge/mediapipe/solutions/vision/image_segmenter)、[Web 使用說明](https://developers.google.com/edge/mediapipe/solutions/vision/image_segmenter/web_js)。

去背功能用 [Google 官方公開示範圖片](https://developers.google.com/static/mediapipe/images/solutions/examples/image_segmentation.png) 驗證，僅作技術測試，不使用使用者個人照片。測試圖片不包含在網站 Repository 或 ZIP 中。

## 研究與修正

詳見 [RESEARCH.md](RESEARCH.md)：中、英、日、韓查核、證據限制、舊色票數值稽核、新版計分與待驗證事項。v4 通過 25,000 組演算法案例、3,000 組鏡像對稱比較與 sRGB 色票檢查；這些是軟體驗證，不是個人色彩診斷的真人準確率。
