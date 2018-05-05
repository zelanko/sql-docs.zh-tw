---
title: SetToArray (MDX) |Microsoft 文件
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SETTOARRAY
dev_langs:
- kbMDX
helpviewer_keywords:
- SetToArray function
ms.assetid: e408c626-3a2a-4ce9-aeb4-247301334893
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 8d444aa9a01867cc6ba91d340ddaf7a6c7005764
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="settoarray-mdx"></a>SetToArray (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  將一個 (含) 以上集合轉換成陣列，以便用在使用者自訂的函數中。  
  
## <a name="syntax"></a>語法  
  
```  
  
SetToArray(Set_Expression1 [ ,Set_Expression2,...n ][ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression1*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Set_Expression2*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Numeric_Expression*  
 有效的數值運算式，這通常是傳回數字之資料格座標的多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **SetToArray**函式會將一或多個集合轉換成陣列，以便在使用者定義函數中使用。 轉換得到的陣列中之維度數目跟指定的集合數目一樣。  
  
 選擇性的數值運算式可以提供陣列資料格中的值。 如果沒有指定數值運算式，則會在目前內容中評估集合的交叉聯結。  
  
 轉換得到的陣列中之資料格座標與集合在清單中的位置是相對應的。 例如，有 `SA`、`SB` 與 `SC` 三個集合。 每個集合都有兩個元素。 MDX 陳述式 `SetToArray(SA, SB, SC)` 會建立以下三個維度陣列：  
  
```  
(SA1, SB1, SC1) (SA2, SB1, SC1) (SA1, SB2, SC1) (SA2, SB2, SC1)   
(SA1, SB1, SC2) (SA2, SB1, SC2) (SA1, SB2, SC2) (SA2, SB2, SC2)   
```  
  
> [!NOTE]  
>  傳回型別**SetToArray**函式是 VARIANT 類型 VT_ARRAY。 因此，輸出的**SetToArray**函式應使用只當做使用者定義函數的輸入。  
  
## <a name="example"></a>範例  
 下列範例會傳回陣列。  
  
```  
SetToArray([Geography].[Geography].Members, [Measures].[Internet Sales Amount])  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 & #40;MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
