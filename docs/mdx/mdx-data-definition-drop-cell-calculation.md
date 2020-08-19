---
description: MDX 資料定義 - DROP CELL CALCULATION
title: DROP CELL CALCULATION 語句 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a407d6325168e2287fc6b815b3b45f0130dd1a4d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429800"
---
# <a name="mdx-data-definition---drop-cell-calculation"></a>MDX 資料定義 - DROP CELL CALCULATION


  移除指定的資料格計算。  
  
## <a name="syntax"></a>語法  
  
```  
  
DROP [ SESSION ] CELL CALCULATION CURRENTCUBE | Cube_Name.CellCalc_Name  
```  
  
## <a name="arguments"></a>引數  
 *Cube_Name*  
 提供 Cube 運算式名稱的有效字串運算式。  
  
 *CellCalc_Name*  
 提供所要卸除之資料格計算名稱的有效字串運算式。  
  
## <a name="see-also"></a>另請參閱  
 [CREATE CELL CALCULATION 語句 &#40;MDX&#41;](../mdx/mdx-data-definition-create-cell-calculation.md)   
 [Mdx 資料定義語句 &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
