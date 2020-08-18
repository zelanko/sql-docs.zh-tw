---
description: (除) (DMX)
title: " (將)  (DMX) Microsoft Docs"
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2249701d074f12e0fc4dc3383d2e62b31ac275f6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88414064"
---
# <a name="divide-dmx"></a>(除) (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  執行算術運算，將一個數字除以另一個數字。  
  
## <a name="syntax"></a>語法  
  
```  
  
Dividend / Divisor  
```  
  
#### <a name="parameters"></a>參數  
 *股利*  
 有效的資料採礦延伸模組 (DMX) 運算式，會傳回數值。  
  
 *因數*  
 傳回數值的有效 DMX 運算式。  
  
## <a name="return-value"></a>傳回值  
 具有較高優先順序之參數資料類型的值。  
  
## <a name="remarks"></a>備註  
 這個運算子傳回的值是第一個運算式除以第二個運算式的商數。  
  
 兩個運算式的資料類型必須相同，或者其中一個運算式必須可以用隱含方式轉換為另一個運算式的資料類型。 如果除數評估為 Null 值，運算子就會引發錯誤。 如果除數與被除數都評估為 Null 值，運算子就會傳回 Null 值。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;DMX&#41;的算術運算子 ](../dmx/operators-arithmetic.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 運算子參考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [DMX &#40;的運算子&#41;](../dmx/operators-dmx.md)   
 [&#40;SSIS 運算式相除&#41;](../integration-services/expressions/divide-ssis-expression.md)   
 [&#40;除以&#41; &#40;Transact-sql&#41;](../t-sql/language-elements/divide-transact-sql.md)  
  
  
