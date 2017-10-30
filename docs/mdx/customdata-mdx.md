---
title: "CustomData (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- EXISTS
dev_langs:
- kbMDX
helpviewer_keywords:
- Exists function
ms.assetid: 61d9f5a2-6f56-4179-a39b-317c8e0a2cdd
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 47f1f10a7636a2c53dc897d9e6858ac214281e73
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="customdata-mdx"></a>CustomData (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回的值**CustomData**有定義; 否則，連接字串屬性**null**。  
  
## <a name="syntax"></a>語法  
  
```  
  
CustomData()  
```  
  
## <a name="return-value"></a>傳回值  
 **CustomData**函式可擷取**CustomData**連接字串屬性，並且傳遞組態設定可供多維度運算式 (MDX) 函數和陳述式，例如[UserName (MDX)](../mdx/username-mdx.md)和[呼叫陳述式 (MDX)](../mdx/mdx-data-manipulation-call.md)。 例如，此函式可以用於動態安全性運算式中選取中的字串值的允許/拒絕的集合成員**CustomData**連接字串屬性。  
  
## <a name="example"></a>範例  
 下列查詢會顯示所傳回的值**CustomData**中導出量值函式：  
  
```  
WITH MEMBER [Measures].CUSTOMDATADEMO AS CUSTOMDATA()  
SELECT [Measures].CUSTOMDATADEMO ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

