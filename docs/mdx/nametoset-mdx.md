---
title: "NameToSet (MDX) |Microsoft 文件"
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
- NAMETOSET
dev_langs:
- kbMDX
helpviewer_keywords:
- NameToSet function
ms.assetid: e02e17d5-4309-49cb-84c7-5b445ac2bd94
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b615ddfdf8698e1d495e6d6070e489aa448d4c96
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="nametoset-mdx"></a>NameToSet (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回包含多維度運算式 (MDX) 指定成員的集合 –格式化字串。  
  
## <a name="syntax"></a>語法  
  
```  
  
NameToSet(Member_Name)   
```  
  
## <a name="arguments"></a>引數  
 *Member_Name*  
 代表成員名稱的有效字串運算式。  
  
## <a name="remarks"></a>備註  
 如果指定的成員名稱存在， **NameToSet**函式會傳回包含該成員的集合。 否則，函數會傳回空的集合。  
  
> [!NOTE]  
>  指定的成員名稱只能是成員名稱，不能是成員運算式。 若要使用成員運算式，請參閱[StrToSet &#40;MDX &#41;](../mdx/strtoset-mdx.md).  
  
## <a name="example"></a>範例  
 下列範例會傳回指定成員名稱的預設量值。  
  
```  
SELECT NameToSet('[Date].[Calendar].[July 2001]') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

