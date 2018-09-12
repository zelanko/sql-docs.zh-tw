---
title: 建立 XML 資料行檢視 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- views [XML in SQL Server]
ms.assetid: eb5f0439-1f69-49c2-8759-e59bda1633b7
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cc4890077c25e98ebff0832423f6d1f0aaabdc46
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43889214"
---
# <a name="create-views-over-xml-columns"></a>建立 XML 資料行檢視
  您可以使用`xml`類型資料行建立檢視。 下列範例會建立一個檢視中的值`xml`類型資料行使用來擷取`value()`方法`xml`資料型別。  
  
```  
-- Create the table.  
CREATE TABLE T (  
    ProductID          int primary key,   
    CatalogDescription xml)  
GO  
-- Insert sample data.  
INSERT INTO T values(1,'<ProductDescription ProductID="1" ProductName="SomeName" />')  
GO  
-- Create view (note the value() method used to retrieve ProductName   
-- attribute value from the XML).  
CREATE VIEW MyView AS   
  SELECT ProductID,  
         CatalogDescription.value('(/ProductDescription/@ProductName)[1]', 'varchar(40)') AS PName  
  FROM T  
GO   
```  
  
 針對此檢視執行下列查詢：  
  
```  
SELECT *   
FROM   MyView  
```  
  
 以下是結果：  
  
```  
ProductID   PName        
----------- ------------  
1           SomeName   
```  
  
 請注意下列有關使用`xml`建立檢視的資料類型：  
  
-   xml 資料類型可以在具體化檢視中建立。 具體化檢視無法以 xml 資料類型方法為基礎， 但是，可以將它轉換成與基底資料表中之 xml 類型資料行不同的 XML 結構描述集合。  
  
-   `xml`資料型別不能在分散式資料分割檢視。  
  
-   針對此檢視執行的 SQL 預測將不會發送到檢視定義的 XQuery 中。  
  
-   檢視中的 XML 資料類型方法將無法更新。  
  
  
