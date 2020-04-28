---
title: 序數（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b22cc6d5a609f8e1f585ccc1229e0e1cd67e1796
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68055645"
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
 **序數**函數經常搭配**IIF**和**CurrentMember**函數使用，以根據查詢結果中每個特定資料格的序數位置，有條件地顯示不同階層層級的不同值。 例如，您可以使用**序數**函數來執行特定層級的計算，並在其他層級顯示預設值 "N/a"。  
  
## <a name="example"></a>範例  
 下列範例會傳回 Calendar 階層中 Calendar Quarter 層級的序號。  
  
```  
WITH MEMBER Measures.x AS [Date].[Calendar].[Calendar Quarter].Ordinal  
SELECT Measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
