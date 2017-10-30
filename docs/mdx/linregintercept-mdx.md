---
title: "LinRegIntercept (MDX) |Microsoft 文件"
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
- LINREGINTERCEPT
dev_langs:
- kbMDX
helpviewer_keywords:
- LinRegIntercept function
ms.assetid: 6ef2527d-e519-4b66-b67e-131c5831234e
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 59e23a316aa99612861a3181b1254b04c8a09014
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="linregintercept-mdx"></a>LinRegIntercept (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  計算集合的線性迴歸，並傳回迴歸線中的 x-intercept 值 y = ax + b。  
  
## <a name="syntax"></a>語法  
  
```  
  
LinRegIntercept(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
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
  
 **LinRegIntercept**函式評估指定的集合，針對第一個數值運算式，以取得 y 軸的值。 此函數接著會針對第二個數值運算式 (如果已指定) 來評估指定的集合，以取得 X 軸的值。 如果沒有指定第二個數值運算式，此函數會使用指定集合中的資料格目前內容，做為 X 軸的值。 Time 維度經常不指定 X 軸引數。  
  
 取得數點之後, **LinRegIntercept**函式會傳回迴歸線 (先前方程式中 b) 的截距。  
  
> [!NOTE]  
>  **LinRegIntercept**函式會忽略空白資料格包含文字或邏輯值。 不過，此函數包括值為零的資料格。  
  
## <a name="example"></a>範例  
 下列範例會為銷售單位和商店銷售量值傳回迴歸線的截距。  
  
```  
LinRegIntercept(LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

