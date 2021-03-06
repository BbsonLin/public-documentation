token 管理
===============================================================================


token 與登入者身份之間的關連
-------------------------------------------------------------------------------

每個人皆有一個獨一無二的 token，這個 token 可以拿來做身份驗證。

使用者未登入的狀況下可將 header 設成 Authorization: Token <personal_token>

如果 token 正確，伺服器會將這次的連線當成是 **該 token 對應的使用者** 發送的。

由於 token 可被拿來作身分驗證，必須要注意 **絕對不要讓別人知道你個人的 token** ，若有被盜用的疑慮則需要重設 token。

.. hint::

    ticket 系統上附件的下載網址通常會長得像以下形式：

    https://dev-rx.ho600.com/download_attachment/32733/

    使用者成功登入且擁有瀏覽該附件的權限的話，則會直接重導向到該附件真正的下載網址，這類網址會長的像以下這樣：

    #.  AWS 檔案儲存空間

        https://dev-sr-ticket2.s3.amazonaws.com/media/private_uploaded_files/YANX/FANW/IRDP/leopard-leopard-spots-animal-wild-39857.jpeg?AWSAccessKeyId=AKIAIV2WIS2GLO3XSNTA&Signature=LezqUYT8LczjoF%2Fk9Mkbi9%2BQcB0%3D&Expires=1550218302

    #.  GOOGLE 檔案儲存空間

        https://commondatastorage.googleapis.com/dev-sr-associate-ticket/ticket-attachments/00/00/00/36/00/09/20190215080431.904598/antler-antler-carrier-fallow-deer-hirsch.jpg


    使用者未登入的話，https://dev-rx.ho600.com/download_attachment/32733/ 會將使用者導向登入頁，\
    登入過後會直接重導向到該附件真正的下載網址。

    當在 trask.com 提供給使用者 ticket 系統上附件的下載網址時，\
    比較好的做法是，要在 trask.com 開發一個網頁，像是: https://trask.com/download.php ，\
    對 trask 使用者來說，他／她看到的檔案網址是 https://trask.com/download.php?file_id=32733 。\
    當他／她點擊 https://trask.com/download.php?file_id=32733 後， download.php \
    內的程式碼會先判斷使用者是否登入、有沒有權限有下載、檔案紀錄存不存在、…等，\
    確認可下載後，在 download.php 中要去讀取 https://dev-rx.ho600.com/download_attachment/32733/ ，
    並得到 ticket 系統所回傳的 AWS S3 或 Google Cloud Storage 網址(如: https://dev-sr-ticket2.s3.amazonaws.com/media/private_uploaded_files/YANX/FANW/IRDP/leopard-leopard-spots-animal-wild-39857.jpeg?AWSAccessKeyId=AKIAIV2WIS2GLO3XSNTA&Signature=LezqUYT8LczjoF%2Fk9Mkbi9%2BQcB0%3D&Expires=1550218302 \
    或 \
    https://commondatastorage.googleapis.com/dev-sr-associate-ticket/ticket-attachments/00/00/00/36/00/09/20190215080431.904598/antler-antler-carrier-fallow-deer-hirsch.jpg ) 。\
    最後把這個附件真正存放的網址回傳給告訴使用者，讓使用者直接到 AWS S3 或 GCS 下載。\
    **絕對不能夠提供給使用者任何含有 token 的 ticket 網址** 。

如何取得個人 token
-------------------------------------------------------------------------------

1.  到頂端工具列選取 _開發人員選項_ 。

    .. figure:: token_management_1_1.png

#. 至 {管理 token} 區塊選擇 [複製] 即會把 token 複製到剪貼簿。

    .. figure:: token_management_1_2.png


如何更換個人 token
-------------------------------------------------------------------------------

1.  到頂端工具列選取 _開發人員選項_ 。

    .. figure:: token_management_2_1.png

#.  至 {管理 token} 區塊選擇 [重設] 。

    .. figure:: token_management_2_2.png

#.  此時跳出 +您確定要重設 token 嗎？ 舊的 token 將無法被使用 的 modal ，選擇 [重設] 即會產生新的一筆個人 token。

    .. figure:: token_management_2_3.png


