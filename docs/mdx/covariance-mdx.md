---
title: 共變數 (MDX) |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 06b86c47b5da75c44d528f77a60e8168fd8b2260
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34577880"
---
# <a name="covariance-mdx"></a>Covariance (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  使用偏誤母體公式 (除以 x-y 配對數)，在集合評估後傳回 x-y 配對值的母體共變數。  
  
## <a name="syntax"></a>語法  
  
```  
  
Covariance(Set_Expression,Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Numeric_Expression_y*  
 有效的數值運算式，這通常是傳回表示 Y 軸數值之資料格座標的多維度運算式 (MDX) 運算式。  
  
 *Numeric_Expression_x*  
 有效的數值運算式，這通常是傳回表示 X 軸數值之資料格座標的多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **共變數**函式評估指定的集合，針對第一個數值運算式，以取得 y 軸的值。 此函數接著會針對第二個數值運算式 (如果已指定) 來評估指定的集合，以取得 X 軸的值集合。 如果未指定第二個數值 expressionis，此函數會使用指定集合中的資料格目前內容做為值當做 x 軸。  
  
 **共變數**函數使用偏誤的母體公式。 這是相對於[CovarianceN](../mdx/covariancen-mdx.md)使用非偏誤的母體公式 （除以 x-y 配對數，再減 1） 的函式。  
  
> [!NOTE]  
>  **共變數**函式會忽略空白資料格包含文字或忽略邏輯值。 不過，此函數包括值為零的資料格。  
  
## <a name="example"></a>範例  
 下列範例示範如何使用 Covariance 函數：  
  
```  
WITH   
MEMBER [Measures].[CovarianceDemo] AS  
COVARIANCE([Date].[Date].[Date].Members, [Measures].[Internet Sales Amount], [Measures].[Internet Order Count])   
SELECT {[Measures].[CovarianceDemo]} ON 0   
FROM  
[Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
