---
title: '- （負）(MDX) |Microsoft 文件'
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 294d932740c210a6b20e209d4da315364c585526
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580790"
---
# <a name="--negative-mdx"></a>- (負) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="see-also"></a>另請參閱  
 [MDX 運算子參考&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
