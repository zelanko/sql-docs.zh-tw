---
title: 層級 (MDX) |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2fba58261bb0ba8f91e8127b1d33b847accf0dc7
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579510"
---
# <a name="levels-mdx"></a>Levels (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
 *L*  
 指定層級名稱的有效字串運算式。  
  
## <a name="remarks"></a>備註  
 如果指定層級編號，**層級**函式會傳回與指定的以零為起始位置相關聯的層級。  
  
 如果指定層級的名稱，則**層級**函式會傳回指定層級。  
  
> [!NOTE]  
>  對於使用者自訂函數，請使用字串運算式語法。  
  
## <a name="examples"></a>範例  
 下列範例將說明每個**層級**函數的語法。  
  
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
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
