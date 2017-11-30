---
title: "LinRegR2 (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: LINREGR2
dev_langs: kbMDX
helpviewer_keywords: LinRegR2 function
ms.assetid: 770d1e1e-d034-43f1-82b1-3f91d52c86be
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: dd86db8226d06fa180d352c5296aacf14eb6d4f4
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="linregr2-mdx"></a>LinRegR2 (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  計算集合的線性迴歸，並傳回決定係數，R<sup>2</sup>。  
  
## <a name="syntax"></a>語法  
  
```  
  
LinRegR2(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
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
  
 **LinRegR2**函式會評估指定的 setagainst 第一個數值 expressionto 取得 y 軸的值。 此函數接著會針對第二個數值運算式 (如果已指定) 來評估指定的集合，以取得 X 軸的值。 如果未指定第二個數值 expressionis，此函數會使用指定集合中的資料格目前內容的值當做 x 軸。 不指定 x axisargument 經常搭配時間維度。  
  
 取得數點之後, **LinRegR2**函式會傳回統計 R<sup>2</sup> ，以描述線性方程式與點的符合程度。  
  
> [!NOTE]  
>  **LinRegR2**函式會忽略空白資料格包含文字或邏輯值。 不過，此函數包括值為零的資料格。  
  
## <a name="example"></a>範例  
 下列範例會傳回統計 R<sup>2</sup>所描述的線性迴歸方程式，銷售單位和商店銷售量值點的符合程度。  
  
```  
LinRegR2(LastPeriods(10), [Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>請參閱  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
