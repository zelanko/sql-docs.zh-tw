---
title: "目前 (MDX) |Microsoft 文件"
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
- CURRENT
dev_langs:
- kbMDX
helpviewer_keywords:
- Current function
ms.assetid: 6f689742-f9b6-4339-a691-31ff28582c36
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 0e12e6549e02161589c769610625c82243decd17
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="current-mdx"></a>Current (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  反覆運算時從一個集合傳回目前的 Tuple。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set_Expression.Current   
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 在反覆運算期間的每個步驟，進行運算的 Tuple 就是目前的 Tuple。 **目前**函式會傳回那個 tuple。 只有在集合上反覆運算時，這個函數才是有效的。  
  
 逐一查看集合的 MDX 函數包括[產生](../mdx/generate-mdx.md)函式。  
  
> [!NOTE]  
>  這個函數只能搭配已命名的集合 (使用集合別名或定義命名集) 使用。  
  
## <a name="examples"></a>範例  
 下列範例示範如何使用**目前**函式內**產生**:  
  
 `WITH`  
  
 `//Creates a set of tuples consisting of all Calendar Years crossjoined with`  
  
 `//all Product Categories`  
  
 `SET MyTuples AS CROSSJOIN(`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS,`  
  
 `[Product].[Category].[Category].MEMBERS)`  
  
 `//Iterates through each tuple in the set and returns the name of the Calendar`  
  
 `//Year in each tuple`  
  
 `MEMBER MEASURES.CURRENTDEMO AS`  
  
 `GENERATE(MyTuples, MyTuples.CURRENT.ITEM(0).NAME, ", ")`  
  
 `SELECT MEASURES.CURRENTDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

