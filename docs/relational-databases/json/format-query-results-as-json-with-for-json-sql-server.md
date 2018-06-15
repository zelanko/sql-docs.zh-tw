---
title: 使用 FOR JSON 將查詢結果格式化為 JSON (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: json
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- FOR JSON
- JSON, exporting
- exporting JSON
ms.assetid: 15b56365-58c2-496c-9d4b-aa2600eab09a
caps.latest.revision: 31
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ad65f71c46a89f3758cb5102021843f96b3adf1e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32940793"
---
# <a name="format-query-results-as-json-with-for-json-sql-server"></a>使用 FOR JSON 將查詢結果格式化為 JSON (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

將 **FOR JSON** 子句新增至 **SELECT** 陳述式，以將查詢結果格式化為 JSON，或將 SQL Server 中的資料匯出為 JSON。 使用 **FOR JSON** 子句，將來自應用程式的 JSON 輸出格式設定委派給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，以簡化用戶端應用程式。
  
 當您使用 **FOR JSON** 子句時，您可以明確指定 JSON 輸出的結構，或讓 SELECT 陳述式的結構決定輸出。  
  
-   若要保有對 JSON 輸出格式的完整控制權，請使用 **FOR JSON PATH**。 您可以建立包裝函式物件和巢狀複雜屬性。  
  
-   若要根據 SELECT 陳述式的結構自動格式化 JSON 輸出，請使用 **FOR JSON AUTO**。  
  
以下是含 **FOR JSON** 子句的 **SELECT** 陳述式範例和其輸出。
  
 ![FOR JSON](../../relational-databases/json/media/jsonslides2forjson.png)
  
## <a name="option-1---you-control-output-with-for-json-path"></a>選項 1 - 使用 FOR JSON PATH 控制輸出
在 **PATH** 模式中，您可以使用點語法 (例如 `'Item.Price'` ) 來格式化巢狀的輸出。  

以下是使用 **PATH** 模式搭配 **FOR JSON** 子句的範例。 下列範例也會使用 **ROOT** 選項來指定具名根項目。 
  
 ![FOR JSON 輸出的流程圖表](../../relational-databases/json/media/forjson-example1.png) 

### <a name="more-info-about-for-json-path"></a>FOR JSON PATH 的詳細資訊
如需詳細資訊和範例，請參閱[以 PATH 模式格式化巢狀 JSON 輸出 &#40;SQL Server&#41;](../../relational-databases/json/format-nested-json-output-with-path-mode-sql-server.md)。

如需語法和使用方式，請參閱 [FOR 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)。  

## <a name="option-2---select-statement-controls-output-with-for-json-auto"></a>選項 2 - SELECT 陳述式使用 FOR JSON AUTO 控制輸出
在 **AUTO** 模式中，SELECT 陳述式的結構決定 JSON 輸出的格式。

根據預設， **null** 值不會包含在輸出中。 您可以使用 **INCLUDE_NULL_VALUES** 來變更此行為。  

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
 
### <a name="more-info-about-for-json-auto"></a>FOR JSON AUTO 的詳細資訊
如需詳細資訊和範例，請參閱[使用 AUTO 模式自動格式化 JSON 輸出 &#40;SQL Server&#41;](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md)。

如需語法和使用方式，請參閱 [FOR 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)。  
  
## <a name="control-other-json-output-options"></a>控制其他 JSON 輸出選項  
使用下列其他選項控制 **FOR JSON** 子句的輸出。  
  
-   **ROOT**。 若要將單一最上層元素新增至 JSON 輸出，請指定 **ROOT** 選項。 如果您未指定此選項，JSON 輸出就不會有根項目。 如需詳細資訊，請參閱 [將根節點與根選項加入至 JSON 輸出 &#40;SQL Server&#41;](../../relational-databases/json/add-a-root-node-to-json-output-with-the-root-option-sql-server.md)。  
  
-   **INCLUDE_NULL_VALUES**。 若要在 JSON 輸出中包含 Null 值，請指定 **INCLUDE_NULL_VALUES** 選項。 如果您未指定此選項，輸出就不會在查詢結果中包含 NULL 值的 JSON 屬性。 如需詳細資訊，請參閱[使用 INCLUDE_NULL_VALUES 選項在 JSON 輸出中包含 Null 值 &#40;SQL Server&#41;](../../relational-databases/json/include-null-values-in-json-include-null-values-option.md)。   

-   **WITHOUT_ARRAY_WRAPPER**。 若要移除預設圍住 **FOR JSON** 子句之 JSON 輸出的方括弧，請指定 **WITHOUT_ARRAY_WRAPPER** 選項。 使用此選項以產生單一 JSON 物件，作為來自單一資料列結果的輸出。 如果您未指定此選項，JSON 輸出就會格式化為陣列，也就是以方括弧括住。 如需詳細資訊，請參閱 [使用 WITHOUT_ARRAY_WRAPPER 選項從 JSON 輸出移除方括弧 &#40;SQL Server&#41;](../../relational-databases/json/remove-square-brackets-from-json-without-array-wrapper-option.md)。 
   
## <a name="output-of-the-for-json-clause"></a>FOR JSON 子句的輸出  
**FOR JSON** 子句的輸出具有下列特性：  
  
1.  結果集包含單一資料行。
    -   小型結果集會包含單一資料列。
    -   大型結果集跨多個資料列分割太長的 JSON 字串。
        -   根據預設，SQL Server Management Studio (SSMS) 會在輸出設定為 [以方格顯示結果] 時，將結果串連成單一資料列。 SSMS 的狀態列會顯示實際資料列計數。
        -   其他用戶端應用程式可能需要程式碼，藉由串連多個資料列的內容，來將較長的結果重新合併成有效的單一 JSON 字串。 如需這個程式碼在 C# 應用程式中的範例，請參閱[在 C# 用戶端應用程式中使用 FOR JSON 輸出](../../relational-databases/json/use-for-json-output-in-sql-server-and-in-client-apps-sql-server.md#use-for-json-output-in-a-c-client-app)。
  
     ![FOR JSON 輸出的範例](../../relational-databases/json/media/forjson-example2.png)  
  
2.  結果會格式化為 JSON 物件陣列。  
  
    -   JSON 陣列中的元素數目等於 SELECT 陳述式結果中的資料列數目 (在套用 FOR JSON 子句之前)。 
  
    -   SELECT 陳述式 (在套用 FOR JSON 子句之前) 結果中的每個資料列會成為陣列中的個別 JSON 物件。  
  
    -   SELECT 陳述式 (在套用 FOR JSON 子句之前) 結果中的每個資料行則會成為 JSON 物件的屬性。  
  
3.  資料行名稱與其值會根據 JSON 語法逸出。 如需詳細資訊，請參閱 [FOR JSON 如何逸出特殊字元和控制字元 &#40;SQL Server&#41;](../../relational-databases/json/how-for-json-escapes-special-characters-and-control-characters-sql-server.md)。
  
### <a name="example"></a>範例
以下是示範 **FOR JSON** 子句如何格式化 JSON 輸出的範例。  
  
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

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>深入了解 SQL Server 和 Azure SQL Database 中的 JSON  
  
### <a name="microsoft-blog-posts"></a>Microsoft 部落格文章  
  
如需特定的解決方案、使用案例和建議，請參閱這些[部落格文章](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)，了解 SQL Server 和 Azure SQL Database 中的內建 JSON 支援。  

### <a name="microsoft-videos"></a>Microsoft 影片

如需 SQL Server 和 Azure SQL Database 中內建 JSON 支援的觀看式簡介，請參閱下列影片：

-   [SQL Server 2016 和 JSON 支援](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [使用 SQL Server 2016 和 Azure SQL Database 中的 JSON](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL 與關聯式領域之間的橋樑 JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>另請參閱  
 [FOR 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)   
 [在 SQL Server 和用戶端應用程式中使用 FOR JSON 輸出 &#40;SQL Server&#41;](../../relational-databases/json/use-for-json-output-in-sql-server-and-in-client-apps-sql-server.md)  
  
  
