---
title: 序數 (MDX) |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 61c5c3c4bbb2f04f1ebb9743e18eb8088632eab0
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581260"
---
# <a name="ordinal-mdx"></a>Ordinal (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回與層級有關以零為基準的序號。  
  
## <a name="syntax"></a>語法  
  
```  
  
Level_Expression.Ordinal   
```  
  
## <a name="arguments"></a>引數  
 *Level_Expression*  
 傳回層級的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **序數**函式經常用於搭配**IIF**和**CurrentMember**有條件地顯示不同的值不同階層層級的函式會根據查詢結果中的每個特定的資料格的序數位置。 例如，您可以使用**序數**函式來執行特定層級的計算，並在其他層級顯示預設值是"N/A"。  
  
## <a name="example"></a>範例  
 下列範例會傳回 Calendar 階層中 Calendar Quarter 層級的序號。  
  
```  
WITH MEMBER Measures.x AS [Date].[Calendar].[Calendar Quarter].Ordinal  
SELECT Measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
