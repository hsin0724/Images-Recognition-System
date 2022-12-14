# Images-Recognition-System

## Declaration - 聲明
此系統為與台灣公司之商業合作專案，故部分內容經過處理且無法公開完整程式碼。  
如想深入了解此系統，面試時可攜帶作品展示及操作此系統。

## Introduction - 專案簡介
此專案為從零開始開發的**影像自動標記系統**，系統主要包含 `選擇模組`、`訓練記錄`、`影像管理`、`標記影像`，`模型訓練`、`模型預測` 等功能，提供使用者依照不同的模組及參數進行影像訓練、測試、預測等功能。  

#### 系統前端  
依照客戶需求規劃系統介面，使用 Adobe Illustrator 、 Adobe XD 繪製系統 UI/UX 介面。
以 Angular 框架為主，搭配 Typescript、SCSS、Angular Material UI 套件等技能開發系統前端。

#### 系統後端  
以 Python 開發，並使用 Django（Python Web Framework）作為後端框架，後端與前端的串接使用 Django REST Framework。系統的影像辨識主程式使用 Python 裡的 Detectron2 library 撰寫，這是目前Mask-RCNN中較快速且準確度更高的模型。由於 Detectron2 是以 Pytorch ( Python 上的兩大深度學習系統之一) 為基礎開發的 library ，擴充度及自由度很高，便於之後對模組進行修改及調整。  

#### 資料庫 
以 PostgreSQL 資料庫進行資料儲存。  

#### 客戶端 
使用 Docker 將前端、後端、資料庫分別容器化並封裝起來，並自動安裝、部署好本軟體所需的所有背景程式和 Library，使軟體能快速在所有電腦上運行，同時也能控制各程式的版本避免錯誤。

