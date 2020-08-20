---
description: Qtd (MDX)
title: Qtd (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ea3bd80fa85d95dd3adf52793d5895425b40b9fe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500451"
---
# <a name="qtd-mdx"></a>Qtd (MDX)


  傳回一組與指定成員相同層級的一組同級成員，以第一個同級為開頭，並以指定的成員結束，如同時間維度中的 *季* 層級條件約束。  
  
## <a name="syntax"></a>語法  
  
```  
  
Qtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 如果未指定成員運算式，則預設值為量值群組中*Time*類型之第一個維度中，第一個階層的目前成員，其類型為*季*。  
  
 **Qtd**函式是[PeriodsToDate &#40;MDX&#41;](../mdx/periodstodate-mdx.md)函數的快捷方式函數，其層級運算式引數設定為*季*。 也就是說，`Qtd(Member_Expression)` 與 `PeriodsToDate(Quarter_Level_Expression, Member_Expression)` 的功能相同。  
  
## <a name="example"></a>範例  
 下列範例會傳回成員的總和 `Measures.[Order Quantity]` ，該成員是 `Date` 從 [ **艾德作品** ] cube 中包含在維度的第三季第三2003季的前兩個月匯總。  
  
```  
WITH MEMBER [Date].[Calendar].[First2MonthsSecondSemester2003] AS  
    Aggregate(  
        QTD([Date].[Calendar].[Month].[August 2003])  
    )  
SELECT   
    [Date].[Calendar].[First2MonthsSecondSemester2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
