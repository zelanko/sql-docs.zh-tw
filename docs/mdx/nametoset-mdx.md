---
title: NameToSet (MDX) |Microsoft 文件
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
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
ms.openlocfilehash: 365181e10812a1f28bf39385a75215e6be304b23
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="nametoset-mdx"></a>NameToSet (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
>  指定的成員名稱只能是成員名稱，不能是成員運算式。 若要使用成員運算式，請參閱[StrToSet &#40;MDX&#41;](../mdx/strtoset-mdx.md)。  
  
## <a name="example"></a>範例  
 下列範例會傳回指定成員名稱的預設量值。  
  
```  
SELECT NameToSet('[Date].[Calendar].[July 2001]') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 & #40;MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
