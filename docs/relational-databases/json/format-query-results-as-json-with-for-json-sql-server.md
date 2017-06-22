---
title: "使用 FOR JSON 將查詢結果格式化為 JSON (SQL Server) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 01/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR JSON
- JSON, exporting
- exporting JSON
ms.assetid: 15b56365-58c2-496c-9d4b-aa2600eab09a
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 06095384c6f6ec876e0d103186b1269d19056987
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="format-query-results-as-json-with-for-json-sql-server"></a>使用 FOR JSON 將查詢結果格式化為 JSON (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

將 **FOR JSON** 子句新增至 **SELECT** 陳述式，以將查詢結果格式化為 JSON，或將 SQL Server 中的資料匯出為 JSON。 使用**FOR JSON**子句，以簡化用戶端應用程式的用戶端應用程式的 JSON 輸出格式設定委派給[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。
  
 當您使用 **FOR JSON** 子句，您可以明確指定輸出的架構，或讓 SELECT 陳述式的架構決定輸出。  
  
-   使用**FOR JSON PATH**維護的 JSON 輸出格式的完整控制權。 您可以建立包裝函式物件和巢狀複雜屬性。  
  
-   使用**FOR JSON AUTO**格式化 JSON 輸出會自動根據 SELECT 陳述式的結構。  
  
以下是含 **FOR JSON** 子句的 **SELECT** 陳述式範例和其輸出。
  
 ![FOR JSON](../../relational-databases/json/media/jsonslides2forjson.png "FOR JSON")  
  
## <a name="maintain-control-over-json-output-with-for-json-path"></a>保有控制權 FOR JSON PATH 使用 JSON 輸出
在 **PATH** 模式中，您可以使用點語法 (例如 `'Item.Price'` ) 來格式化巢狀的輸出。  

以下是使用 **PATH** 模式搭配 **FOR JSON** 子句的範例。 下列範例也會使用 **ROOT** 選項來指定具名根項目。 
  
 ![FOR JSON 輸出流程圖表](../../relational-databases/json/media/forjson-example1.png "FOR JSON 輸出流程圖表")  

### <a name="more-info"></a>其他資訊
如需詳細資訊和範例，請參閱[使用 PATH 模式 &#40; 格式化巢狀 JSON 輸出SQL Server &#41;](../../relational-databases/json/format-nested-json-output-with-path-mode-sql-server.md).

如需語法和使用方式，請參閱 [FOR 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)。  

## <a name="let-the-select-statement-control-json-output-with-for-json-auto"></a>讓 SELECT 陳述式控制使用 FOR JSON AUTO JSON 輸出
在 **AUTO** 模式中，SELECT 陳述式的結構決定 JSON 輸出的格式。 根據預設， **null** 值不會包含在輸出中。 您可以使用 **INCLUDE_NULL_VALUES** 來變更此行為。  

以下是使用 **AUTO** 模式搭配 **FOR JSON** 子句的範例查詢。
 
**查詢：**  
  
```sql  
SELECT name, surname  
FROM emp  
FOR JSON AUTO  
```  
  
 **結果**  
  
```json  
[{
    "name": "John"
}, {
    "name": "Jane",
    "surname": "Doe"
}]
```  
### <a name="more-info"></a>其他資訊
如需詳細資訊和範例，請參閱[自動格式化 JSON 輸出使用 AUTO 模式 &#40;SQL Server &#41;](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md).

如需語法和使用方式，請參閱 [FOR 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)。  
  
## <a name="control-other-json-output-options"></a>控制其他 JSON 輸出選項  
控制的輸出**FOR JSON**子句使用下列其他選項。  
  
-   **根**。 若要將單一最上層元素新增至 JSON 輸出，請指定 **ROOT** 選項。 如果您未指定此選項，JSON 輸出就沒有根項目。 如需詳細資訊，請參閱 [將根節點與根選項加入至 JSON 輸出 &#40;SQL Server&#41;](../../relational-databases/json/add-a-root-node-to-json-output-with-the-root-option-sql-server.md)。  
  
-   **INCLUDE_NULL_VALUES**。 若要在 JSON 輸出中包含 Null 值，請指定 **INCLUDE_NULL_VALUES** 選項。 如果您未指定此選項，輸出就不在查詢結果中包含 NULL 值的 JSON 屬性。 如需詳細資訊，請參閱[使用 INCLUDE_NULL_VALUES 選項 &#40; JSON 輸出中包含 Null 值SQL Server &#41;](../../relational-databases/json/include-null-values-in-json-include-null-values-option.md).   

-   **WITHOUT_ARRAY_WRAPPER**。 若要移除預設圍住 **FOR JSON** 子句之 JSON 輸出的方括弧，請指定 **WITHOUT_ARRAY_WRAPPER** 選項。 使用此選項以產生單一 JSON 物件做為從單一資料列結果的輸出。 如果您未指定此選項，JSON 輸出格式化為陣列-也就是以方括弧括住。 如需詳細資訊，請參閱 [使用 WITHOUT_ARRAY_WRAPPER 選項從 JSON 輸出移除方括弧 &#40;SQL Server&#41;](../../relational-databases/json/remove-square-brackets-from-json-without-array-wrapper-option.md)。 
   
## <a name="output-of-the-for-json-clause"></a>FOR JSON 子句的輸出  
 **FOR JSON** 子句的輸出具有下列特性。  
  
1.  結果集包含單一資料行。
    -   小型結果集會包含單一資料列。
    -   大型結果集分割很長的 JSON 字串，跨多個資料列。
        -   根據預設，SQL Server Management Studio (SSMS) 將串連結果為單一資料列之輸出的設定時**以方格顯示結果**。 SSMS 的 [狀態] 列會顯示實際資料列計數。
        -   其他用戶端應用程式可能需要串連長的結果結合多個資料列內容的程式碼。 如需這個程式碼的 C# 應用程式的範例，請參閱[C# 用戶端應用程式中的使用 FOR JSON 輸出](https://docs.microsoft.com/en-us/sql/relational-databases/json/use-for-json-output-in-sql-server-and-in-client-apps-sql-server#use-for-json-output-in-a-c-client-app)。
  
     ![FOR JSON 輸出範例](../../relational-databases/json/media/forjson-example2.png "FOR JSON 輸出範例")  
  
2.  結果會格式化為 JSON 物件陣列。  
  
    -   JSON 陣列中的元素數目等於資料列數目在 SELECT 陳述式的結果 （FOR JSON 子句會套用之前）。 
  
    -   在 SELECT 陳述式 （在 FOR JSON 子句會套用） 的結果中的每個資料列會成為陣列中個別的 JSON 物件。  
  
    -   （之前子句套用適用於 JSON) 的 SELECT 陳述式的結果中每個資料行會成為 JSON 物件的屬性。  
  
3.  資料行名稱與其值會根據 JSON 語法逸出。 如需詳細資訊，請參閱 [FOR JSON 如何逸出特殊字元和控制字元 &#40;SQL Server&#41;](../../relational-databases/json/how-for-json-escapes-special-characters-and-control-characters-sql-server.md)。
  
### <a name="example"></a>範例
以下是範例，示範如何**FOR JSON**子句格式化 JSON 輸出。  
  
**查詢結果**  
  
|||||  
|-|-|-|-|  
|**A**|**B**|**C**|**D**|  
|10|11|12|X|  
|20|21|22|Y|  
|30|31|32|Z|  
  
 **JSON 輸出**  
  
```json  
[{
    "A": 10,
    "B": 11,
    "C": 12,
    "D": "X"
}, {
    "A": 20,
    "B": 21,
    "C": 22,
    "D": "Y"
}, {
    "A": 30,
    "B": 31,
    "C": 32,
    "D": "Z"
}] 
```  
 如需您在 **FOR JSON** 子句輸出中所看到之項目的詳細資訊，請參閱下列主題。  
-   [FOR JSON 如何將 SQL Server 資料類型轉換為 JSON 資料類型 &#40;SQL Server&#41;](../../relational-databases/json/how-for-json-converts-sql-server-data-types-to-json-data-types-sql-server.md)  
**FOR JSON** 子句使用本主題中描述的規則，在 JSON 輸出中將 SQL 資料類型轉換為 JSON 類型。  

-   [FOR JSON 如何逸出特殊字元和控制字元 &#40;SQL Server&#41;](../../relational-databases/json/how-for-json-escapes-special-characters-and-control-characters-sql-server.md)  
 **FOR JSON** 子句會逸出特殊字元，並在 JSON 輸出中代表控制字元，如本主題中所描述。  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>深入了解內建 JSON 支援 SQL Server 中  
針對特定的解決方案，大量使用案例和建議，請參閱[有關內建 JSON 支援的部落格文章](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)Microsoft 經理專案 jovan popovic 的 Azure SQL Database 和 SQL Server 中。
  
## <a name="see-also"></a>另請參閱  
 [FOR 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)   
 [在 SQL Server 和用戶端應用程式中使用 FOR JSON 輸出 &#40;SQL Server&#41;](../../relational-databases/json/use-for-json-output-in-sql-server-and-in-client-apps-sql-server.md)  
  
  

