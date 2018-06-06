---
title: + （新增）(DMX) |Microsoft 文件
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- + (add)
- add operator (+)
ms.assetid: 35e7636f-814c-44c3-94a7-384a305d65ea
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: b28cf10467c7c321c60ba0a433fc1c883d58d403
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="-add-dmx"></a>+ (加) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  執行算術作業，將兩個數加在一起。  
  
## <a name="syntax"></a>語法  
  
```  
  
Numeric_Expression + Numeric_Expression  
```  
  
#### <a name="parameters"></a>參數  
 *Numeric_Expression*  
 有效的資料採礦延伸模組 (DMX) 運算式，會傳回數值。  
  
## <a name="return-value"></a>傳回值  
 具有較高優先順序之參數資料類型的值。  
  
## <a name="remarks"></a>備註  
 兩個運算式的資料類型必須相同，或者其中一個運算式必須可以用隱含方式轉換為另一個運算式的資料類型。 如果一個運算式評估為 Null 值，則運算子會傳回其他運算式的結果。  
  
## <a name="see-also"></a>另請參閱  
 [算術運算子&#40;DMX&#41;](../dmx/operators-arithmetic.md)   
 [資料採礦延伸模組&#40;DMX&#41;運算子參考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [運算子&#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
