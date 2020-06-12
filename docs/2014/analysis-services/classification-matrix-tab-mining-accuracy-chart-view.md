---
title: 分類矩陣索引標籤（挖掘精確度圖表視圖） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.accuracychart.confusionmatrix.f1
ms.assetid: 85d5a047-d656-41e0-8a31-400271c2a620
author: minewiskan
ms.author: owend
ms.openlocfilehash: d202d552b25095d0d0845ff64f9c0e289f7bba0e
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527494"
---
# <a name="classification-matrix-tab-mining-accuracy-chart-view"></a>分類矩陣索引標籤 (採礦精確度圖表檢視)
  [**分類矩陣**] 索引標籤會顯示 [資料**行對應**] 索引標籤上 [模型] 方格中選取之每個模型的分類矩陣。只有在 [資料**行對應**] 索引標籤中選取的可預測資料行不是連續的情況時，才可以使用分類矩陣。 如需 [**分類矩陣**] 索引標籤的詳細描述，請參閱[測試和驗證 &#40;資料採礦&#41;](data-mining/testing-and-validation-data-mining.md)。  
  
## <a name="options"></a>選項  
 **複製**  
 將每個分類矩陣的內容複製到剪貼簿。  
  
 **\<model>的計數\< predictable column>**  
 顯示採礦結構中之每個採礦模型的分類矩陣。 矩陣包含下列資料行：  
  
|值|描述|  
|-----------|-----------------|  
|**預測的**|包含可預測資料行之每個狀態的資料列。|  
|**\<states>實際**|可預測資料行中之每個狀態的資料行。 如果資料列與資料行的狀態對應，則資料格代表狀態存在於資料庫中的實際次數。 如果它們不對應，則資料格代表預測的錯誤。|  
  
## <a name="see-also"></a>另請參閱  
 [&#40;資料採礦&#41;的挖掘精確度圖表設計工具](mining-accuracy-chart-designer-data-mining.md)   
 [測試和驗證工作，以及如何 &#40;資料採礦&#41;](data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)   
 [測試及驗證 &#40;資料採礦&#41;](data-mining/testing-and-validation-data-mining.md)  
  
  
