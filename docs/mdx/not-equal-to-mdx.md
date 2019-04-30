---
title: '&lt;&gt; （不等於）(MDX) |Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ac3241e7d6acd8ba883cdd59f9410f4a0fd9187d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63277520"
---
# <a name="ltgt-not-equal-to-mdx"></a>&lt;&gt; （不等於）(MDX)


  執行比對作業，判定某個多維度運算式 (MDX) 運算式的值是否不等於另一個 MDX 運算式的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
MDX_Expression <> MDX_Expression  
```  
  
#### <a name="parameters"></a>參數  
 *MDX_Expression*  
 有效的 MDX 運算式。  
  
## <a name="return-value"></a>傳回值  
 布林值根據以下條件而定：  
  
-   **true**如果這兩個參數都為非 null，而且第一個參數不等於第二個參數。  
  
-   **false**如果這兩個參數都為非 null，而且第一個參數等於第二個參數。  
  
-   Null，如果有一個參數或兩個參數都評估為 Null 值。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 運算子參考&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
