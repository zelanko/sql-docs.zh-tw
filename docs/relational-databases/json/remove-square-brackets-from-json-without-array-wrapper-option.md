---
title: "從 JSON 輸出移除方括弧 - WITHOUT_ARRAY_WRAPPER 選項 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- WITHOUT_ARRAY_WRAPPER
ms.assetid: aa86c2d1-458e-465f-abfa-75470137d054
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 9045ebe77cf2f60fecad22672f3f055d8c5fdff2
ms.openlocfilehash: bf0d7645df22c9a7540650e3c7f2ca2d0db8e1cc
ms.contentlocale: zh-tw
ms.lasthandoff: 07/31/2017

---
# <a name="remove-square-brackets-from-json---withoutarraywrapper-option"></a>從 JSON 輸出移除方括弧 - WITHOUT_ARRAY_WRAPPER 選項
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

若要移除預設圍住 **FOR JSON** 子句之 JSON 輸出的方括弧，請指定 **WITHOUT_ARRAY_WRAPPER** 選項。 將此選項用於單一資料列結果，以產生單一 JSON 物件作為輸出，而不是內含單一元素的陣列。

如果您將此選項用於多個資料列結果，由於有多個元素且遺漏方括號，因此產生的輸出不是有效的 JSON。  
  
## <a name="example-single-row-result"></a>範例 (單一資料列結果)  
下列範例顯示使用或不使用 **WITHOUT_ARRAY_WRAPPER** 選項的 **FOR JSON** 子句輸出。  
  
 **查詢**  
  
```sql  
SELECT 2015 as year, 12 as month, 15 as day  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER 
```  

 使用**結果** with the **結果**   
  
```json  
{
    "year": 2015,
    "month": 12,
    "day": 15
} 
```  
  
 不使用 **WITHOUT_ARRAY_WRAPPER** 選項的**結果** (預設值)  
  
```json  
[{
    "year": 2015,
    "month": 12,
    "day": 15
}]
```  

## <a name="example-multiple-row-result"></a>範例 (多個資料列結果)
以下是使用 **FOR JSON** 選項的 **WITHOUT_ARRAY_WRAPPER** 選項。 這個範例會產生多個資料列結果。 由於有多個元素且遺漏方括號，因此輸出不是有效的 JSON。
  
 **查詢**  
  
```sql  
SELECT TOP 3 SalesOrderNumber, OrderDate, Status  
FROM Sales.SalesOrderHeader  
ORDER BY ModifiedDate  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER 
```  
  
 使用**結果** with the **結果**   
  
```json  
{
    "SalesOrderNumber": "SO43662",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}, {
    "SalesOrderNumber": "SO43661",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}, {
    "SalesOrderNumber": "SO43660",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
} 
```  
  
 不使用 **WITHOUT_ARRAY_WRAPPER** 選項的**結果** (預設值)  
  
```json  
[{
    "SalesOrderNumber": "SO43662",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}, {
    "SalesOrderNumber": "SO43661",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}, {
    "SalesOrderNumber": "SO43660",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}]
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>深入了解 SQL Server 中的內建 JSON 支援  
對於大量的特定解決方案、使用案例和建議，請參閱 SQL Server 和 Azure SQL Database 中 Microsoft 經理專案 Jovan Popovic 所撰寫的[有關內建 JSON 支援的部落格文章](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)。
  
## <a name="see-also"></a>另請參閱  
 [FOR 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
  
  

