---
description: Ordinal (MDX)
title: 序數 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 74811da22f8c73536749acad41dfbe859b00eeea
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471730"
---
# <a name="ordinal-mdx"></a>Ordinal (MDX)


  傳回與層級有關以零為基準的序號。  
  
## <a name="syntax"></a>語法  
  
```  
  
Level_Expression.Ordinal   
```  
  
## <a name="arguments"></a>引數  
 *Level_Expression*  
 傳回層級的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **序數**函數經常搭配**IIF**和**CurrentMember**函數使用，以根據查詢結果中每個特定資料格的序數位置，有條件地在不同的階層層級顯示不同的值。 例如，您可以使用 **序數** 函數在特定層級執行計算，並在其他層級顯示預設值 "N/a"。  
  
## <a name="example"></a>範例  
 下列範例會傳回 Calendar 階層中 Calendar Quarter 層級的序號。  
  
```  
WITH MEMBER Measures.x AS [Date].[Calendar].[Calendar Quarter].Ordinal  
SELECT Measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
