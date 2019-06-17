---
title: 維度 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b2703122b67debf0749abcd2ea01114fb6ecaa06
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63248137"
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
 如果指定階層編號，則**維度**函式會傳回其以零為起始的位置，在 cube 中的階層指定階層編號。  
  
 如果指定階層名稱，則**維度**函式會傳回指定的階層。 一般而言，您可以使用此字串版本**維度**與使用者定義函式的函式。  
  
> [!NOTE]  
>  **量值**維度永遠由`Dimensions(0)`。  
  
## <a name="examples"></a>範例  
 下列範例會使用**維度**函數來傳回名稱、 層級計數和計數指定的階層，使用數值運算式和字串運算式的成員。  
  
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
  
  
