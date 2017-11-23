---
title: "LinRegSlope (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: LINREGSLOPE
dev_langs: kbMDX
helpviewer_keywords: LinRegSlope function
ms.assetid: dc61f941-b25d-4eef-9b25-75e03a1dd6de
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 5fa20727d25c908ad663461cf9a0b639ac1e74d5
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="linregslope-mdx"></a>LinRegSlope (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  計算集合的線性迴歸，並傳回迴歸線的斜率值 y = ax + b。  
  
## <a name="syntax"></a>語法  
  
```  
  
LinRegSlope(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Numeric_Expression_y*  
 有效的數值運算式，這通常是傳回表示 Y 軸數值之資料格座標的多維度運算式 (MDX) 運算式。  
  
 *Numeric_Expression_x*  
 有效的數值運算式，這通常是傳回表示 X 軸數值之資料格座標的多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 線性迴歸利用最小平方法，計算迴歸線方程式 (也就是說，數點之間的最佳直線)。 迴歸線具有下列方程式，其中為斜率，b 是截距：  
  
 y = ax+b  
  
 **LinRegSlope**函式評估指定的集合，針對第一個數值運算式，以取得 y 軸的值。 此函數接著會針對第二個數值運算式 (如果已指定) 來評估指定的集合運算式，以取得 X 軸的值。 如果沒有指定第二個數值運算式，此函數會使用指定集合中的資料格目前內容，做為 X 軸的值。 Time 維度經常不指定 X 軸引數。  
  
 取得數點之後, **LinRegSlope**函式會傳回迴歸線的斜率 (先前方程式中)。  
  
> [!NOTE]  
>  **LinRegSlope**函式會忽略空白資料格包含文字或邏輯值。 不過，此函數包括值為零的資料格。  
  
## <a name="example"></a>範例  
 下列範例會為銷售單位和商店銷售量值傳回迴歸線的斜率。  
  
```  
LinRegSlope(LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>請參閱＜  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
