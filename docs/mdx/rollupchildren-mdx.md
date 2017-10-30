---
title: "RollupChildren (MDX) |Microsoft 文件"
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
- ROLLUPCHILDREN
dev_langs:
- kbMDX
helpviewer_keywords:
- RollupChildren function
ms.assetid: 6f092540-067d-443f-b631-8523836a0d86
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b29a351d8425d235adc29b8a5b997915b70de047
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="rollupchildren-mdx"></a>RollupChildren (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回由積存特定成員子成員的值，利用指定的一元 (Unary) 運算子所產生的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
RollupChildren(Member_Expression, Unary_Operator)   
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
 *Unary_Operator*  
 指定一元運算子的有效字串運算式。  
  
## <a name="remarks"></a>備註  
 **RollupChildren**函式會彙總指定的成員，使用指定的一元運算子的子系的值。  
  
 下表描述了對此函數有效的一元運算子。  
  
|運算子|結果|  
|--------------|------------|  
|**+**|總計 = 總計 + 目前的子系|  
|**-**|總計 = 總計 - 目前的子系|  
|**\***|總計 =總計 * 目前的子系|  
|**/**|總計 =總計 / 目前的子系|  
|**%**|總計 = (總計 / 目前的子系) * 100|  
|**~**|不會在積存中使用子系。 它的值會被忽略。|  
  
 如果成員屬性中的運算子不在上面的清單中，則會發生錯誤。 評估的順序是由同層級(Sibling) 的順序決定，而不是運算子的優先順序。  
  
## <a name="example"></a>範例  
 下列範例使用名為 "Alternate Rollup Operator" 的成員屬性，其包含一元運算子的替代值，以便用交替方式積存 Account 維度中 Net Profit 階層的子系。 這個成員屬性不存在於 Adventure Works Cube，但可予以建立。 這種使用**RollupChildren**函式無法編列預算的應用程式中用於假設分析。  
  
```  
RollupChildren  
   ( [Account].[Net Profit]  
   , [Account].CurrentMember.Properties ('Alternate Rollup Operator') )  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

