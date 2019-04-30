---
title: BottomPercent (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2a627ea8e5dd7a8f8266fcf0ea374e6abcde4bdc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63208800"
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
  
 *百分比*  
 有效的數值運算式，指定要傳回的 Tuple 百分比。  
  
 *Numeric_Expression*  
 有效的數值運算式，這通常是傳回數字之資料格座標的多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **BottomPercent**函式會計算指定的數值運算式，評估指定的集合，並以遞增順序排序集合的總和。 然後，此函數會傳回最低值的元素，它們的總和值累計百分比至少是指定的百分比。 這個函數會傳回累計總計至少是指定百分比之集合的最小子集。 傳回從最大到最小排列的元素。  
  
> [!IMPORTANT]  
>  **BottomPercent**函數跟[TopPercent](../mdx/toppercent-mdx.md)函式，必會破壞階層架構。 如需詳細資訊，請參閱 Order 函數。  
  
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
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
