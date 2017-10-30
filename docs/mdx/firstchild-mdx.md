---
title: "FirstChild (MDX) |Microsoft 文件"
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
- FIRSTCHILD
dev_langs:
- kbMDX
helpviewer_keywords:
- FirstChild function
ms.assetid: 3c19a169-7658-4b31-93a9-85f74225ba05
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b003d5df78f2387b54bc306c4edb2bdb2c1beadf
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="firstchild-mdx"></a>FirstChild (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回指定之成員的第一個子系。  
  
## <a name="syntax"></a>語法  
  
```  
  
Member_Expression.FirstChild   
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
### <a name="example"></a>範例  
 下列查詢會傳回 Fiscal 階層中 2003 會計年度的第一個子系，也就是 Fiscal Year 2003 的上半年度。  
  
```  
SELECT [Date].[Fiscal].[Fiscal Year].&[2003].FirstChild ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [LastChild &#40;MDX &#41;](../mdx/lastchild-mdx.md)   
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

