---
title: LastPeriods （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6a9337e925da40f148bbe0d2c77fb1cf4f5f1a99
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67905769"
---
# <a name="lastperiods-mdx"></a>LastPeriods (MDX)


  傳回指定成員之前的成員集合 (包含指定成員)。  
  
## <a name="syntax"></a>語法  
  
```  
  
LastPeriods(Index [ ,Member_Expression ] )  
```  
  
## <a name="arguments"></a>引數  
 *索引*  
 指定週期數目的有效數值運算式。  
  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 如果指定的週期數目是正數，則**LastPeriods**函數會傳回一組成員，其開頭為從指定成員運算式延遲*索引*1 的成員，並以指定的成員做為結尾。 函數所傳回的成員數目等於*Index*。  
  
 如果指定的週期數目是負數， **LastPeriods**函數會傳回一組以指定成員開頭，並以指定成員的潛在客戶（-*索引*-1）為結尾的成員。 函數傳回的成員數目等於*Index*的絕對值。  
  
 如果指定的週期數目為零，則**LastPeriods**函數會傳回空的集合。 這不同于**Lag**函數，如果指定0，則會傳回指定的成員。  
  
 如果未指定成員， **LastPeriods**函數會使用**CurrentMember**。 如果沒有維度標示為 Time 維度，此函數將會剖析，並且在不發生錯誤的情況下執行，但會在用戶端應用程式中造成資料格錯誤。  
  
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
  
  
