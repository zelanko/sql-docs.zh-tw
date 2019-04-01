---
title: 建立 XML 資料行檢視 | Microsoft Docs
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- views [XML in SQL Server]
ms.assetid: eb5f0439-1f69-49c2-8759-e59bda1633b7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7fcb87e9baac60999f5fd810556d2d9e0790b1a9
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511565"
---
# <a name="create-views-over-xml-columns"></a>建立 XML 資料行檢視
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  您可以使用 **xml** 類型的資料行建立檢視。 下列範例會建立一個檢視，而在此檢視中會使用 `xml` xml **資料類型的** value() **方法，擷取** 類型資料行中的值。  
  
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
  
 請注意下列有關使用 **xml** 資料類型來建立檢視的要點：  
  
-   xml 資料類型可以在具體化檢視中建立。 具體化檢視無法以 xml 資料類型方法為基礎， 但是，可以將它轉換成與基底資料表中之 xml 類型資料行不同的 XML 結構描述集合。  
  
-   **xml** 資料類型無法用於「分散式資料分割檢視」。  
  
-   針對此檢視執行的 SQL 預測將不會發送到檢視定義的 XQuery 中。  
  
-   檢視中的 XML 資料類型方法將無法更新。  
  
  
