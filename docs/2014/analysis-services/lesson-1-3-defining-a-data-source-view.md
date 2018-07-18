---
title: 定義資料來源檢視 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: af00938a-5a06-4fae-b2fc-f3fb0ca3cea5
caps.latest.revision: 28
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 556c860f3714de07e2b0f0242b9c73b731af2f4b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37286145"
---
# <a name="defining-a-data-source-view"></a>定義資料來源檢視
  定義您在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 專案中使用的資料來源之後，下一個步驟通常是定義專案的資料來源檢視。 資料來源檢視是資料來源在專案中定義之指定資料表和檢視的中繼資料的單一統一檢視。 在資料來源檢視中儲存中繼資料可讓您在開發期間使用中繼資料，而不需要開啟與任何基礎資料來源的連接。 如需詳細資訊，請參閱 [多維度模型中的資料來源檢視](multidimensional-models/data-source-views-in-multidimensional-models.md)。  
  
 在下列工作中，您可以定義一個包含 **AdventureWorksDW2012** 資料來源的 5 個資料表的資料來源檢視。  
  
### <a name="to-define-a-new-data-source-view"></a>若要定義新的資料來源檢視  
  
1.  在方案總管中 (於 [Microsoft Visual Studio] 視窗右側)，以滑鼠右鍵按一下 [資料來源檢視]，然後按一下 [新增資料來源檢視]。  
  
2.  在 [歡迎使用資料來源檢視精靈] 頁面上，按一下 [下一步]。 此時會出現 [選取資料來源] 頁面。  
  
3.  在 [關聯式資料來源] 底下，已選取 [Adventure Works DW 2012] 資料來源。 按 [下一步] 。  
  
    > [!NOTE]  
    >  若要建立依據多個資料來源的資料來源檢視，首先要定義一個依據單一資料來源的資料來源檢視。 這個資料來源稱為主要資料來源。 然後您可以從次要資料來源加入資料表和檢視。 當您根據多個資料來源中的相關資料表設計包含屬性的維度時，可能需要將 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料來源定義為主要資料來源，才能使用其分散式查詢引擎功能。  
  
4.  在 [選取資料表和檢視表] 頁面上，從所選取資料來源提供的物件清單中選取資料表和檢視表。 您可以篩選這份清單來幫助您選取資料表和檢視。  
  
    > [!NOTE]  
    >  按一下右上角的最大化按鈕，如此視窗就會涵蓋全螢幕。 這樣做可讓您更輕易地查看完整的可用物件清單。  
  
     在 [可用的物件] 清單中，選取下列物件。 您可以在按住 CTRL 鍵的同時，按一下每個資料表，藉以選取多個資料表：  
  
    -   **DimCustomer (dbo)**  
  
    -   **DimDate (dbo)**  
  
    -   **DimGeography (dbo)**  
  
    -   **DimProduct (dbo)**  
  
    -   **FactInternetSales (dbo)**  
  
5.  按一下 [>] 將所選取的資料表加入 [包含的物件] 清單中。  
  
6.  按 **[下一步]**。  
  
7.  在 [名稱] 欄位中，確認有顯示 [Adventure Works DW 2012]，然後按一下 [完成]。  
  
     [Adventure Works DW 2012] 資料來源檢視會出現在方案總管的 [資料來源檢視] 資料夾內。 資料來源檢視的內容也會顯示在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 的 [資料來源檢視設計工具] 中。 這個設計師包含下列元素：  
  
    -   [圖表] 窗格，以圖形表示資料表及其關聯性。  
  
    -   [資料表] 窗格，以樹狀檢視顯示資料表及其結構描述元素。  
  
    -   [圖表組合管理] 窗格，可讓您建立子圖表來檢視資料來源檢視的子集。  
  
    -   [資料來源檢視設計工具] 特有的工具列。  
  
8.  若要最大化 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 開發環境，請按一下 [最大化] 按鈕。  
  
9. 若要以 50% 的大小檢視 [圖表] 窗格中的資料表，請按一下 [資料來源檢視設計工具] 工具列上的**顯示比例**圖示。 這樣會隱藏每一個資料表的資料行詳細資料。  
  
10. 若要隱藏方案總管，請按一下 [自動隱藏] 按鈕，它是標題列上的圖釘圖示。 若要再次檢視 [方案總管]，請沿著開發環境的右側將指標定位在 [方案總管] 索引標籤上。 若要取消隱藏方案總管，請再按一次 [自動隱藏] 按鈕。  
  
11. 如果視窗預設並未隱藏，請按一下 [屬性] 視窗和方案總管視窗標題列上的 [自動隱藏]。  
  
     現在您可以在 [圖表] 窗格中檢視所有資料表及其關聯性。 請注意，FactInternetSales 資料表和 DimDate 資料表之間有 3 種關聯性。 每一個銷售都有 3 個相關的銷售日期：訂購日期、截止日期和出貨日期。 若要檢視任何關聯性的詳細資料，請按兩下 [圖表] 窗格內的關聯性箭頭。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [修改預設資料表名稱](lesson-1-4-modifying-default-table-names.md)  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型中的資料來源檢視](multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
