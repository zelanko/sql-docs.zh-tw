---
title: CustomData （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d2884e23cbee78acacdb72e386f0e99610e9629f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68135831"
---
# <a name="customdata-mdx"></a>CustomData (MDX)


  傳回**CustomData**連接字串屬性的值（如果已定義）。否則**為 null**。  
  
## <a name="syntax"></a>語法  
  
```  
  
CustomData()  
```  
  
## <a name="return-value"></a>傳回值  
 **CustomData**函數可以抓取**CustomData**連接字串屬性，並傳遞要供多維度運算式（mdx）函數和語句使用的設定（例如[UserName （mdx）](../mdx/username-mdx.md)和[CALL 語句（mdx））](../mdx/mdx-data-manipulation-call.md)。 例如，這個函數可以在動態安全性運算式中用來選取**CustomData**連接字串屬性中字串值的允許/拒絕集合成員。  
  
## <a name="example"></a>範例  
 下列查詢會顯示計算量值中**CustomData**函數所傳回的值：  
  
```  
WITH MEMBER [Measures].CUSTOMDATADEMO AS CUSTOMDATA()  
SELECT [Measures].CUSTOMDATADEMO ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
