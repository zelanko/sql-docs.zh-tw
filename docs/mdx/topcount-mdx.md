---
description: TopCount (MDX)
title: TopCount (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b7d917963d8500e06bf9d2adcd1057e72e50512a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412874"
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
  
 *Count*  
 有效的數值運算式，會指定要傳回的 Tuple 數目。  
  
 *Numeric_Expression*  
 有效的數值運算式，這通常是傳回數字之資料格座標的多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 如果指定了數值運算式， **TopCount** 函式會根據指定的集合，以遞減的順序來排序指定集合中由指定集合指定的元組。 排序集合之後， **TopCount** 函式會傳回具有最高值的指定數量的元組。  
  
> [!IMPORTANT]  
>  如同 [BottomCount](../mdx/bottomcount-mdx.md) 函式， **TopCount** 函數一律會中斷階層。  
  
 如果未指定數值運算式，則函式會以自然順序傳回成員的集合，不含任何排序，其行為就像 [Head (MDX) ](../mdx/head-mdx.md) 函數一樣。  
  
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
  
  
