---
title: "Stdev 函數 (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STDEV
dev_langs:
- kbMDX
helpviewer_keywords:
- Stdev function [MDX]
ms.assetid: c3e31763-18ca-4a2b-bc03-3ee777970c68
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8cd0171595e5cdfd44c850565c0eba42d45784eb
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="stdev-mdx"></a>Stdev (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  使用非偏誤母體公式 (除以 n-1)，在評估集合後傳回數值運算式的樣本標準差。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stdev(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Numeric_Expression*  
 有效的數值運算式，這通常是傳回數字之資料格座標的多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **Stdev**函式會使用非偏誤的母體公式，而[StdevP](../mdx/stdevp-mdx.md)函數使用偏誤的母體公式。  
  
## <a name="example"></a>範例  
 下列範例使用非偏誤母體公式，針對 2003 日曆年度前三個月評估後，傳回 Internet Order Quantity 的標準差。  
  
```  
WITH MEMBER Measures.x AS   
   Stdev   
   ( { [Date].[Calendar].[Month].[January 2003],  
       [Date].[Calendar].[Month].[February 2003],  
       [Date].[Calendar].[Month].[March 2003]},  
    [Measures].[Internet Order Quantity])  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

