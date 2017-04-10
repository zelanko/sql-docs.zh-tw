---
title: "關於 SQL Server 中 JSON 的常見問題集 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "07/07/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "JSON、常見問題集"
ms.assetid: feae120b-55cc-4601-a811-278ef1c551f9
caps.latest.revision: 9
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 9
---
# 關於 SQL Server 中 JSON 的常見問題集
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 在此處尋找關於 SQL Server 中內建 JSON 支援的一些常見問題解答。  
 
## FOR JSON 和 JSON 輸出

### FOR JSON PATH 或 FOR JSON AUTO？  
 **問：** 我需要透過單一資料表上的簡易 SQL 查詢，建立 JSON 文字結果。 FOR JSON PATH 與 FOR JSON AUTO 產生相同的輸出。 我該使用哪一個選項？  
  
 **答：** 使用 FOR JSON PATH。 JSON 輸出並無任何差異，但 AUTO 模式具備某些額外邏輯，其會檢查是否應將資料行執行巢狀處理。 請考慮使用 PATH 做為預設選項。  

### 建立巢狀的 JSON 結構  
 **問：** 我需要在相同層級產生具有數個陣列的複雜 JSON。 FOR JSON PATH 可使用路徑建立巢狀物件，而 FOR JSON AUTO 會針對每個資料表建立額外巢狀層級。 這兩個選項皆無法產生我想要的輸出。 如何建立現有選項未直接支援的自訂 JSON 格式？  
  
 **答：** 您可新增 FOR JSON 查詢做為資料行運算式傳回 JSON 文字，以建立任何資料結構，或是使用 JSON_QUERY 函數手動建立 JSON，如下列範例所示。  
  
```tsql  
SELECT col1, col2, col3,  
             (SELECT col11, col12, col13 FROM t11 WHERE t11.FK = t1.PK FOR JSON PATH) as t11,  
             (SELECT col21, col22, col23 FROM t21 WHERE t21.FK = t1.PK FOR JSON PATH) as t21,  
             (SELECT col31, col32, col33 FROM t31 WHERE t31.FK = t1.PK FOR JSON PATH) as t31,  
             JSON_QUERY('{"'+col4'":"'+col5+'"}' as t41  
FROM t1  
FOR JSON PATH  
```  
  
資料行運算式中的所有 FOR JSON 查詢或 JSON_QUERY 函數結果，皆會格式化為個別的巢狀 JSON 子物件並包含於主要結果。  

### 避免在 FOR JSON 輸出中產生雙逸出 JSON  
 **問：** 我已將 JSON 文字儲存於資料表資料行。 我想要將其包含在 FOR JSON 輸出中。 FOR JSON 會逸出 JSON 中的所有字元，因此我會收到 JSON 字串而非巢狀物件，如下列範例所示。  
  
```tsql  
SELECT 'Text' as myText, '{"day":23}' as myJson  
FOR JSON PATH  
```  
  
 此查詢會產生下列輸出。  
  
```json  
[{"myText":"Text","myJson":"{\"day\":23}"}]  
```  
  
 如何防止此行為？ 我想讓 `{"day":23}` 以 JSON 物件形式傳回而非逸出的文字。  
  
 **答：** 儲存於文字資料行的 JSON 或常值，其處理方式與任何文字相似。 其會以雙引號括住並逸出。 若您想要傳回未逸出的 JSON 物件，則必須將此資料行以引數形式傳送至 JSON_QUERY 函數，如下列範例所示。  
  
```tsql  
SELECT col1, col2, col3, JSON_QUERY(jsoncol1) AS jsoncol1  
FROM tab1  
FOR JSON PATH  
```  
  
 JSON_QUERY 若無選用的第二參數，則僅會傳回第一個引數做為結果。 由於 JSON_QUERY 會傳回有效的 JSON，因此 FOR JSON 知道此結果無須逸出。

### 使用 WITHOUT_ARRAY_WRAPPER 子句產生的 JSON，會在 FOR JSON 輸出中逸出  
 **問：** 我嘗試使用 FOR JSON 和 WITHOUT_ARRAY_WRAPPER 選項，格式化資料行運算式。  
  
