---
title: 範例重新命名 &lt;row&gt; 元素 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, renaming <row> example
ms.assetid: b042292a-0b6e-40a3-b254-71c06e626706
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 01b835696c5e64182cffb72aea80d53b3c3bb776
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62704907"
---
# <a name="example-renaming-the-ltrowgt-element"></a>範例重新命名 &lt;row&gt; 元素
  如果是結果集中的每一個資料列，RAW 模式會產生一個 `<row>`元素。 您可以將一個選擇性引數指定給 RAW 模式，選擇性地為此元素指定另一個名稱，如下列查詢所示。 此查詢會針對資料列集的每一個資料列，各傳回一個 <`ProductModel`> 元素。  
  
## <a name="example"></a>範例  
  
```  
SELECT ProductModelID, Name   
FROM Production.ProductModel  
WHERE ProductModelID=122  
FOR XML RAW ('ProductModel'), ELEMENTS  
GO  
```  
  
 以下是結果。 因為已將 `ELEMENTS` 指示詞加入查詢中，所以結果會呈現為元素中心。  
  
```  
<ProductModel>  
  <ProductModelID>122</ProductModelID>  
  <Name>All-Purpose Bike Stand</Name>  
</ProductModel>   
```  
  
## <a name="see-also"></a>另請參閱  
 [使用 FOR XML 的 RAW 模式](use-raw-mode-with-for-xml.md)  
  
  
