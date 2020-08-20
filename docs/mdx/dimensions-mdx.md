---
description: Dimensions (MDX)
title: 維度 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c98167516f9e01525ecd351389c885c48626636e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491415"
---
# <a name="dimensions-mdx"></a>Dimensions (MDX)


  傳回由數值或字串運算式所指定的階層。  
  
## <a name="syntax"></a>語法  
  
```  
  
Numeric expression syntax  
Dimensions(Hierarchy_Number)  
  
String expression syntax  
Dimensions(Hierarchy_Name)  
```  
  
## <a name="arguments"></a>引數  
 *Hierarchy_Number*  
 指定階層編號的有效數值運算式。  
  
 *Hierarchy_Name*  
 指定階層名稱的有效字串運算式。  
  
## <a name="remarks"></a>備註  
 如果指定了階層編號， **維度** 函數會傳回階層，其在 cube 內的以零為基底的位置是指定的階層編號。  
  
 如果指定階層名稱， **維度** 函數會傳回指定的階層。 一般來說，您會將這個字串 **版本的 dimension 函數與** 使用者定義函數搭配使用。  
  
> [!NOTE]  
>  **量值**維度一律以表示 `Dimensions(0)` 。  
  
## <a name="examples"></a>範例  
 下列範例會使用數值運算式和字串 **運算式，以使用 dimension 函數來** 傳回指定階層的名稱、層級計數和成員計數。  
  
```  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Name  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Levels.Count  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Members.Count  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Name  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Levels.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Members.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
