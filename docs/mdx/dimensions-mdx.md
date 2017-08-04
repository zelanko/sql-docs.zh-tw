---
title: "維度 (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Dimensions
dev_langs:
- kbMDX
helpviewer_keywords:
- Dimensions function
ms.assetid: 64f63aa0-ef74-4415-a0c9-8acc6cd81739
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 462ea16745816af3c344af05f24437f370e7ce9e
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="dimensions-mdx"></a>Dimensions (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 如果指定階層編號，**維度**函式會傳回其以零為起始的位置，在 cube 內階層指定階層編號。  
  
 如果指定階層名稱，則**維度**函式會傳回指定的階層。 一般而言，您可以使用此字串版本**維度**函式搭配使用者自訂函數。  
  
> [!NOTE]  
>  **量值**維度永遠由`Dimensions(0)`。  
  
## <a name="examples"></a>範例  
 下列範例會使用**維度**函數來傳回名稱、 層級計數和指定的階層，使用數值運算式和字串運算式的成員計數。  
  
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
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

