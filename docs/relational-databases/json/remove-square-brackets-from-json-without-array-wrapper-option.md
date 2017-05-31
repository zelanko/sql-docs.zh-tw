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
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ea60d5a74c680e9c2aba571a76815f77913da471
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="remove-square-brackets-from-json---withoutarraywrapper-option"></a>從 JSON 輸出移除方括弧 - WITHOUT_ARRAY_WRAPPER 選項
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  若要移除預設圍住 **FOR JSON** 子句之 JSON 輸出的方括弧，請指定 **WITHOUT_ARRAY_WRAPPER** 選項。 使用此選項以產生單一 JSON 物件作為輸出，而不是陣列。  
  
 如果您未指定此選項，JSON 輸出以方括號括住。  
  
## <a name="examples"></a>範例  
 下列範例顯示使用或不使用 **WITHOUT_ARRAY_WRAPPER** 選項的 **FOR JSON** 子句輸出。  
  
 **查詢**  
  
```tsql  
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
  
 不使用**結果** without the **結果**   
  
```json  
[{
    "year": 2015,
    "month": 12,
    "day": 15
}]
```  
  
 以下是使用 **FOR JSON** 選項的 **WITHOUT_ARRAY_WRAPPER** 選項。  
  
 **查詢**  
  
```tsql  
SELECT TOP 1 SalesOrderNumber, OrderDate, Status  
FROM Sales.SalesOrderHeader  
ORDER BY ModifiedDate  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER 
```  
  
 使用**結果** with the **結果**   
  
```json  
{
    "SalesOrderNumber": "SO43660",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
} 
```  
  
 不使用**結果** without the **結果**   
  
```json  
[{
    "SalesOrderNumber": "SO43660",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}]
```  
  
## <a name="see-also"></a>另請參閱  
 [FOR 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
  
  

