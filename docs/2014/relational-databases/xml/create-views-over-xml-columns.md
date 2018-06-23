---
title: 建立 XML 資料行檢視 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- views [XML in SQL Server]
ms.assetid: eb5f0439-1f69-49c2-8759-e59bda1633b7
caps.latest.revision: 14
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: ec628981acc51d660a0e8a99dba991d957955e9b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135574"
---
# <a name="create-views-over-xml-columns"></a>建立 XML 資料行檢視
  您可以使用`xml`類型資料行建立檢視。 下列範例會建立一個檢視中的值從`xml`類型資料行使用擷取`value()`方法`xml`資料型別。  
  
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
  
 請注意下列有關使用重點`xml`資料類型來建立檢視：  
  
-   xml 資料類型可以在具體化檢視中建立。 具體化檢視無法以 xml 資料類型方法為基礎， 但是，可以將它轉換成與基底資料表中之 xml 類型資料行不同的 XML 結構描述集合。  
  
-   `xml`資料類型不能在分散式資料分割檢視。  
  
-   針對此檢視執行的 SQL 預測將不會發送到檢視定義的 XQuery 中。  
  
-   檢視中的 XML 資料類型方法將無法更新。  
  
  