---
description: CustomData (MDX)
title: CustomData (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ed7bfe2841caf9bd5b2c6e6caf102323db6d62ed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88413164"
---
# <a name="customdata-mdx"></a>CustomData (MDX)


  傳回 **CustomData** 連接字串屬性的值（如果已定義）。否則 **為 null**。  
  
## <a name="syntax"></a>語法  
  
```  
  
CustomData()  
```  
  
## <a name="return-value"></a>傳回值  
 **CustomData**函式可以取出**CustomData**連接字串屬性，並將多維度運算式所使用的設定設定 (mdx) 函數和語句，例如使用者[名稱 (MDX) ](../mdx/username-mdx.md) ，以及[ (mdx) 的呼叫語句](../mdx/mdx-data-manipulation-call.md)。 例如，您可以在動態安全性運算式中使用這個函數，在 **CustomData** 連接字串屬性中選取字串值的允許/拒絕的集合成員。  
  
## <a name="example"></a>範例  
 下列查詢會顯示計算量值中 **CustomData** 函數所傳回的值：  
  
```  
WITH MEMBER [Measures].CUSTOMDATADEMO AS CUSTOMDATA()  
SELECT [Measures].CUSTOMDATADEMO ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
