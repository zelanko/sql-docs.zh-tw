---
title: CustomData (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d2884e23cbee78acacdb72e386f0e99610e9629f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135831"
---
# <a name="customdata-mdx"></a>CustomData (MDX)


  傳回的值**CustomData**連接字串屬性，如有定義; 否則**null**。  
  
## <a name="syntax"></a>語法  
  
```  
  
CustomData()  
```  
  
## <a name="return-value"></a>傳回值  
 **CustomData**函式可擷取**CustomData**連接字串屬性，並且傳遞組態設定可供多維度運算式 (MDX) 函數和陳述式，例如[UserName (MDX)](../mdx/username-mdx.md)並[CALL 陳述式 (MDX)](../mdx/mdx-data-manipulation-call.md)。 比方說，此函式可以用於動態安全性運算式來選取中的字串值的允許/拒絕的集合成員**CustomData**連接字串屬性。  
  
## <a name="example"></a>範例  
 下列查詢會顯示所傳回的值**CustomData**中導出量值函式：  
  
```  
WITH MEMBER [Measures].CUSTOMDATADEMO AS CUSTOMDATA()  
SELECT [Measures].CUSTOMDATADEMO ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
