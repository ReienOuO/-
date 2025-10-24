#小組作業4

flowchart LR
    User([使用者])
    System([物體3D人物模型轉換系統])
    DB[(模型資料庫)]
    LogDB[(使用者紀錄資料庫)]

    User -->|上傳圖片 / 選擇風格 / 操作請求| System
    System -->|回傳3D模型 / 錯誤提示 / 狀態訊息| User

    System -->|儲存模型資料| DB
    DB -->|讀取模型資料| System

    System -->|記錄使用者操作| LogDB
