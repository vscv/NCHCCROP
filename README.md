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
現在單機切圖很方便，以下為MacBookPro單機切圖範例：((在mount google的雲端硬碟上執行可能拖慢了速度))

清一下暫存
▶ rm tiles/*

▶ identify taoyuan_airport.tif_2.tif
 taoyuan_airport.tif_2.tif TIFF 7629x6993 7629x6993+0+0 8-bit sRGB 152.635MiB 0.010u 0:00.006
 
▶ time magick taoyuan_airport.tif_2.tif -crop 2000x2000 tiles/tiles%03d.jpg
 ===============
 CPU    328%
 User    6.029
 System    1.897
 Total    2.415
 
 ▶ time magick taoyuan_airport.tif_2.tif -crop 500x500 tiles/tiles%03d.jpg
 ===============
 CPU    140%
 User    3.541
 System    1.084
 Total    3.286
 
 
 ▶ identify Taipei2tif.tif
Taipei2tif.tif TIFF 13343x15752 13343x15752+0+0 8-bit sRGB 601.327MiB 0.030u 0:00.028

▶ time magick Taipei2tif.tif -crop 1000x1000 tiles/tiles%03d.jpg
 ===============
 CPU    260%
 User    22.540
 System    7.132
 Total    11.383

 ▶ ls -l tiles | wc -l
     225
     
▶ time magick Taipei2tif.tif -crop 200x200 tiles/tiles%03d.jpg
===============
CPU	26%
User	14.571
System	3.618
Total	1:08.55 (?)

▶ ls -l tiles | wc -l
    5294

▶ identify PIA23405.tif
PIA23405.tif TIFF 15950x6500 15950x6500+0+0 8-bit sRGB 170.014MiB 0.000u 0:00.008 

▶ time magick PIA23405.tif -crop 1024x1024 tiles/tiles%03d.jpg
===============
CPU    157%
User    9.587
System    3.319
Total    8.201

▶ ls -l tiles | wc -l                                         
     113

