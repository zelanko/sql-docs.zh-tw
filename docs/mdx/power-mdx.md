---
title: ^ (Power) (MDX) |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e360b1b70a6bcbbfc3d7dd2c9bde496d5d3cad87
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580940"
---
# <a name="-power-mdx"></a>^ (乘冪) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  執行算術運算，將一個數字乘至另一個數字的乘冪。  
  
## <a name="syntax"></a>語法  
  
```  
  
Numeric_Expression ^ Numeric_Expression  
```  
  
#### <a name="parameters"></a>參數  
 *Numeric_Expression*  
 傳回數值的有效多維度運算式 (MDX) 運算式。  
  
## <a name="return-value"></a>傳回值  
 具有較高優先順序之參數的資料類型的值。  
  
## <a name="remarks"></a>備註  
 兩個運算式的資料類型必須相同，或者其中一個運算式必須可以用隱含方式轉換為另一個運算式的資料類型。 如果一個運算式評估為 Null 值，運算子就會傳回 Null 值。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 運算子參考&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
