---
title: "* （乘）(MDX) |Microsoft 文件"
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
- '*'
dev_langs:
- kbMDX
helpviewer_keywords:
- '* (multiply operator)'
- multiply operator (*)
ms.assetid: 073fd098-65bd-4a30-81dd-d233d007490d
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d47373a1b24eda4084218daaee731f6ebd16860a
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="-multiply-mdx"></a>* (乘) (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  執行兩個數目相乘的算術運算。  
  
## <a name="syntax"></a>語法  
  
```  
  
Numeric_Expression * Numeric_Expression  
```  
  
#### <a name="parameters"></a>參數  
 *Numeric_Expression*  
 傳回數值的有效多維度運算式 (MDX) 運算式。  
  
## <a name="return-value"></a>傳回值  
 具有較高優先順序之參數的資料類型的值。  
  
## <a name="remarks"></a>備註  
 兩個運算式的資料類型必須相同，或者其中一個運算式必須可以用隱含方式轉換為另一個運算式的資料類型。 如果一個運算式評估為 Null 值，運算子就會傳回 Null 值。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 運算子參考 &#40;MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  

