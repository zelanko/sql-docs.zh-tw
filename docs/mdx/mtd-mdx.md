---
title: Mtd (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 74c8748ae02df8747be5670f09ec11c7dfa8e882
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63278090"
---
# <a name="mtd-mdx"></a>Mtd (MDX)


  傳回與指定成員層級相同的同層級成員集合，以第一個同層級成員開始，以指定的成員結束，如同受 Time 維度中的 Year 層級條件約束。  
  
## <a name="syntax"></a>語法  
  
```  
  
Mtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 如果未指定成員運算式，預設值是第一個階層的目前成員的型別層級*個月*類型的第一個維度*時間*量值群組中。  
  
 **Mtd**功能的捷徑函數[PeriodsToDate](../mdx/periodstodate-mdx.md)函式時所依據的層級的屬性階層的 Type 屬性設定為*月*。 也就是說，`Mtd(Member_Expression)` 相當於 `PeriodsToDate(Month_Level_Expression,Member_Expression)`。  
  
## <a name="example"></a>範例  
 下列範例會傳回 2002 年 7 月初至 7 月 20 日當月網際網路銷售的月運費成本總和。  
  
```  
WITH MEMBER Measures.x AS SUM   
   (  
      MTD([Date].[Calendar].[Date].[July 20, 2002])  
     , [Measures].[Internet Freight Cost]  
     )  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [Sum &#40;MDX&#41;](../mdx/sum-mdx.md)   
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
