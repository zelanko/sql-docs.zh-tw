---
title: LinRegVariance （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b45328614bbefe730c815f528e82f220ad0093e9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67905508"
---
# <a name="linregvariance-mdx"></a>LinRegVariance (MDX)


  計算集合的線性回歸，並傳回與迴歸線 y = ax + b 相關聯的變異數。  
  
## <a name="syntax"></a>語法  
  
```  
  
LinRegVariance(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] ] )  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Numeric_Expression_y*  
 有效的數值運算式，這通常是傳回表示 Y 軸數值之資料格座標的多維度運算式 (MDX) 運算式。  
  
 *Numeric_Expression_x*  
 有效的數值運算式，這通常是傳回表示 X 軸數值之資料格座標的多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 線性迴歸利用最小平方法，計算迴歸線方程式 (也就是說，數點之間的最佳直線)。 迴歸線具有下列方程式，其中 a 是斜率，而 b 是截距：  
  
 y = ax+b  
  
 **LinRegVariance**函數會評估指定的 setagainst 第一個數值運算式，以取得 y 軸的值。 此函數接著會針對第二個數值運算式 (如果已指定) 來評估指定的集合，以取得 X 軸的值。 如果沒有指定第二個數值運算式，此函數會使用指定集合中的資料格目前內容，做為 X 軸的值。 Time 維度經常不指定 X 軸引數。  
  
 取得一組點之後， **LinRegVariance**函式會傳回統計變異數，以描述線性方程序與點的符合程度。  
  
> [!NOTE]  
>  **LinRegVariance**函數會忽略空的資料格或包含文字或邏輯值的資料格。 不過，此函數包括值為零的資料格。  
  
## <a name="example"></a>範例  
 下列範例會傳回統計變異數，以描述線性方程式與單位銷售量和商店銷售量值點的符合程度。  
  
```  
LinRegVariance(LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
