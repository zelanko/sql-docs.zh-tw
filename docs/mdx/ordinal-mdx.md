---
title: 序數 (MDX) |Microsoft 文件
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 83036ec2ee0fa69c9ebb8cc2a905361eeae0aafa
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34742667"
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
  
  
