---
title: "Lag (MDX) |Microsoft 文件"
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
- LAG
dev_langs:
- kbMDX
helpviewer_keywords:
- Lag function
ms.assetid: 08c704ea-35d8-44ee-abe5-93bd24b99906
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: eedeae82c5b7566f0c59a6876fc6743c61794de0
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="lag-mdx"></a>Lag (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回成員層級中，在特定成員之前特定幾個位置的成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
Member_Expression.Lag(Index)   
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
 *索引*  
 指定落後的成員位置數目之有效數值運算式。  
  
## <a name="remarks"></a>備註  
 層級內的成員位置是由屬性階層的自然順序決定。 位置的編號是以零為基底。  
  
 如果指定的落後是零，**延隔**函式會傳回指定的成員本身。  
  
 如果指定的落後是負數，**延隔**函式會傳回後續成員。  
  
 `Lag(1)`相當於[PrevMember](../mdx/prevmember-mdx.md)函式。 `Lag(-1)`相當於[NextMember](../mdx/nextmember-mdx.md)函式。  
  
 **延隔**函數很相似[導致](../mdx/lead-mdx.md)函式中，不同處在於**導致**函式會以相反的方向，以尋找**延隔**函式。 也就是說，`Lag(n)` 相當於 `Lead(-n)`。  
  
## <a name="example"></a>範例  
 下列範例會傳回 2001 年 12 月的值：  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lag(2) ON 0  
FROM [Adventure Works]  
  
```  
  
 下列範例會傳回 2002 年 3 月的值：  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lag(-1) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

