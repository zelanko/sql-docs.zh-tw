---
title: "沒有名稱的資料行 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "名稱 [SQL Server], 資料行不具有"
ms.assetid: 440de44e-3a56-4531-b4e4-1533ca933cac
caps.latest.revision: 10
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 10
---
# 沒有名稱的資料行
  任何沒有名稱的資料行都將予以內嵌。 例如，未指定資料行別名的計算資料行或巢狀純量查詢將會產生沒有任何名稱的資料行。 如果此資料行是 **xml** 類型，就會插入該資料類型執行個體的內容。 否則，就會以文字節點的形式插入資料行內容。  
  
```  
SELECT 2+2  
FOR XML PATH  
```  
  
 產生此 XML。 依預設，對於資料列集中的每個資料列，產生的 XML 中會產生 <`row`> 元素。 這與 RAW 模式相同。  
  
 `<row>4</row>`  
  
 下列查詢會傳回三個資料行的資料列集。 沒有名稱的第三個資料行具有 XML 資料。 PATH 模式會插入 xml 類型的執行個體。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID,  
       Name,  
       Instructions.query('declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
                /MI:root/MI:Location   
              ')   
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH ;  
GO  
```  
  
 以下是部份結果：  
  
 `<row>`  
  
 `<ProductModelID>7</ProductModelID>`  
  
 `<Name>HL Touring Frame</Name>`  
  
 `<MI:Location ...LocationID="10" ...></MI:Location>`  
  
 `<MI:Location ...LocationID="20" ...></MI:Location>`  
  
 `...`  
  
 `</row>`  
  
## 另請參閱  
 [搭配 FOR XML 使用 PATH 模式](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  