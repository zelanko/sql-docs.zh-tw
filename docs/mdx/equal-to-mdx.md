---
title: = （等於）（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 189facb54de244ff220b41ec08c8b02faf5a2c27
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68139318"
---
# <a name="-equal-to-mdx"></a>=  (等於) (MDX)


  執行比對作業，判定某個多維度運算式 (MDX) 運算式的值是否等於另一個 MDX 運算式的值。  
  
> [!NOTE]  
>  若要比較物件，請使用[IS &#40;MDX&#41;](../mdx/is-mdx.md)運算子。 例如，當您正在檢查查詢軸上的目前成員是否為特定成員時，請使用 IS 運算子。  
  
## <a name="syntax"></a>語法  
  
```  
  
MDX_Expression = MDX_Expression   
```  
  
#### <a name="parameters"></a>參數  
 *MDX_Expression*  
 有效的 MDX 運算式。  
  
## <a name="return-value"></a>傳回值  
 布林值根據以下條件而定：  
  
-   如果第一個參數的值等於第二個參數的值，**則為 true** 。  
  
-   如果第一個參數的值不等於第二個參數的值，則**為 false** 。  
  
-   如果兩個參數都是 null，或其中一個參數為 null，另一個參數為0，則**為 true** 。  
  
## <a name="examples"></a>範例  
 下列查詢顯示這些條件的範例：  
  
 `With`  
  
 `--Returns true`  
  
 `Member [Measures].bool1 as 1=1`  
  
 `--Returns false`  
  
 `Member [Measures].bool2 as 1=0`  
  
 `--Returns true`  
  
 `Member [Measures].bool3 as null=null`  
  
 `--Returns true`  
  
 `Member [Measures].bool4 as 0=null`  
  
 `--Returns false`  
  
 `Member [Measures].bool5 as 1=null`  
  
 `Select {[Measures].bool1,[Measures].bool2,[Measures].bool3,[Measures].bool4,[Measures].bool5}`  
  
 `On 0`  
  
 `From [Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 運算子參考 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
