---
description: Levels (MDX)
title: 層級 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f3b0a7eaea166fdefbfd947faf95b58f74bdb8be
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429870"
---
# <a name="levels-mdx"></a>Levels (MDX)


  傳回層級，而其在維度或階層中的位置是由數值運算式指定，或者其名稱是由字串運算式指定。  
  
## <a name="syntax"></a>語法  
  
```  
  
Numeric expression syntax  
Hierarchy_Expression.Levels( Level_Number )  
  
String expression syntax  
Hierarchy_Expression.Levels( Level_Name )  
```  
  
## <a name="arguments"></a>引數  
 *Hierarchy_Expression*  
 傳回階層的有效多維度運算式 (MDX) 運算式。  
  
 *Level_Number*  
 指定層級編號的有效數值運算式。  
  
 *Level_Name*  
 指定層級名稱的有效字串運算式。  
  
## <a name="remarks"></a>備註  
 如果指定 **了層級** 編號，level 函式會傳回與指定之以零為基底的位置相關聯的層級。  
  
 如果指定了層級名稱，level **函數會** 傳回指定的層級。  
  
> [!NOTE]  
>  對於使用者自訂函數，請使用字串運算式語法。  
  
## <a name="examples"></a>範例  
 下列範例說明每個 **層級** 函數語法。  
  
### <a name="numeric"></a>數值  
 下列範例會傳回 Country 層級：  
  
```  
SELECT [Geography].[Geography].Levels(1) ON 0  
FROM [Adventure Works]  
```  
  
### <a name="string"></a>String  
 下列範例會傳回 Country 層級：  
  
```  
SELECT [Geography].[Geography].Levels('Country') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
