---
title: 拆分（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 17f1233310ce8b070e12fbf25dca0e256ff34664
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68070743"
---
# <a name="divide-dmx"></a>(除) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  執行算術運算，將一個數字除以另一個數字。  
  
## <a name="syntax"></a>語法  
  
```  
  
Dividend / Divisor  
```  
  
#### <a name="parameters"></a>參數  
 *股利*  
 有效的資料採礦延伸模組 (DMX) 運算式，會傳回數值。  
  
 *除數*  
 傳回數值的有效 DMX 運算式。  
  
## <a name="return-value"></a>傳回值  
 具有較高優先順序之參數資料類型的值。  
  
## <a name="remarks"></a>備註  
 這個運算子傳回的值是第一個運算式除以第二個運算式的商數。  
  
 兩個運算式的資料類型必須相同，或者其中一個運算式必須可以用隱含方式轉換為另一個運算式的資料類型。 如果除數評估為 Null 值，運算子就會引發錯誤。 如果除數與被除數都評估為 Null 值，運算子就會傳回 Null 值。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;DMX&#41;的算術運算子](../dmx/operators-arithmetic.md)   
 [DMX&#41; Operator Reference &#40;的資料採礦延伸模組](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [DMX&#41;&#40;的運算子](../dmx/operators-dmx.md)   
 [除法 &#40;SSIS 運算式&#41;](../integration-services/expressions/divide-ssis-expression.md)   
 [&#40;除&#41; &#40;Transact-sql&#41;](../t-sql/language-elements/divide-transact-sql.md)  
  
  
