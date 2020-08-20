---
description: SELECT INTO (DMX)
title: SELECT INTO (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e7bc85d20ab3c1c087b6352d16777b2bb7d7dcd0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500857"
---
# <a name="select-into-dmx"></a>SELECT INTO (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  建立一個以現有採礦模型的採礦結構為基礎的採礦模型。 **SELECT INTO**語句會藉由複製架構和其他不屬於實際演算法的資訊，來建立新的採礦模型。  
  
## <a name="syntax"></a>語法  
  
```  
  
SELECT INTO <new model>   
USING <algorithm> [(<parameter list>)] [WITH DRILLTHROUGH[,] [FILTER(<expression>)]]  
FROM <existing model>  
```  
  
## <a name="arguments"></a>引數  
 *新模型*  
 所建立之新模型的唯一名稱。  
  
 *演算法*  
 資料採礦演算法的提供者定義名稱。  
  
 *參數清單*  
 選擇性。 提供者自訂之演算法參數的逗號分隔清單。  
  
 *expression*  
 在定型資料上，評估為有效篩選條件的運算式。 如需可當做篩選準則使用之運算式的詳細資訊，請參閱 [&#40;Analysis Services 資料採礦&#41;的採礦模型篩選 ](https://docs.microsoft.com/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining)。  
  
 *現有的模型*  
 要複製之現有模型的名稱。  
  
## <a name="remarks"></a>備註  
 如果現有的模型已定型，當此陳述式執行時，會自動處理新模型。 否則，新模型會保持為未處理。  
  
 只有當現有模型的結構與新模型的演算法相容時， **SELECT INTO** 語句才能運作。 因此，此陳述式最適用於快速建立與測試以相同演算法為基礎的模式。 如果您要變更演算法類型，新的演算法必須支援現有模型中每個資料行的資料類型，否則在處理模型時，可能會發生錯誤。  
  
 **WITH 鑽取**子句可讓您在新的採礦模型上進行鑽取。 唯有您建立模型時，才能啟用鑽研。  
  
## <a name="example-1-altering-the-parameters-of-the-model"></a>範例 1：變更模型的參數  
 下列範例 `TM_Clustering` 會根據您在「 [基本資料採礦」教學](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)課程中建立的現有「採礦模型」建立新的「採礦模型」。 在新的模型中，CLUSTER_COUNT 參數經過修改，使新模型中最多會有 5 個群集。 相反地，現有的模型使用預設值 10。  
  
```  
SELECT * INTO [New_Clustering]  
USING [Microsoft_Clustering] (CLUSTER_COUNT = 5)   
FROM [TM Clustering]  
```  
  
## <a name="example-2-adding-a-filter-to-the-model"></a>範例 2：將篩選器加入到模型中  
 下列範例根據現有的採礦模型建立新的採礦模型，並在模型上加入篩選器。 篩選器會將定型資料限制為僅住在特定區域的客戶。  
  
```  
SELECT * INTO [Clustering Europe Region]  
USING [Microsoft_Clustering] WITH FILTER(Region='Europe')  
FROM [TM Clustering]  
```  
  
> [!NOTE]  
>  套用到案例資料表的篩選器可以使用 SELECT INTO 陳述式進行變更，如此範例所示，不過，如果原始模型在巢狀資料表上包含篩選器，則無法使用此語法變更或移除巢狀資料表篩選器，但是會從原始模型，以原樣複製。 若要利用巢狀資料表上的不同篩選器建立模型，請使用 ALTER STRTUCTURE...ADD MODEL 語法。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40;DMX&#41; 資料定義語句](../dmx/dmx-statements-data-definition.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 資料動作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
