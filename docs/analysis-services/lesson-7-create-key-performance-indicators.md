---
title: 第 8 課： 建立關鍵效能指標 |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6e56d4a533caaf95077eb06fabb5fd0bc0c42b07
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="lesson-7-create-key-performance-indicators"></a>第 7 課： 建立關鍵效能指標
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在這一課，您將建立關鍵效能指標 (KPI)。 KPI 會對照量值或絕對值所定義的「目標」值，量測由「基底」量值所定義之值的效能。 在報表用戶端應用程式中，KPI 可為商務專業人士提供快速而簡便的方法來了解商務成就的摘要，或是找出趨勢。 若要進一步了解，請參閱[Kpi](../analysis-services/tabular-models/kpis-ssas-tabular.md)。  
  
完成本課程的估計時間： **15 分鐘**  
  
## <a name="prerequisites"></a>必要條件  
本主題是表格式模型教學課程的一部分，必須依序完成。 然後再執行工作，在這一課，您應已完成上一課：[第 6 課： 建立量值](../analysis-services/lesson-6-create-measures.md)。   
  
## <a name="create-key-performance-indicators"></a>建立關鍵效能指標  
  
#### <a name="to-create-an-internetcurrentquartersalesperformance-kpi"></a>若要建立 InternetCurrentQuarterSalesPerformance KPI  
  
1.  在模型設計師中，按一下**FactInternetSales**資料表 （標籤）。  
  
2.  在量值方格中，按一下空的資料格。  
  
3.  在資料表上方的公式列中，輸入下列公式： 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=IFERROR([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    此量值將做為 KPI 的基底量值。  
  
4.  以滑鼠右鍵按一下**InternetCurrentQuarterSalesPerformance** > **建立 KPI**。   
  
5.  在 [關鍵效能指標 (KPI)] 對話方塊中**目標**選取**絕對值**，然後輸入**1.1**。  
  
7.  在左側 (下) 滑動軸欄位輸入 **1**，然後在右側 (上) 滑動軸欄位中輸入 **1.07**。  
  
8.  在 [選取圖示樣式] 中，選取菱形 (紅色)、三角形 (黃色)、圓形 (綠色) 圖示類型。
  
    ![做為表格式-lesson7-kpi](../analysis-services/media/as-tabular-lesson7-kpi.png)
    
    > [!TIP]  
    > 請注意展開**描述**可用圖示樣式下方的標籤。 使用此輸入不同的 KPI 元素，使其更容易識別在用戶端應用程式中的描述。  
  
9. 按一下 [確定] 完成 KPI。  
  
    在量值方格中，請注意圖示旁**InternetCurrentQuarterSalesPerformance**量值。 這個圖示表示這個量值是 KPI 的基底值。  
  
#### <a name="to-create-an-internetcurrentquartermarginperformance-kpi"></a>若要建立 InternetCurrentQuarterMarginPerformance KPI  
  
1.  中的量值方格**FactInternetSales**資料表中，按一下空白儲存格。  
  
2.  在資料表上方的公式列中，輸入下列公式：  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  以滑鼠右鍵按一下**InternetCurrentQuarterMarginPerformance** > **建立 KPI**。  
  
4.  在 [關鍵效能指標 (KPI)] 對話方塊中**目標**選取**絕對值**，然後輸入**1.25**。   
  
5.  在 [定義狀態臨界值] 中，滑動左側 (下) 滑動軸欄位，直到欄位顯示 **0.8**，然後滑動右側 (上) 滑動軸欄位，直到欄位顯示 **1.03**。  
  
6.  在 [選取圖示樣式] 中，選取菱形 (紅色)、三角形 (黃色)、圓形 (綠色) 圖示類型，然後按一下 [確定]。  
  
## <a name="whats-next"></a>下一步
移至下一課：[第 8 課： 建立檢視方塊](../analysis-services/lesson-8-create-perspectives.md)。
  
  
