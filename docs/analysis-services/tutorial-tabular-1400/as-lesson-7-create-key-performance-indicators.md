---
title: Analysis Services 教學課程第 7 課：建立關鍵效能指標 |Microsoft Docs
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 348a012b5915c6b02f04481673fc33128001ff73
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685405"
---
# <a name="create-key-performance-indicators"></a>建立關鍵效能指標

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在這一課，您可以建立關鍵效能指標 (Kpi)。 Kpi 用來量測計所定義之值的效能*基底*量值、 針對*目標*由量值或絕對值定義的值。 在報表用戶端應用程式中，KPI 可為商務專業人士提供快速而簡便的方法來了解商務成就的摘要，或是找出趨勢。 若要進一步了解，請參閱[Kpi](../tabular-models/kpis-ssas-tabular.md)
  
完成本課程的估計時間：**15 分鐘**  
  
## <a name="prerequisites"></a>先決條件  

這篇文章是表格式模型化教學課程中，應該依序完成的一部分。 執行工作之前在這一課，您應已完成上一課：[第 6 課：建立量值](../tutorial-tabular-1400/as-lesson-6-create-measures.md)。   
  
## <a name="create-key-performance-indicators"></a>建立關鍵效能指標  
  
#### <a name="to-create-an-internetcurrentquartersalesperformance-kpi"></a>若要建立 InternetCurrentQuarterSalesPerformance KPI  
  
1.  在模型設計師中，按一下**FactInternetSales**資料表。  
  
2.  在量值方格中，按一下空的資料格。  
  
3.  在資料表上方的公式列中，輸入下列公式： 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    此量值做為 kpi 基底量值。  
  
4.  在量值方格中，以滑鼠右鍵按一下**InternetCurrentQuarterSalesPerformance** > **Create KPI**。   
  
5.  在 [關鍵效能指標 (KPI)] 對話方塊中，在**目標**選取**絕對值**，然後輸入**1.1**。  
  
7.  在左側 (下) 滑動軸欄位輸入 **1**，然後在右側 (上) 滑動軸欄位中輸入 **1.07**。  
  
8.  在 [選取圖示樣式] 中，選取菱形 (紅色)、三角形 (黃色)、圓形 (綠色) 圖示類型。
  
    ![as-lesson7-kpi](../tutorial-tabular-1400/media/as-lesson7-kpi.png)
    
    > [!TIP]  
    > 請注意可擴充**描述**可用圖示樣式下方的標籤。 您可以使用各種 KPI 元素的描述，使其更容易在用戶端應用程式。  
  
9. 按一下 [確定] 完成 KPI。  
  
    在量值方格中，請注意圖示旁**InternetCurrentQuarterSalesPerformance**量值。 這個圖示表示這個量值是 KPI 的基底值。  
  
#### <a name="to-create-an-internetcurrentquartermarginperformance-kpi"></a>若要建立 InternetCurrentQuarterMarginPerformance KPI  
  
1.  中的量值方格**FactInternetSales**資料表中，按一下空白儲存格。  
  
2.  在資料表上方的公式列中，輸入下列公式：  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  以滑鼠右鍵按一下**InternetCurrentQuarterMarginPerformance** > **建立 KPI**。  
  
4.  在 [關鍵效能指標 (KPI)] 對話方塊中，在**目標**選取**絕對值**，然後輸入**1.25**。   
  
5.  在左側 （下） 滑動軸欄位中，滑動直到欄位顯示**0.8**，然後滑動右側 （高） 滑桿欄位，直到欄位顯示**1.03**。  
  
6.  在 [選取圖示樣式] 中，選取菱形 (紅色)、三角形 (黃色)、圓形 (綠色) 圖示類型，然後按一下 [確定]。  
  
## <a name="whats-next"></a>下一步

[第 8 課：建立檢視方塊](../tutorial-tabular-1400/as-lesson-8-create-perspectives.md)。
  
  
