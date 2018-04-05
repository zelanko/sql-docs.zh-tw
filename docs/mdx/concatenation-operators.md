---
title: 串連運算子 |Microsoft 文件
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- concatenation operators [MDX]
ms.assetid: 9e4c181a-b71e-41ec-98a1-ec8b5b5103b1
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 53d8d860a6725c9967dc3f16459a1782bdf93db8
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="concatenation-operators"></a>串連運算子
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 當串連中使用的字串有相同的定序 (Collation) 時，產生的串連字串會擁有跟輸入一樣的定序。 如果串連中使用的字串有不同的定序，定序優先順序的規則就會決定產生之串連字串的定序。 如需詳細資訊，請參閱[語言和定序 &#40;Analysis Services&#41;](../analysis-services/languages-and-collations-analysis-services.md)。  
  
## <a name="see-also"></a>請參閱  
 [MDX 運算子參考 &#40;MDX &#41;](../mdx/mdx-operator-reference-mdx.md)   
 [運算子 &#40;MDX 語法 &#41;](../mdx/operators-mdx-syntax.md)  
  
  