![系統架構圖(新版)](https://user-images.githubusercontent.com/67618752/193440190-9803bee5-0556-4fac-b58a-7ffb34448cd2.jpg)


> 正在開發功能 :  
* 模型精準度製作柱狀圖表。
* 影像管理介面改成以分頁模式顯示照片。  
<br>
<br> 

## Function Demo - 功能展示
### 系統頁面 - 選擇模型   
此為系統打開後跳出的第一個頁面。主要供使用者進行選擇模型、建立新模型、編輯模型或刪除模型等操作。  
![model](https://user-images.githubusercontent.com/67618752/193448373-82db60b5-7843-4ec6-b3a2-5397944c3687.png)

**新建模型功能**  
輸入新模型資料按下【建立新模組】按鈕後新模型卡片將依照卡面順序顯示於畫面上。如未選擇模型照片自動帶入「預設照片」。  
![create_mpdel](https://user-images.githubusercontent.com/67618752/193448284-3f65d996-9239-49aa-aa98-c1970c27a0d6.gif)

**編輯模型功能**  
點選【編輯模型】鈕後所顯示的頁面。供使用者進行修改模型名稱、模型說明、模型圖片及刪除模組等功能。  
![edit_model](https://user-images.githubusercontent.com/67618752/193449340-1996a321-1324-4e19-bd8e-34d90196cf46.gif)
  
**刪除模型功能**  
選擇欲刪除的模型後按下【刪除模型】按鈕，系統將會跳出警告視窗確認使用者是否要刪除模型。刪除模型時需輸入「指定文字」才可刪除，指定文字輸入錯誤或未輸入指定文字皆會顯示錯誤提示。  
![delete_model](https://user-images.githubusercontent.com/67618752/193450194-97d568bf-a9a6-46ad-abe2-a0a15ce0edbf.gif)
<br>  
<br> 

### 系統頁面 - 訓練紀錄
於選擇模型頁面點擊【選擇模型】按鈕後所顯示的頁面。此頁面提供上一次使用該模型的訓練紀錄、訓練參數、及 Loss Rate 等結果，可作為之後訓練的參考。  ![record](https://user-images.githubusercontent.com/67618752/193452012-394ea2dd-59fb-485a-800e-d07b0771c5a4.gif)
<br>  
<br>  

### 系統頁面 - 影像標記
整合開源軟體 VGG Image Annotator (VIA) 圖像標記工具至前端畫面，此頁面可進行影像匯入、影像標記、匯入及輸出 coco / json 檔等功能。  
![Screenshot_235](https://user-images.githubusercontent.com/67618752/193452411-4a2a9791-73e3-4a39-a5a0-90814783beb2.png)
<br>  
<br>  

### 系統頁面 - 影像管理  
具備影像管理功能，可於此頁面新增照片、刪除照片、及新增 COCO 檔。使用者可透過切換 train / test / validation 三個分頁來查看資料夾內照片，且可分別上傳照片至不同分類，未標記過的照片會顯示「紅色外框」並顯示在最前方。  

**新增影像功能**  
於選取的分頁點選選【新增照片】按鈕可新增影像至該分頁裡。  
![add_image](https://user-images.githubusercontent.com/67618752/193452697-8766a346-99fd-4bc5-b81c-13d594435a32.gif)  

**刪除影像功能**  
點選【刪除照片】按鈕後會跳出【取消刪除】與【確定刪除】按鈕，勾選要刪除的照片(可複選)後點選確定刪除即可刪除照片。點選取消刪除將取消此次操作。  
![delete_image](https://user-images.githubusercontent.com/67618752/193452934-c0eca527-dbf5-4094-ac21-62c04ad62949.gif)

**新增COCO檔功能** 
點選【新增COCO檔】按鈕。在此頁面上傳的影像會直接被用在模型訓練當中，並自動生成訓練所需之 COCO 檔。  
![create_COCO](https://user-images.githubusercontent.com/67618752/193452534-7a51c241-0744-4350-97cd-6c32d475c348.gif)
<br>  
<br>  

### 系統頁面 - 模型訓練  
此為進行模型訓練及設定相關參數之頁面。選擇權重檔案後需等待出現「檔案上傳成功」的字樣，如未選擇權重檔案則自動使用「預設權重檔」。  
![model_training](https://user-images.githubusercontent.com/67618752/193454836-e577e8d1-217e-4be5-9f2e-56eb7459dec5.gif)

**參數進階設定**  
點選【進階設定】按鈕後，可設定相關參數預設值。點擊【還原預設】按鈕將出現警示，點擊確認後將會把所有訓練參數還原成「預設值」。  
![training_default](https://user-images.githubusercontent.com/67618752/193454877-53a0289e-effc-478e-83bd-fffd52024896.gif)

**模型訓練中**  
模型訓練中的頁面會顯示「預計剩餘時間」、「目前訓練代次 / 預計訓練代次」、相關參數及目前訓練進度條。會在每個 Iteration 都輸出 Training Loss 及 Validation Loss 讓使用者能及時觀測訓練效果。訓練結束後會對最終模型進行測試 (使用 test dataset)，等待測試結果的途中會顯示 「等待測試結果中…」，測試完成後將顯示 「訓練完成」，之後才可進入訓練結果頁面。  
![training_finish](https://user-images.githubusercontent.com/67618752/193454738-b734b71e-083e-404c-a318-74e70721ff64.gif)  

**終止訓練功能**  
若想提早中止預測可點擊 【終止訓練】按鈕，點選終止預測後會出現警告視窗詢問使用者是否確定終止，點選確定後將可進入預測結果頁面。  
![stop_training](https://user-images.githubusercontent.com/67618752/193457548-37ffa75f-0501-4dab-9783-b6e11816e9f5.gif)

**模型訓練結果**  
呈現此次訓練結果資料的頁面。下方圖表使用 APEXCHARTS 套件完成，將滑鼠游標移至圖表上方時會顯示詳細的 Loss 值，且可使用滑鼠框選圖表來放大檢視該區間資料。使用者可透過圖表右上角工具列將 Loss Rate 圖輸出為 SVG、PNG、或 CSV 格式並下載到電腦中。模型訓練完成後可進行「保存權重」功能，點擊【保存權重】按鈕後畫面上方會出現「儲存權重中...」提示，儲存成功後會出現「儲存完成」提示，使用者可至下載資料夾查看資料。  
![save_model_weight](https://user-images.githubusercontent.com/67618752/193463370-1e73c522-f92a-40a8-b863-f78c6c90a2ec.gif)
<br>  
<br>  

### 系統頁面 - 模型預測
此為進行模型預測及設定相關參數之頁面。在進行模型訓練前會先將模型預測鎖住，至少需進行一次的模型訓練才可進行模型預測，如未訓練過則出現無法進行模型預測之錯誤提示。  
![valid_alert](https://user-images.githubusercontent.com/67618752/193466004-beccd9b9-25a0-4720-8526-254c3ea75f3e.png)

進行模型預測前必須選擇「模型預測權重檔案」及預測「預測照片檔案」，否則【開始預測】按鈕會鎖住。兩者皆選擇檔案並出現 「檔案上傳成功」字樣後，才可點選【開始預測】。  
![valid_uploadFile](https://user-images.githubusercontent.com/67618752/193466136-ac05429e-3089-4691-96d9-07812bde7d59.gif)

**模型預測中**  
模型預測中的頁面會顯示「已完成預測的照片張數 / 總張數」及相關參數。若想提早中止預測可點擊 【終止預測】按鈕，點選終止預測後會出現警告視窗詢問使用者是否確定終止，點選確定後將可進入預測結果頁面。  
![validtion](https://user-images.githubusercontent.com/67618752/193464913-7360c654-e045-4dae-b388-a05c66dfa1de.gif)

**模型預測結果**  
模型預測結果頁面會顯示本次預測的模型資料、標記資料及預測圖片。預測結果照片清單可點選【展開】按鈕來顯示詳細結果。  
![valid_result](https://user-images.githubusercontent.com/67618752/193464790-4b5c1f11-7d8e-4a69-bbe1-823953e48320.gif)

想看得更精細時可點擊預測照片，之後將出現彈跳視窗並可於此視窗對照片進行放大 & 拖曳效果。  
![zoomin_image2](https://user-images.githubusercontent.com/67618752/193465548-773f5f9f-9676-41ad-81cc-a9aefbefc02d.gif)

**儲存預測結果**  
點選【儲存結果】按鈕可將預測結果照片及預測結果 csv 檔壓縮成 zip 檔儲存至下載資料夾。  
![save_result](https://user-images.githubusercontent.com/67618752/193464763-6f0c4c68-5915-4728-b1ce-3da930eada04.gif)

