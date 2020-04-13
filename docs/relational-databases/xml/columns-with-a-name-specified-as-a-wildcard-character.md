---
title: 使用萬用字元指定資料行 (SQLXML) |Microsoft Docs
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns with
ms.assetid: d9551df1-5bb4-4c0b-880a-5bb049834884
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
ms.openlocfilehash: 0820b0d43c51dd7aeabf773f5f9809b7a8005d68
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664695"
---
# <a name="columns-with-a-name-specified-as-a-wildcard-character"></a>以萬用字元 (*) 指定名稱的資料行

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

如果以萬用字元 (\*) 指定資料行名稱，則插入該資料行內容的方式，就像是沒有指定資料行名稱一樣。 如果此資料行是非**xml** 類型的資料行，則會以文字節點插入資料行內容，如下列範例所示：  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT E.BusinessEntityID "@EmpID",   
       FirstName "*",   
       MiddleName "*",   
       LastName "*"  
FROM   HumanResources.Employee AS E  
  INNER JOIN Person.Person AS P  
    ON E.BusinessEntityID = P.BusinessEntityID  
WHERE E.BusinessEntityID=1  
FOR XML PATH;  
```  
  
 以下是結果：  

```xml
<row EmpID="1">KenJSánchez</row>
```

 如果此資料行是 **xml** 類型，就會插入對應的 XML 樹狀結構。 例如，下列查詢為資料行名稱指定 "*"，該資料行名稱包含 XQuery 針對 Instructions 資料行所傳回的 XML。  
  
```sql
SELECT   
       ProductModelID,  
       Name,  
       Instructions.query('declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
                /MI:root/MI:Location   
              ') as "*"  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH;   
```  
  
 以下是結果。 插入 XQuery 所傳回的 XML，但不會有包裝元素。  

```xml
<row>
  <ProductModelID>7</ProductModelID>
  <Name>HL Touring Frame</Name>
  <MI:Location LocationID="10">...</MI:Location>
  <MI:Location LocationID="20">...</MI:Location>
  ...
</row>
```

## <a name="see-also"></a>另請參閱  
 [搭配 FOR XML 使用 PATH 模式](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
