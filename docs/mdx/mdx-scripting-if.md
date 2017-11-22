---
title: "如果陳述式 (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords: statements [MDX], IF
ms.assetid: 8830cce5-9e06-4f89-a555-295bb0d0a8a1
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: c5eaeffbc4ede2bedf0d85d8ef0ec4b40fb1993b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="mdx-scripting---if"></a>MDX 指令碼-如果
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  條件為 True 時執行陳述式。  
  
## <a name="syntax"></a>語法  
  
```  
  
IF expression THEN assignment END IF  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 評估為布林值而傳回  true 或 false 的多維度運算式  (MDX) 運算式。  
  
 *指派*  
 將值指派給 Subcube 或導出屬性的 MDX 運算式。  
  
## <a name="remarks"></a>備註  
 使用 IF 陳述式的控制流程中，這是與不同的是[IIf &#40;MDX &#41;](../mdx/iif-mdx.md)函式和[CASE 陳述式 &#40;MDX &#41;](../mdx/case-statement-mdx.md) ，只可用來傳回值或物件。  
  
## <a name="examples"></a>範例  
 在下列範例中，範圍限制在 Customers 維度之 Customers Geography 階層的 Country 層級。 如果目前的量值是 Internet Sales Amount，則 Internet Sales Amount 會設定為 10：  
  
 `SCOPE ([Customer].[Customer Geography].[Country].MEMBERS);`  
  
 `IF Measures.CurrentMember IS [Measures].[Internet Sales Amount] THEN this = 10 END IF;`  
  
 `END SCOPE`;  
  
## <a name="see-also"></a>請參閱＜  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
