---
title: 第8課：建立關鍵效能指標 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a6c8ac2b-64ba-456f-b418-7bf0afe145d1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1d9d3145583670fb849321bac5b57928caacfbc2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66078364"
---
# <a name="lesson-8-create-key-performance-indicators"></a>第 8 課：建立關鍵效能指標
  在這一課，您將建立關鍵效能指標 (KPI)。 Kpi 是用來針對*目標*值（也是由量值或絕對值所定義），測量由*基底*量值定義之值的效能。 在報告用戶端應用程式中，KPI 可讓商務專業人士輕鬆、快速地概括了解商務成果或找出趨勢。 如需詳細資訊，請參閱 [KPI &#40;SSAS 表格式&#41;](tabular-models/kpis-ssas-tabular.md)。  
  
 完成本課程的估計時間： **15 分鐘**  
  
## <a name="prerequisites"></a>先決條件  
 本主題是表格式模型教學課程的一部分，請依序完成。 在執行本課中的工作之前，您應已完成上一課： [第 7 課：建立量值](lesson-6-create-measures.md)。  
  
## <a name="create-key-performance-indicators"></a>建立關鍵效能指標  
  
#### <a name="to-create-an-internet-current-quarter-sales-performance-kpi"></a>若要建立網際網路當季銷售績效 (Internet Current Quarter Sales Performance) KPI  
  
1.  在模型設計師中，按一下 [網際網路銷售]**** 資料表 (索引標籤)。  
  
2.  在量值方格中，按一下空的儲存格。  
  
3.  在資料表上方的公式列中，輸入下列公式︰  
  
     `Internet Current Quarter Sales Performance :=IFERROR([Internet Current Quarter Sales]/[Internet Previous Quarter Sales Proportion to QTD],BLANK())`  
  
     完成建立公式時，按 ENTER。  
  
     此量值將做為 KPI 的基底量值。  
  
4.  在量值方格中，以滑鼠右鍵按一下 [網際網路當季銷售績效]**** 量值，然後按一下 [建立 KPI]****。  
  
     [關鍵效能指標]**** 對話方塊隨即開啟。  
  
5.  在 [關鍵效能指標]**** 對話方塊的 [定義目標值]**** 中，選取 [絕對值]**** 選項。  
  
6.  在 [**絕對值**] 欄位中， `1.1`輸入，然後按 enter。  
  
7.  在 [**定義狀態臨界**值] 的左側（低）滑杆欄位中`1`，輸入，然後在右側（高）滑杆欄位中， `1.07`輸入。  
  
8.  在 [選取圖示樣式]**** 中，選取菱形 (紅色)、三角形 (黃色)、圓形 (綠色) 圖示類型。  
  
    > [!TIP]  
    >  請注意可用圖示樣式下方的 [描述]**** 可擴充欄位。 您可以為各個不同的 KPI 元素輸入描述，使其在用戶端應用程式中更容易識別。  
  
9. 按一下 [確定] **** 來完成 KPI。  
  
     請注意量值方格中 [網際網路當季銷售績效]**** 量值旁的圖示。 這個圖示表示此量值做為 KPI 的基準值。  
  
#### <a name="to-create-an-internet-current-quarter-margin-performance-kpi"></a>若要建立網際網路當季毛利率績效 (Internet Current Quarter Margin Performance) KPI  
  
1.  在 [網際網路銷售]**** 資料表的量值方格中，按一下空的資料格。  
  
2.  在資料表上方的公式列中，輸入下列公式︰  
  
     `Internet Current Quarter Margin Performance :=IF([Internet Previous Quarter Margin Proportion to QTD]<>0,([Internet Current Quarter Margin]-[Internet Previous Quarter Margin Proportion to QTD])/[Internet Previous Quarter Margin Proportion to QTD],BLANK())`  
  
     完成建立公式時，按 ENTER。  
  
3.  在量值方格中，以滑鼠右鍵按一下 [網際網路當季毛利率績效]**** 量值，然後按一下 [建立 KPI]****。  
  
4.  在 [關鍵效能指標]**** 對話方塊的 [定義目標值]**** 中，選取 [絕對值]**** 選項。  
  
5.  在 [**絕對值**] 欄位中， `1.25`輸入。  
  
6.  在 [定義狀態臨界值]**** 中，滑動左側 (下) 滑動軸欄位，直到欄位顯示 **0.8**，然後滑動右側 (上) 滑動軸欄位，直到欄位顯示 **1.03**。  
  
7.  在 [選取圖示樣式]**** 中，選取菱形 (紅色)、三角形 (黃色)、圓形 (綠色) 圖示類型，然後按一下 [確定]****。  
  
## <a name="next-step"></a>後續步驟  
 若要繼續進行本教學課程，請前往下一課： [第 9 課：建立檢視方塊](lesson-8-create-perspectives.md)。  
  
  
