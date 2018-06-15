---
title: 邏輯運算式 (XQuery) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- logical operators [SQL Server], XQuery
- effective Boolean value [XQuery]
- logical expressions [XQuery]
- EBV
- expressions [XQuery], logical
ms.assetid: de94cd2e-2d48-49fb-9ebd-a2d90c79bf62
caps.latest.revision: 26
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 20579cbbc8fc16fad2ab33c033fa8c73fbeadf1d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33076765"
---
# <a name="logical-expressions-xquery"></a>邏輯運算式 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery 支援邏輯**和**和**或**運算子。  
  
```  
expression1 and expression2  
expression1 or expression2  
```  
  
 測試運算式`expression1,``expression2`，請在[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]可能會導致空的序列、 一個或多個節點的序列或單一布林值。 根據結果而定，將以下列方式來決定有效的布林值：   
  
-   如果測試運算式產生空白時序，運算式的結果即為 False。  
  
-   如果測試運算式產生單一布林值 ，該值即為運算式的結果。  
  
-   如果測試運算式產生一或多個節點的序列，運算式的結果即為 True。  
  
-   否則，就會引發靜態錯誤。  
  
 邏輯**和**和**或**運算子套用至與標準語意之運算式結果的布林值。  
  
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
  
  
