---
title: "不 (MDX) |Microsoft 文件"
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
- NOT
dev_langs:
- kbMDX
helpviewer_keywords:
- NOT operator [MDX]
ms.assetid: c11bd3b0-54b3-4a6d-babc-6067722194db
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b6da446a370065c3782ac3c76445988d266b60d7
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="not-mdx"></a>NOT (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在數值運算式上執行邏輯否定。  
  
## <a name="syntax"></a>語法  
  
```  
  
NOT Expression1  
```  
  
#### <a name="parameters"></a>參數  
 *Expression1*  
 傳回數值的有效多維度運算式 (MDX) 運算式。  
  
## <a name="return-value"></a>傳回值  
 布林值，傳回**false**如果引數評估為**true**，否則**true**。  
  
## <a name="remarks"></a>備註  
 **不**運算子會將運算式視為布林值 (零 （0) 做為**false**，否則**true**) 運算子執行邏輯否定之前。 下表將說明如何**不**運算子執行邏輯否定。  
  
|*Expression1*|傳回值|  
|-------------------|------------------|  
|**true**|**false**|  
|**false**|**true**|  
  
## <a name="see-also"></a>另請參閱  
 [MDX 運算子參考 &#40;MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  

