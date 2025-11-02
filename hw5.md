# HW5 — UML 類別圖 / 循序圖 / 活動圖
**專題：AI 擬人化 3D 建模系統**

---

## 一、UML 類別圖 (Class Diagram)

說明：此類別圖為系統主要物件與其屬性/方法的概念性設計，利於呈現系統資料結構與責任分配。

```plantuml
@startuml ClassDiagram
' 定義類別
class User {
  - userId: String
  - username: String
  - email: String
  - passwordHash: String
  + login()
  + uploadImage(image)
  + previewModel(modelId)
  + saveModel(modelId)
  + shareModel(modelId, platform)
}

class Image {
  - imageId: String
  - ownerId: String
  - uri: String
  - metadata: Map
  + preprocess()
}

class ObjectRecognition {
  - modelVersion: String
  + recognize(image): RecognitionResult
}

class RecognitionResult {
  - label: String
  - confidence: float
  - bbox: Rectangle
}

class ModelGenerator {
  - generatorType: String
  + generate3D(result, styleOptions): ModelFile
}

class ModelFile {
  - modelId: String
  - format: String
  - uri: String
  - thumbnailUri: String
  + export(format)
}

class PreviewEngine {
  + renderModel(modelFile)
  + setPose(modelId, pose)
  + setExpression(modelId, expression)
}

class Storage {
  + save(modelFile)
  + load(modelId): ModelFile
  + saveImage(image)
}

class SocialAPI {
  + share(modelFile, platform)
}

' 關係
User "1" -- "0..*" Image
User "1" -- "0..*" ModelFile
Image --> ObjectRecognition : uses
ObjectRecognition --> RecognitionResult
RecognitionResult --> ModelGenerator : input
ModelGenerator --> ModelFile
ModelFile --> Storage : save/load
User --> PreviewEngine : uses
PreviewEngine --> ModelFile : render
User --> SocialAPI : uses
Storage ..> ModelFile : stores
@enduml
