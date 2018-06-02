---
title: '&lt;&gt; （不等於）(MDX) |Microsoft 文件'
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0ccccc64c4a6b2048a50ac1099c4a31b07537ae0
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580550"
---
# <a name="ltgt-not-equal-to-mdx"></a>&lt;&gt; （不等於）(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
  
