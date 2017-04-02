---
title: "散佈圖 (Analysis Services - 資料採礦) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "圖表 [Analysis Services]"
  - "採礦模型 [Analysis Services], 驗證"
  - "散佈圖"
  - "迴歸演算法 [Analysis Services]"
ms.assetid: 166812ec-fd1c-47c8-88db-d5041142be91
caps.latest.revision: 20
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 20
---
# 散佈圖 (Analysis Services - 資料採礦)
  *「散佈圖」* (Scatter Plot) 會針對此模型所預測的值來繪製資料中的實際值。 散佈圖會沿著 X 軸顯示實際值，並沿著 Y 軸顯示預測值。 散佈圖也會顯示一條線來說明完美預測，也就是預測值完全符合實際值的情況。 這條理想 45 度線上之點的距離會指示預測執行的成果好壞。  
  
## 了解散佈圖  
 假設行銷部門中的模型是根據促銷電子郵件中傳送之連結的點選次數來預測每天的銷售。 由於點選次數和銷售數量都是連續的數值，所以您可以將點選次數繪製為獨立變數，並將銷售繪製為相依變數。 當您這樣做時，直線會顯示預期的線性關係，而該線周圍散佈的點則會顯示預期值與實際值的差異。 這項分析可大致告訴您，某一組結果如何與特定輸入產生相互關聯性，以及與理想模型之間的變異有多大。  
  
## 解譯結果  
 下圖顯示針對剛剛描述的案例所建立的散佈圖範例。  
  
 ![線性迴歸散佈圖的範例](../../analysis-services/data-mining/media/scatterplot-callctr.gif "線性迴歸散佈圖的範例")  
  
 您可以將滑鼠暫停在散佈於此線周圍的任何點上，以檢視工具提示內的預測值和實際值。 散佈圖沒有 **[採礦圖例]** ；但是，該圖本身會包含一個圖例來顯示與此模型有關的分數。 如需解譯分數的詳細資訊，請參閱[線性迴歸模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)。  
  
 您可以將圖表的視覺表示法複製到剪貼簿，但不是基礎資料或公式。 如果您想要檢視這條線的迴歸公式，您可以針對此模型建立內容查詢。 如需詳細資訊，請參閱[線性迴歸模型查詢範例](../../analysis-services/data-mining/linear-regression-model-query-examples.md)。  
  
## 散佈圖的限制  
 只有當您在 **[輸入選擇]** 索引標籤上選擇的模型包含連續可預測屬性時，才會建立散佈圖。 您不必進行任何其他選擇；散佈圖圖表類型會自動顯示在以模型和屬性類型為根據的 **[增益圖]** 索引標籤上。  
  
 雖然時間序列模型會預測連續數字，但是您無法使用散佈圖來測量時間序列模型的精確度。 您可以使用其他方法，例如保留歷程記錄資料的一部分。 如需詳細資訊，請參閱[時間序列模型查詢範例](../../analysis-services/data-mining/time-series-model-query-examples.md)。  
  
## 相關內容  
 下列主題包含有關如何建立及使用散佈圖與相關精確度圖表的詳細資訊。  
  
|主題|連結|  
|------------|-----------|  
|提供如何為此目標郵寄模型建立增益圖的逐步解說。|[資料採礦基本教學課程](../Topic/Basic%20Data%20Mining%20Tutorial.md)<br /><br /> [使用增益圖測試精確度 &#40;基本資料採礦教學課程&#41;](../Topic/Testing%20Accuracy%20with%20Lift%20Charts%20\(Basic%20Data%20Mining%20Tutorial\).md)|  
|說明相關的圖表類型。|[增益圖 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/lift-chart-analysis-services-data-mining.md)<br /><br /> [收益圖 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/profit-chart-analysis-services-data-mining.md)<br /><br /> [分類矩陣 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/classification-matrix-analysis-services-data-mining.md)|  
|描述採礦模型和採礦結構的交叉驗證用法。|[交叉驗證 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)|  
|描述建立增益圖及其他精確度圖表的步驟。|[測試及驗證工作與操作方法 &#40;資料採礦&#41;](../../analysis-services/data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)|  
  
## 請參閱＜  
 [測試和驗證 &#40;資料採礦&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
  