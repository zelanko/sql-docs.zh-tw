---
title: "建立 XML 資料行檢視 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: views [XML in SQL Server]
ms.assetid: eb5f0439-1f69-49c2-8759-e59bda1633b7
caps.latest.revision: "14"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7f54e918c8b2c26cfde2807e6049011f1b6698d8
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="create-views-over-xml-columns"></a>建立 XML 資料行檢視
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] 您可以使用 **xml** 類型的資料行建立檢視。 下列範例會建立一個檢視，而在此檢視中會使用 `xml` xml **資料類型的** value() **方法，擷取** 類型資料行中的值。  
  
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
  
  
