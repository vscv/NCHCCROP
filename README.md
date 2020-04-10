# NCHCCROP
A very very old distributed image split/crop practice using Bash and ImageMagick.

## 前言
大約是在2006~2007年間對大型空照/衛照圖原始圖轉換成TSB or Google Map等可用的LoD多解析度小圖需求下，利用12+1的電腦叢集(TDW, tiled display wall  cluster)將各切圖task藉由ssh分散到各節點中執行，檔案則放在master node的/shm(仿ram disk)中讓各節點可以同時access。本專案完全使用BASH語法，多數是在計算與處理一些切割檔案的尺寸變數而已，最後由ImageMagick的convert工具進行裁切。

## 注意
* 僅供回憶Bash語法使用
* 本專案只是撒12份出去(印象中...)，沒有再把各節點的thread再細分一次多工處理，且每一分都用迴圈重複crop分到的sub-image，因此效能還有待加強。
* 在需要做很多層LoD時效能比較好，如果只是單張大圖切一層，現在的PC/notebook的效能都會比分散式的好喔。
* 只限在已經設好ssh通行的環境(PC叢集一般沒問題都預設好ssh-key了)


==============================================
## 簡單做法
現在單機切圖很方便，以下為MacBookPro單機切圖範例：()
