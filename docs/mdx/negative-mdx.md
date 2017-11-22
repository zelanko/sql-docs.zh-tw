---
title: "- （負）(MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: '-'
dev_langs: kbMDX
helpviewer_keywords:
- '- (negative)'
- negative operator (-)
ms.assetid: 7fbe83ed-aaa5-41f6-a17c-bfc2e1bffa77
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 8edc65c7a9c021dbb8f3ae28e83413fbf3b3548c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="--negative-mdx"></a>- (負) (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  執行一元運算，這項運算會傳回數值運算式的負值。  
  
## <a name="syntax"></a>語法  
  
```  
  
- Numeric_Expression  
```  
  
#### <a name="parameters"></a>參數  
 *Numeric_Expression*  
 傳回數值的有效多維度運算式 (MDX) 運算式。  
  
## <a name="return-value"></a>傳回值  
 具有指定參數之資料類型的負值。  
  
## <a name="examples"></a>範例  
 以下範例示範此運算子的用法。  
  
```  
-- This member creates a negative version of the  
-- Reseller Freight Cost.  
WITH MEMBER   
   Measures.[Resell Cost as Negative]   
   AS -Measures.[Reseller Freight Cost]  
SELECT   
   [Date].[Calendar Month of Year].Children ON COLUMNS,  
   [Product].[Product Categories].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    {[Measures].[Resell Cost as Negative]}  
```  
  
## <a name="see-also"></a>請參閱＜  
 [MDX 運算子參考 &#40;MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
