---
title: 邏輯運算式（XQuery） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
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
ms.openlocfilehash: 5b1dc7b961dd0b85824ea180cbc4815d5488a360
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68004501"
---
# <a name="logical-expressions-xquery"></a>邏輯運算式 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery 支援邏輯**and**和**or**運算子。  
  
```  
expression1 and expression2  
expression1 or expression2  
```  
  
 中[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的測試運算式`expression1,``expression2`會產生空的序列、一或多個節點的序列，或單一布林值。 根據結果而定，將以下列方式來決定有效的布林值：   
  
-   如果測試運算式產生空白時序，運算式的結果即為 False。  
  
-   如果測試運算式產生單一布林值 ，該值即為運算式的結果。  
  
-   如果測試運算式產生一或多個節點的序列，運算式的結果即為 True。  
  
-   否則，就會引發靜態錯誤。  
  
 接著，邏輯**and**和**or**運算子會套用至具有標準邏輯語義的運算式產生的布林值。  
  
 下列查詢會從產品目錄中，針對特定的產品型號，從「封面`Picture`小型圖片」、「<> 元素」中抓取。 請注意對於每個產品描述文件，目錄可以儲存具有不同屬性的一或多個產品圖片，例如大小與角度。  
  
```  
SELECT CatalogDescription.query('  
     declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
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
  xmlns:PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
  <PD:Angle>front</PD:Angle>  
  <PD:Size>small</PD:Size>  
  <PD:ProductPhotoID>31</PD:ProductPhotoID>  
</PD:Picture>  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [XQuery 運算式](../xquery/xquery-expressions.md)  
  
  
