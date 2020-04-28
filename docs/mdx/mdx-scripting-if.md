---
title: IF 語句（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 41bd34fbd3d296f4aa38877e6d26e25eba9ae726
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68138685"
---
# <a name="mdx-scripting---if"></a>MDX 指令碼 - IF


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
 若為控制流程，請使用 IF 語句，這與[IIf &#40;mdx&#41;](../mdx/iif-mdx.md)函數和[CASE 語句 &#40;](../mdx/case-statement-mdx.md)只能用來傳回值或物件的 mdx&#41;不同。  
  
## <a name="examples"></a>範例  
 在下列範例中，範圍限制在 Customers 維度之 Customers Geography 階層的 Country 層級。 如果目前的量值是 Internet Sales Amount，則 Internet Sales Amount 會設定為 10：  
  
 `SCOPE ([Customer].[Customer Geography].[Country].MEMBERS);`  
  
 `IF Measures.CurrentMember IS [Measures].[Internet Sales Amount] THEN this = 10 END IF;`  
  
 `END SCOPE`;  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
