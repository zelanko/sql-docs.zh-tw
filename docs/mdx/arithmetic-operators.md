---
title: "算術運算子 |Microsoft 文件"
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
- arithmetic operators
ms.assetid: 1dff3e20-fe9d-4155-bf06-27d6458188e9
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: bc3adf599f92a74dd996a0ef090f6f42ab1fba0d
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="arithmetic-operators"></a>算術運算子
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

  您可以使用多維度運算式 (MDX) 中的算術運算子，執行任何算術計算，包括加、減、乘與除。  
  
 MDX 支援下表中列出的算術運算子。  
  
|運算子|Description|  
|--------------|-----------------|  
|[+ （加）](../mdx/add-mdx.md)|兩個數字相加。|  
|[/ （除法）](../mdx/divide-mdx-operator-reference.md)|以一個數目除以另一個數目。|  
|[* （乘）](../mdx/multiply-mdx.md)|兩個數目相乘。|  
|[-（減）](../mdx/subtract-mdx.md)|兩個數字相減。|  
|^ (乘冪)|計算某一個數字的次方數。|  
  
> [!NOTE]  
>  MDX 不包含用來取得某個數字之平方根的函數。 若要取得某個數字的平方根，請使用 ^ 運算子將它乘至 0.5 的乘冪。  
  
## <a name="order-of-precedence"></a>優先順序  
 下列規則決定算術運算子在 MDX 運算式中的優先順序：  
  
-   運算式中的算術運算子如果不止一個，MDX 就會先計算乘法與除法，然後再計算減法與加法。  
  
-   運算式中所有的算術運算子具有相同層級的優先順序時，執行順序為由左至右。  
  
-   先計算括號中的運算式，再計算其他所有運算。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 運算子參考 &#40;MDX &#41;](../mdx/mdx-operator-reference-mdx.md)   
 [運算子 &#40;MDX 語法 &#41;](../mdx/operators-mdx-syntax.md)  
  
  

