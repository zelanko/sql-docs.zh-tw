---
description: Axis (MDX)
title: 軸 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 47e0da231b0792e0099f5e6ee4fe8eda9fb45f9d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421932"
---
# <a name="axis-mdx"></a>Axis (MDX)


  傳回指定座標軸上的 Tuple 集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Axis(Axis_Number)  
```  
  
## <a name="arguments"></a>引數  
 *Axis_Number*  
 指定座標軸數目的有效數值運算式。  
  
## <a name="remarks"></a>備註  
 **Axis**函數會使用軸的以零為基底的位置，來傳回軸上的一組元組。 例如，`Axis(0)` 傳回 COLUMNS 座標軸，`Axis(1)` 傳回 ROWS 座標軸等等。 **軸**函數不能用在篩選軸上。 使用這個函數可讓導出成員得知正在執行之查詢的內容。 例如，您可以建立一個導出成員，讓它只提供資料列軸上選取之成員的總和。 它也可讓某一軸的定義相依於另一軸的定義。 例如，根據資料行軸上第一個項目的值來排序資料列軸的內容。  
  
> [!NOTE]  
>  座標軸僅能參考先前的座標軸。 例如，`Axis(0)` 必須在評估 COLUMNS 座標軸之後出現，如在 ROW 或 PAGE 座標軸上。  
  
## <a name="examples"></a>範例  
 下列範例查詢會示範如何使用 Axis 函數：  
  
 `WITH MEMBER MEASURES.AXISDEMO AS`  
  
 `SETTOSTR(AXIS(1))`  
  
 `SELECT MEASURES.AXISDEMO ON 0,`  
  
 `[Date].[Calendar Year].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 下列範例會示範如何在導出成員內使用 Axis 函數：  
  
 `WITH MEMBER MEASURES.AXISDEMO AS`  
  
 `SUM(AXIS(1), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.AXISDEMO} ON 0,`  
  
 `{[Date].[Calendar Year].&[2003], [Date].[Calendar Year].&[2004]} ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
