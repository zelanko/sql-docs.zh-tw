---
title: "= （等於） (MDX) |Microsoft 文件"
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
- =
dev_langs:
- kbMDX
helpviewer_keywords:
- equals operator (=)
- = (equals operator)
ms.assetid: 5e1f3b58-a646-4fc1-a3f1-19090a5437b7
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9e446cf812f57a3cc3df74728b74c072d1b089bc
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="-equal-to-mdx"></a>=  (等於) (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  執行比對作業，判定某個多維度運算式 (MDX) 運算式的值是否等於另一個 MDX 運算式的值。  
  
> [!NOTE]  
>  若要比較的物件，使用[IS & #40;MDX & #41;](../mdx/is-mdx.md)運算子。 例如，當您正在檢查查詢軸上的目前成員是否為特定成員時，請使用 IS 運算子。  
  
## <a name="syntax"></a>語法  
  
```  
  
MDX_Expression = MDX_Expression   
```  
  
#### <a name="parameters"></a>參數  
 *MDX_Expression*  
 有效的 MDX 運算式。  
  
## <a name="return-value"></a>傳回值  
 布林值根據以下條件而定：  
  
-   **true**的第一個參數的值是否等於第二個參數的值。  
  
-   **false**的第一個參數的值是否不等於第二個參數的值。  
  
-   **true**如果這兩個參數都是 null，或一個參數是 null，且另一個參數為 0。  
  
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
 [MDX 運算子參考 & #40;MDX & #41;](../mdx/mdx-operator-reference-mdx.md)  
  
  

