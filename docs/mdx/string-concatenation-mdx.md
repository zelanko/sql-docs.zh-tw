---
title: + （字串串連）（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4d5f2316e3af5ce3c925ef71e1da5baf5bab868d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036847"
---
# <a name="-string-concatenation-mdx"></a>+ (字串串連) (MDX)


  執行字串作業，串連兩個以上的字元字串、Tuple 或字串與 Tuple 的組合。  
  
## <a name="syntax"></a>語法  
  
```  
  
String_Expression + String_Expression  
```  
  
#### <a name="parameters"></a>參數  
 *String_Expression*  
 傳回字串值的有效多維度運算式 (MDX) 運算式。  
  
## <a name="return-value"></a>傳回值  
 具有較高優先順序之參數的資料類型的值。  
  
## <a name="remarks"></a>備註  
 兩個運算式的資料類型必須相同，或者其中一個運算式必須可以用隱含方式轉換為另一個運算式的資料類型。 如果一個運算式評估為 Null 值，則運算子會傳回其他運算式的結果。  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 運算子參考 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
