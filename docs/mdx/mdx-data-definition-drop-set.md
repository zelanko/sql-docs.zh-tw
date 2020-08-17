---
description: MDX 資料定義 - DROP SET
title: DROP SET 語句 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0992df0c7180c8a572fb1f8c34b99059ab118ea4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387234"
---
# <a name="mdx-data-definition---drop-set"></a>MDX 資料定義 - DROP SET


  移除命名集。  
  
## <a name="syntax"></a>語法  
  
```  
  
DROP [SESSION] SET   
   <Cube_Reference>.Set_Name   
               [,<Cube_Reference>.Set_Name ...n]  
  
<Cube_Reference> ::= {CURRENTCUBE | Cube_Name}  
  
```  
  
## <a name="arguments"></a>引數  
 *Cube_Name*  
 提供 Cube 名稱的有效字串運算式。  
  
 *Set_Name*  
 提供所要卸除之命名集名稱的有效字串運算式。  
  
## <a name="remarks"></a>備註  
 如需命名集的詳細資訊，請參閱[在 MDX 中建立命名集 &#40;MDX&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-named-sets-building-named-sets)。  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 資料定義語句 &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
