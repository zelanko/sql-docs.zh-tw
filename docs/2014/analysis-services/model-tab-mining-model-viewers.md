---
title: 模型索引標籤（採礦模型檢視器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.timeseries.decisiontree.f1
ms.assetid: 50570bb4-fcac-411e-b530-0398437efda7
author: minewiskan
ms.author: owend
ms.openlocfilehash: 42285f94057441d01259c5fd54ce896dd0316b94
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84537360"
---
# <a name="model-tab-mining-model-viewers"></a>模型索引標籤 (採礦模型檢視器)
  Microsoft 時間序列檢視器中的 [模型]**** 索引標籤會將時間序列的表示顯示為圖形中的節點，這與決策樹模型中採用的方式類似。  
  
 使用此時間序列模型檢視可擷取有關時間序列分析的有用資訊，包括圖形的方程式、ARIMA 詞彙和係數。  
  
 **如需詳細資訊，請參閱** [Microsoft 時間序列演算法](data-mining/microsoft-time-series-algorithm.md)、 [使用 Microsoft 時間序列檢視器瀏覽模型](data-mining/browse-a-model-using-the-microsoft-time-series-viewer.md)、 [Microsoft 時間序列演算法](data-mining/microsoft-time-series-algorithm.md)  
  
## <a name="options"></a>選項  
 **重新整理檢視器內容**  
 在檢視器中重新載入採礦模型。  
  
 **採礦模型**  
 選擇要檢視的採礦模型。 採礦模型會在其關聯的檢視器中開啟。  
  
 **檢視者**  
 選擇用來瀏覽選取之採礦模型的檢視器。 您可以使用此模型類型的自訂檢視器，或 [Microsoft 一般內容樹狀檢視器]****。 還可以使用外掛程式檢視器 (如果有)。  
  
 **放大**  
 放大圖表。  
  
 **縮小**  
 縮小圖表。  
  
 **複製圖表檢視**  
 將圖表的可見部分複製到剪貼簿。  
  
 **複製整個圖表**  
 將整個圖表複製到剪貼簿。  
  
 **將圖表縮放至視窗大小**  
 縮小圖表，直到畫面能容納整個圖表為止。  
  
 **路徑**  
 從下拉式清單中選取要在檢視器中顯示的樹狀目錄。  
  
 如果時間序列模型包含多個數列，每個數列都會表示成個別的樹狀目錄。 例如，如果您在一段時間內為 [Quantity] 和 [Sales Amount] 建立預測，則將為每個可預測屬性建立單獨的數列。  
  
 清單中色彩反白顯示的長度表示樹狀目錄中的層級數目。 也就是說，可由單一節點表示的時間序列模型會包含一個用於描述趨勢的方程式，並且彩色列會很短 (當然，如果該模型是混合模型，則節點會同時包含 ARIMA 和 ARTXP 方程式)。  
  
 如果下拉式清單中顯示的樹狀目錄有較長的彩色列，這表示該模型在樹狀目錄中有多個分支。 分支表示迴歸更為複雜，而且模型必須分為多個區段，每個節點中都有一個 (或一對) 不同的方程式。  
  
 **背景**  
 使用此控制項可選取每個節點中背景色彩所表示的狀態。  
  
 **預設展開**  
 調整模型中所有樹狀顯示的預設層級數目。  
  
 **顯示層級**  
 變更樹狀目錄中顯示的層級數目。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦演算法 &#40;Analysis Services-資料採礦&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [&#40;資料採礦模型設計工具的採礦模型檢視器&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [資料採礦模型檢視器](data-mining/data-mining-model-viewers.md)  
  
  
