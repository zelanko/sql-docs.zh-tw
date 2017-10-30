---
title: "串連運算子 |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
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
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ae299577ece2c712504631fb85eeac4499c4d4c7
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="concatenation-operators"></a>串連運算子
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="see-also"></a>另請參閱  
 [MDX 運算子參考 &#40;MDX &#41;](../mdx/mdx-operator-reference-mdx.md)   
 [運算子 &#40;MDX 語法 &#41;](../mdx/operators-mdx-syntax.md)  
  
  

