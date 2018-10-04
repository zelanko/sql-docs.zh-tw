---
title: 邏輯運算式 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- logical operators [SQL Server], XQuery
- effective Boolean value [XQuery]
- logical expressions [XQuery]
- EBV
- expressions [XQuery], logical
ms.assetid: de94cd2e-2d48-49fb-9ebd-a2d90c79bf62
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f30b9673ac7ba59e54544e00aaeecbf501c7500b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47627896"
---
# <a name="logical-expressions-xquery"></a>邏輯運算式 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery 支援邏輯**並**並**或**運算子。  
  
```  
expression1 and expression2  
expression1 or expression2  
```  
  
 測試運算式`expression1,``expression2`，請在[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]可能會導致空的序列、 一或多個節點的序列或單一布林值。 根據結果而定，將以下列方式來決定有效的布林值：   
  
-   如果測試運算式產生空白時序，運算式的結果即為 False。  
  
-   如果測試運算式產生單一布林值 ，該值即為運算式的結果。  
  
-   如果測試運算式產生一或多個節點的序列，運算式的結果即為 True。  
  
-   否則，就會引發靜態錯誤。  
  
 邏輯**並**並**或**運算子則會套用至產生的布林值，與標準語意之運算式。  
  
 下列查詢會從產品目錄擷取特定產品型號正面角度的小型圖片，即  <`Picture`> 元素。 請注意對於每個產品描述文件，目錄可以儲存具有不同屬性的一或多個產品圖片，例如大小與角度。  
  
```  
SELECT CatalogDescription.query('  
     declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     for $F in /PD:ProductDescription/PD:Picture[PD:Size="small"   
                                                 and PD:Angle="front"]  
     return   
         $F   
    ') as Result  
FROM  Production.ProductModel  
where ProductModelID=19  
```  
  
 以下是結果：  
  
```  
<PD:Picture   
  xmlns:PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
  <PD:Angle>front</PD:Angle>  
  <PD:Size>small</PD:Size>  
  <PD:ProductPhotoID>31</PD:ProductPhotoID>  
</PD:Picture>  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [XQuery 運算式](../xquery/xquery-expressions.md)  
  
  
