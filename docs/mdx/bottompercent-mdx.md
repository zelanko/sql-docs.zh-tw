---
title: BottomPercent （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cbcf9086cedc9221c39832bd0b7d55e5f0814c7f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68016908"
---
# <a name="bottompercent-mdx"></a>BottomPercent (MDX)


  以遞增的順序排序集合，並傳回數值最低的 Tuple 集合，此集合的累計總和等於或大於指定的百分比。  
  
## <a name="syntax"></a>語法  
  
```  
  
BottomPercent(Set_Expression, Percentage, Numeric_Expression)   
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *比例*  
 有效的數值運算式，指定要傳回的 Tuple 百分比。  
  
 *Numeric_Expression*  
 有效的數值運算式，這通常是傳回數字之資料格座標的多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **BottomPercent**函數會針對指定的集合進行評估之後，計算指定之數值運算式的總和，並以遞增的順序排序集合。 然後，此函數會傳回最低值的元素，它們的總和值累計百分比至少是指定的百分比。 這個函數會傳回累計總計至少是指定百分比之集合的最小子集。 傳回從最大到最小排列的元素。  
  
> [!IMPORTANT]  
>  **BottomPercent**函數（例如[TopPercent](../mdx/toppercent-mdx.md)函數）一律會中斷階層。 如需詳細資訊，請參閱 Order 函數。  
  
## <a name="example"></a>範例  
 下列範例會為 Bike 類別目錄傳回 2003 會計年度 Geography 維度 Geography 階層中 City 層級之成員的最小集合，此集合的累計總計使用 Reseller Sales Amount 量值計算至少是累計總計的 15% (以此集合中最小銷售數的成員開頭)。  
  
```  
SELECT  
[Product].[Product Categories].Bikes ON 0,  
BottomPercent  
   ({[Geography].[Geography].[City].Members}  
   , 15  
   , ([Measures].[Reseller Sales Amount],[Product].[Product Categories].Bikes)  
   ) ON 1  
FROM [Adventure Works]  
WHERE ([Measures].[Reseller Sales Amount],[Date].[Fiscal].[Fiscal Year].[FY 2003])  
```  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
