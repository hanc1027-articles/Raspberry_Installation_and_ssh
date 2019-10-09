## 樹苺派灌系統及遠端ssh連線

### 安裝系統
- 假定已經買好了Raspberry pi 3、16GB以上的microSD卡、以及microUSB線
- 至官網下載映像檔：https://www.raspberrypi.org/downloads/raspbian/
- 下載Raspbian Buster with desktop (選擇zip)
- 解壓縮
- 灌開機系統至16GB的microSD卡(這邊以Mac為例)
    - 打開Mac的「終端機」，輸入:
    ```bash
    $ diskutil list #替查microSD卡硬碟位置，我的電腦是 /dev/disk2
    $ diskutil unmountdisk /dev/disk2 
    $ sudo dd if=[解壓縮的映像檔位置] of=[要燒錄的microSD卡位置，這邊為:/dev/disk2] bs=1m; sync #開始將開機映像檔燒錄至microSD，過程會有點久，它不會自己跑出進度條，可按 ctrl+T 查看進度。
    ```
- 燒錄完畢後，即可將microSD卡插入樹苺派，插上HDMI連接螢幕，插上鍵盤及滑鼠，開機
- 一開始會有一些簡單的設定，照做即可。重要的是，*設定的密碼一定要記住*，往後ssh遠端登入需要。
- 完成~
--- 
### ssh遠端登入
- 前面步驟完成後，應該可以看到類似平常看到的Windows或Mac亦或是其他Lunix系統顯示的樣子
- 打開樹苺派的「終端機」，輸入"
    ```bash
    $ ifconfig # 查詢此樹苺派的ip位置，先記起來。我的電腦因有先設定固定ip，查到的是 192.168.1.10
    ```
- 樹苺派關機
- 將microSD卡拔出，插到Mac電腦上，在microSD卡的根目錄新增一個名為「ssh」的檔案(無需副檔名，內容為空白)。因安全性關系，官方將ssh預設為關閉，所以需添加此檔案，讓它開機時，自動開啟22port。
- 完成後，將microSD卡插回樹苺派，插上RJ45的網路線(此時無需滑鼠、鍵盤)，開機
- 回到Mac的終端機上，輸入:
    ```bash
    $ ssh pi@192.168.1.10 # pi為它預設的帳號，後面為前步驟查到的ip位置
    ```
- 接著會需要輸入密碼，其為在圖形介面系統設定的密碼
- 完成ssh遠端登入