---
title: 串連運算子 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7298f80a7d3f61b5b00692be8fbc480429487454
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68892464"
---
# <a name="concatenation-operators"></a>串連運算子


  串連運算子 (Concatenation Operator) 的符號為加號 (+)。 您可以將兩個或更多個字元字串合併或串連成一個字元字串。 您也可以串連二進位字串。  
  
 以下程式碼是串連運算子的範例，結合產_品名稱與產品的唯一名稱：  
  
```  
WITH MEMBER Measures.ProductName AS   
   Product.Product.CurrentMember.Name + " (" + Product.Product.CurrentMember.UniqueName + ")"  
SELECT   
   {Measures.ProductName} ON COLUMNS,  
   Product.Product.Members ON ROWS  
FROM [Adventure Works]  
```  
  
## <a name="language-considerations"></a>語言串連  
 當串連中使用的字串有相同的定序 (Collation) 時，產生的串連字串會擁有跟輸入一樣的定序。 如果串連中使用的字串有不同的定序，定序優先順序的規則就會決定產生之串連字串的定序。 如需詳細資訊，請參閱[語言和定序 &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/languages-and-collations-analysis-services)。  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 運算子參考 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [運算子 &#40;MDX 語法&#41;](../mdx/operators-mdx-syntax.md)  
  
  
