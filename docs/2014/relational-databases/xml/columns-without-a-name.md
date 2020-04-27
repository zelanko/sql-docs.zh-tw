---
title: 沒有名稱的資料行 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns without
ms.assetid: 440de44e-3a56-4531-b4e4-1533ca933cac
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8e4d4eccfe7bcad3abd2c6d89f867ac8f88129a6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62637586"
---
# <a name="columns-without-a-name"></a>沒有名稱的資料行
  任何沒有名稱的資料行都將予以內嵌。 例如，未指定資料行別名的計算資料行或巢狀純量查詢將會產生沒有任何名稱的資料行。 如果此資料行是 `xml` 類型，就會插入該資料類型執行個體的內容。 否則，就會以文字節點的形式插入資料行內容。  
  
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
       Instructions.query('declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
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
  
## <a name="see-also"></a>另請參閱  
 [搭配 FOR XML 使用 PATH 模式](use-path-mode-with-for-xml.md)  
  
  
