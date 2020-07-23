---
title: 從 &lt; 模型選取 &gt; （DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 43a7157c5ec7889b2f8cb7018423d909f3db3cb7
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970520"
---
# <a name="select-from-ltmodelgt-dmx"></a>從 &lt; 模型選取 &gt; （DMX）
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  執行空白預測聯結，傳回指定資料行之最可能的一或多個值。 只會使用採礦模型中的內容建立預測。  
  
## <a name="syntax"></a>語法  
  
```  
  
SELECT <expression list> [TOP <n>] FROM <model>   
[WHERE <condition list>]   
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>引數  
 *運算式清單*  
 運算式、預測或純預測資料行的逗號分隔清單。  
  
 *n*  
 選擇性。 指定要傳回多少資料列的整數。  
  
 *model*  
 模型識別碼。  
  
 *條件清單*  
 選擇性。 限制從資料行清單傳回之值的條件。  
  
 *expression*  
 選擇性。 傳回純量值的運算式。  
  
## <a name="remarks"></a>備註  
 *運算式清單*中的資料行必須定義為 [預測] 或 [僅預測]，或與可預測資料行相關。  
  
## <a name="naive-bayes-example"></a>貝氏機率分類範例  
 下列範例在 Bike Buyer 資料行執行空白預測聯結，並傳回 TM Naive Bayes 採礦模型中最可能的狀態。  
  
```  
SELECT ([Bike Buyer]) FROM [TM_Naive_Bayes]  
```  
  
## <a name="time-series-example"></a>時間序列範例  
 下列範例會在 Forecasting 模型中的 Amount 資料行上執行預測，傳回後 4 期狀態。 Model Region 資料行將自行車車型與區域結合至單一識別碼。 查詢會使用[PredictTimeSeries &#40;DMX&#41;](../dmx/predicttimeseries-dmx.md)函數來執行預測。  
  
```  
SELECT [Model Region], PredictTimeSeries(Amount, 4)   
FROM Forecasting  
```  
  
## <a name="see-also"></a>另請參閱  
 [選取 &#40;DMX&#41;](../dmx/select-dmx.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 資料定義語句](../dmx/dmx-statements-data-definition.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 資料動作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
