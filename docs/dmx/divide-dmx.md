---
title: （除法）(DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8ab2b355c551b868cec3ee4329460f8bb0532236
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37972664"
---
# <a name="divide-dmx"></a>（除法）(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  執行算術運算，將一個數字除以另一個數字。  
  
## <a name="syntax"></a>語法  
  
```  
  
Dividend / Divisor  
```  
  
#### <a name="parameters"></a>參數  
 *被除數*  
 有效的資料採礦延伸模組 (DMX) 運算式，會傳回數值。  
  
 *除數*  
 傳回數值的有效 DMX 運算式。  
  
## <a name="return-value"></a>傳回值  
 具有較高優先順序之參數資料類型的值。  
  
## <a name="remarks"></a>備註  
 這個運算子傳回的值是第一個運算式除以第二個運算式的商數。  
  
 兩個運算式的資料類型必須相同，或者其中一個運算式必須可以用隱含方式轉換為另一個運算式的資料類型。 如果除數評估為 Null 值，運算子就會引發錯誤。 如果除數與被除數都評估為 Null 值，運算子就會傳回 Null 值。  
  
## <a name="see-also"></a>另請參閱  
 [算術運算子&#40;DMX&#41;](../dmx/operators-arithmetic.md)   
 [資料採礦延伸模組&#40;DMX&#41;運算子參考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [運算子&#40;DMX&#41;](../dmx/operators-dmx.md)   
 [將&#40;SSIS 運算式&#41;](../integration-services/expressions/divide-ssis-expression.md)   
 [&#40;將&#41; &#40;TRANSACT-SQL&#41;](../t-sql/language-elements/divide-transact-sql.md)  
  
  
