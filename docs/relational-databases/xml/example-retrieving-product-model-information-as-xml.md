---
title: 範例：以 XML 的形式擷取產品型號資訊 | Microsoft Docs
description: 請檢視範例，以了解如何搭配 FOR XML 子句來使用 RAW 模式將產品模型資訊作為 XML 擷取。
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, retrieving XML information example
ms.assetid: 3828b4ca-3ab2-444f-9c58-8be6e7f064a6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4850857682bddf64be8312cea67d577cc3a1f939
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85632762"
---
# <a name="example-retrieving-product-model-information-as-xml"></a>範例：將產品型號資訊當做 XML 來擷取
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  下列查詢會傳回產品型號資訊。 `RAW` 模式是在 `FOR XML` 子句中指定。  
  
## <a name="example"></a>範例  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119  
FOR XML RAW;  
GO  
```  
  
 以下是部份結果：  
  
 `<row ProductModelID="122" Name="All-Purpose Bike Stand" />`  
  
 `<row ProductModelID="119" Name="Bike Wash" />`  
  
 您可以指定 `ELEMENTS` 指示詞，以擷取元素中心的 XML。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119  
FOR XML RAW, ELEMENTS;  
GO  
```  
  
 以下是結果：  
  
```  
<row>  
  <ProductModelID>122</ProductModelID>  
  <Name>All-Purpose Bike Stand</Name>  
</row>  
<row>  
  <ProductModelID>119</ProductModelID>  
  <Name>Bike Wash</Name>  
</row>  
```  
  
 您可以選擇性地指定 `TYPE` 指示詞，將結果擷取為 **XML** 類型。 `TYPE` 指示詞不會變更結果的內容， 只會影響結果的資料類型。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119  
FOR XML RAW, TYPE ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [搭配 FOR XML 使用 RAW 模式](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
  
  
