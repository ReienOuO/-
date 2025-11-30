erDiagram
    User ||--o{ GenerationRecord : 進行生成
    GenerationRecord ||--|{ InputImage : 基於
    GenerationRecord ||--|{ 3DModel : 產生

    User {
        int UserID PK
        string 帳號
        string 密碼
        datetime 註冊時間
    }

    GenerationRecord {
        int RecordID PK
        int UserID FK
        datetime 生成時間
        string 風格類別
        string 關鍵字
        string 辨識物體名稱
        float 辨識信心分數
    }
    
    InputImage {
        int ImageID PK
        int RecordID FK
        string 檔案路徑_URL
        datetime 上傳時間
    }
    
    3DModel {
        int ModelID PK
        int RecordID FK
        string 檔案路徑_URL
        string 檔案格式
        string 建模是否成功_Status
    }