```tsql  
SELECT 'Text' as myText,  
       (SELECT 12 day, 8 mon FOR JSON PATH, WITHOUT_ARRAY_WRAPPER) as myJson  
FOR JSON PATH   
```  
  
 FOR JSON 查詢傳回的文字似乎會逸出為純文字。 僅在指定 WITHOUT_ARRAY_WRAPPER 時才會發生此情況。 為何不會將它視為 JSON 物件，並將它以未逸出方式包含在結果中？  
  
 **答：** 若您指定 WITHOUT_ARRAY_WRAPPER 選項，則產生的 JSON 文字不一定有效。 因此，外部 FOR JSON 會假定此為純文字並逸出字串。 若您確定 JSON 輸出有效，請使用 JSON_QUERY 函數將其包裝以升級為正確格式的 JSON，如下列範例所示。  
  
```tsql  
SELECT 'Text' as myText,  
      JSON_QUERY((SELECT 12 day, 8 mon FOR JSON PATH, WITHOUT_ARRAY_WRAPPER)) as myJson  
FOR JSON PATH    
```  

## OPENJSON 和 JSON 輸入

### 使用 OPENJSON 從 JSON 文字傳回巢狀 JSON 子物件  
 **問：** 無法使用具明確結構描述的 OPENJSON，開啟包含純量值、物件和陣列的複雜 JSON 物件陣列。 參考 WITH 子句中的索引鍵時，僅會傳回純量值。 物件和陣列會以 Null 值形式傳回。 如何擷取 JSON 物件中的物件或陣列？  
  
 **答：** 若您想要傳回物件或陣列作為資料行，請在資料行定義中使用 AS JSON 選項，如下列範例所示。  
  
```tsql  
SELECT scalar1, scalar2, obj1, obj2, arr1  
FROM OPENJSON(@json)  
             WITH ( scalar1 int,  
                          scalar2 datetime2,  
                          obj1 NVARCHAR(MAX) AS JSON,  
                          obj2 NVARCHAR(MAX) AS JSON,  
                          arr1 NVARCHAR(MAX) AS JSON)  
```  

### 請使用 OPENJSON 傳回長文字值，不要用 JSON_VALUE。  
 **問：** 在包含長文字的 JSON 文字當中具有描述索引鍵。 `JSON_VALUE(@json, '$.description')` 傳回 NULL 而非值。  
  
 **答：** JSON_VALUE 設計為傳回小純量值。 函數通常會傳回 NULL 而非溢位錯誤。 若您想要傳回整數值，請使用支援 NVARCHAR(MAX) 值的 OPENJSON，如下列範例所示。  
  
```tsql  
SELECT myText FROM OPENJSON(@json) WITH (myText NVARCHAR(MAX) '$.description')  
```  

### 請使用 OPENJSON 處理重複的索引鍵，不要用 JSON_VALUE。  
 **問：** 在 JSON 文字中具有重複的索引鍵。 JSON_VALUE 僅傳回在路徑上找到的第一個索引鍵。 如何傳回所有具相同名稱的索引鍵？  
  
 **答：** JSON 內建純量函數僅會傳回第一次出現的參考物件。 若您需要多個索引鍵，請使用 OPENJSON 資料表值函式，如下列範例所示。  
  
```tsql  
SELECT value FROM OPENJSON(@json, '$.info.settings')  
WHERE [key] = 'color'  
```  

### OPENJSON 需要相容性層級 130  
 **問：** 嘗試在 SQL Server 2016 中執行 OPENJSON，結果收到下列錯誤。  
  
 `Msg 208, Level 16, State 1 ‘Invalid object name OPENJSON’`  
  
 **答：** OPENJSON 函式僅適用於相容性等級 130。 若您的資料庫相容性等級低於 130，則會隱藏 OPENJSON。 其他 JSON 函數適用於所有的相容性層級。  
 
## 其他問題

### 在 JSON 文字中包含非英數字元的參考索引鍵  
 **問：** 在 JSON 文字的索引鍵中具有非英數字元。 如何參考這些屬性？  
  
 **答：** 您必須在 JSON 路徑中使用引號將其括住。 例如，`JSON_VALUE(@json, '$."$info"."First Name".value')`。
 