---
title: "MeasureGroupMeasures (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- MeasureGroupMeasures function
ms.assetid: 69d9b205-1ca7-4741-9ca9-c7926bc87ead
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 17f8ba22b30fbfe925ae219a9f13bbdc5a9f1be0
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="measuregroupmeasures-mdx"></a>MeasureGroupMeasures (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回屬於指定量值群組的量值集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
MEASUREGROUPMEASURES(MeasureGroupName)  
```  
  
## <a name="arguments"></a>引數  
 *MeasureGroupName*  
 包含量值群組名稱的有效字串運算式，可從中擷取量值集合。  
  
## <a name="remarks"></a>備註  
 指定的字串必須完全符合量值群組名稱。 含空格的量值群組名稱不需要方括號。  
  
## <a name="example"></a>範例  
 下列範例會傳回 Adventure Works Cube 中 Internet Sales 量值群組的所有量值。  
  
```  
SELECT MeasureGroupMeasures('Internet Sales') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

