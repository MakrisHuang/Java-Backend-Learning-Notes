# Restful

#### 設計要點
* 注意版本號，新的API是否要兼容舊的
* 每一次request時要送出多少資料、訊息碼

#### 小記
* 可用``Pageable``回傳指定數量的物件
* 用``@JsonProperty``建立物件來解析request body