---
title: 指定要搭配 FOR XML 使用的根元素 |Microsoft Docs
description: 檢視範例查詢，指定 FOR XML 子句的 ROOT 選項來在所產生 XML 中要求單一的最上層元素。
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, specifying root element example
- RAW mode, with FOR XML example
ms.assetid: bcc54b11-0713-4e43-8dbe-d6f3ad1993b5
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
ms.openlocfilehash: cf32be608e844036893b7c7dbf42ba76db0c203f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85632645"
---
# <a name="example-specifying-a-root-element-for-the-xml-generated-by-for-xml"></a>範例：為 FOR XML 產生的 XML 指定根元素
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  藉由在 `ROOT` 查詢中指定 `FOR XML` 選項，您可以要求在產生的 XML 中傳回單一的最上層元素，如下列查詢所示。 為 `ROOT` 指示詞所指定的引數會提供根元素的名稱。  
  
## <a name="example"></a>範例  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name   
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119 or ProductModelID=115  
FOR XML RAW, ROOT('MyRoot')  
GO
```  
  
 以下是結果：  
  
```  
<MyRoot>  
  <row ProductModelID="122" Name="All-Purpose Bike Stand" />  
  <row ProductModelID="119" Name="Bike Wash" />  
  <row ProductModelID="115" Name="Cable Lock" />  
</MyRoot>  
```  
  
## <a name="see-also"></a>另請參閱  
 [搭配 FOR XML 使用 RAW 模式](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
  
  
