---
title: TopCount (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fa8edcf8af510a41affdcbcc9924edf69cf4c220
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63228050"
---
# <a name="topcount-mdx"></a>TopCount (MDX)


  以遞減的順序排序集合，並傳回數值最高的指定元素數。  
  
## <a name="syntax"></a>語法  
  
```  
  
TopCount(Set_Expression,Count [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *計數*  
 有效的數值運算式，會指定要傳回的 Tuple 數目。  
  
 *Numeric_Expression*  
 有效的數值運算式，這通常是傳回數字之資料格座標的多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 如果指定數值運算式，則**TopCount**函式，依遞減順序排序，評估指定數值運算式所指定的值根據所指定集合中 tuple設定。 排序集合之後, **TopCount**函式會傳回指定的最高值的 tuple 數目。  
  
> [!IMPORTANT]  
>  像是[BottomCount](../mdx/bottomcount-mdx.md)函式**TopCount**函數必會破壞階層架構。  
  
 如果未指定數值運算式，函數會傳回集合的成員以自然的順序，不進行任何排序，其運作方式[Head (MDX)](../mdx/head-mdx.md)函式。  
  
## <a name="examples"></a>範例  
 下列範例會依 Internet Sales Amount 傳回前 10 天：  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `TOPCOUNT([Date].[Date].[Date].MEMBERS, 10, [Measures].[Internet Sales Amount])`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 下列範例會為 Bike 類別目錄傳回集合中的前五個成員，這個集合包含 Geography 維度 Geography 階層 City 層級以及 Date 維度 Fiscal 階層所有會計年度的成員組合，並根據 Reseller Sales Amount 量值排序 (以此集合中最大銷售數的成員開頭)。  
  
```  
SELECT [Measures].[Reseller Sales Amount] ON 0,  
TopCount  
   ({[Geography].[Geography].[City].Members   
      *[Date].[Fiscal].[Fiscal Year].Members}  
   , 5  
   , [Measures].[Reseller Sales Amount]  
   ) ON 1  
FROM [Adventure Works]  
WHERE([Product].[Product Categories].Bikes)  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
