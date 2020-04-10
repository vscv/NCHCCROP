# NCHCCROP
A very old distributed image split/crop tool by Bash and ImageMagick.

## 前言
大約是在2007年對大型空照/衛照圖原始圖轉換成TSB or Google Map等可用的LoD多解析度小圖，利用12+1的電腦叢集將各切圖task藉由ssh分散到各節點中執行，檔案則放在master node的/shm(仿ram disk)中各節點可以同時access。

本專案
