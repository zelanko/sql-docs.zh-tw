---
description: Lag (DMX)
title: DMX)  (延隔 |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4e7aa504c3afd236ddd748a7ee81cbbb6cf90b7c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466560"
---
# <a name="lag-dmx"></a>Lag (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  傳回目前案例的日期與培訓集的最後日期之間的時間配量。  
  
## <a name="syntax"></a>語法  
  
```  
  
Lag()  
```  
  
## <a name="return-type"></a>傳回類型  
 interger 類型的純量值。  
  
## <a name="remarks"></a>備註  
 如果在索引鍵時間資料行位於嵌套資料表內的模型上使用 **Lag** 函數，則函數必須位於語句的子 select 內。  
  
## <a name="examples"></a>範例  
 下列範例傳回前 12 個月用來培訓模型之資料內的案例。  
  
```  
SELECT * FROM [Forecasting].CASES  
WHERE Lag() < 12  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40;DMX&#41; 函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41;函數 &#40;](../dmx/functions-dmx.md)   
 [&#40;DMX&#41;的一般預測函數 ](../dmx/general-prediction-functions-dmx.md)  
  
  
