---
description: LastPeriods (MDX)
title: LastPeriods (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 60e8adf1dba453fb536f95a4fa113e16f6950f62
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494881"
---
# <a name="lastperiods-mdx"></a>LastPeriods (MDX)


  傳回指定成員之前的成員集合 (包含指定成員)。  
  
## <a name="syntax"></a>語法  
  
```  
  
LastPeriods(Index [ ,Member_Expression ] )  
```  
  
## <a name="arguments"></a>引數  
 *Index*  
 指定週期數目的有效數值運算式。  
  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 如果指定的週期數目是正數， **LastPeriods** 函式會傳回一組成員，這些成員是從指定成員運算式的 *索引* -1 落後的成員開始，並以指定的成員做為結尾。 函數傳回的成員數目等於 *Index*。  
  
 如果指定的週期數目是負數， **LastPeriods** 函式會傳回一組以指定成員開頭的成員，並以從指定成員的 (- *Index* -1) 的成員做為結尾。 函數傳回的成員數目等於 *索引*的絕對值。  
  
 如果指定的週期數目為零，則 **LastPeriods** 函數會傳回空集合。 這不同于 **Lag** 函數，如果指定0，則會傳回指定的成員。  
  
 如果未指定成員， **LastPeriods** 函數會使用 **CurrentMember**。 如果沒有維度標示為 Time 維度，此函數將會剖析，並且在不發生錯誤的情況下執行，但會在用戶端應用程式中造成資料格錯誤。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 2002 會計年度第二、第三、第四會計季度的預設量值。  
  
```  
SELECT LastPeriods(3,[Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002]) ON 0  
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  這個範例也可以使用 : (冒號) 運算子撰寫如下：  
>   
>  `[Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002]: [Date].[Fiscal].[Fiscal Quarter].[Q2 FY 2002]`  
  
 下列範例會傳回 2002 會計年度第一個會計季度的預設量值。 雖然指定的週期數是三，但是只會傳回一個，因為該會計年度中沒有更早的週期。  
  
```  
SELECT LastPeriods  
   (3,[Date].[Fiscal].[Fiscal Quarter].[Q1 FY 2002]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
