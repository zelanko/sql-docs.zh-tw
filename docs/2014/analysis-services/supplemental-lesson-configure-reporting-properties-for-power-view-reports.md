---
title: 設定 Power View 報表的報表屬性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0ffc5f44-17d3-42d4-bc2c-baf3b4485e2d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 812c205c1e612604c0c39a5effb3b9da50308d7a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66067963"
---
# <a name="configure-reporting-properties-for-power-view-reports"></a>設定 Power View 報表的報表屬性
  在此補充課程中，我們將會針對 Adventure Works Internet Sales Model 專案設定報表屬性。 報表屬性讓使用者能夠更輕鬆地在 Power View 中選取及顯示模型資料。 您也會設定屬性來隱藏某些資料行和資料表，並建立新的資料供圖表使用。  
  
 在完成本課並將模型重新部署至與 SharePoint 和 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 整合的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 執行個體之後，您可以建立資料來源、指定資料連接資訊、啟動 Power View 並針對模型設計報表。  
  
 本課將不會描述如何建立及使用 Power View 報表。 本課的目的是要針對表格式模型作者提供將影響模型資料顯示於 Power View 中之方式的屬性和設定簡介。 若要深入了解建立 Power View 報表，請參閱[教學課程：在 Power View 中建立範例報表](https://go.microsoft.com/fwlink/?LinkId=221204)。  
  
 估計的時間才能完成這一課：**30 分鐘**  
  
## <a name="prerequisites"></a>先決條件  
 這個補充課程是表格式模型教學課程的一部分，必須依序完成。 在執行本補充課程中的工作之前，您應已完成之前所有課程。  
  
 為了完成這個特殊補充課程，您也必須具備以下條件：  
  
-   Adventure Works Internet Sales Model (透過本教學課程完成) 已準備要部署或是已經部署至於表格式模式下執行的 Analysis Services 執行個體。  
  
-   將 SharePoint 網站與表格式模式下執行的 [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] 和 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 整合，並設定為可支援 Power View 報表。  
  
-   您必須具備充分的權限，才能在 SharePoint 網站上建立指向 Adventure Works Internet Sales Model 的資料連接。  
  
## <a name="model-properties-that-affect-reporting"></a>影響報表的模型屬性  
 在撰寫表格式模型時，您可以在個別資料行和資料表上設定某些屬性，以增強 Power View 中的使用者報表體驗。 此外，您也可以建立其他模型資料來支援資料視覺效果以及報表用戶端的其他特有功能。 在範例 Adventure Works Internet Sales Model 中，以下是您將進行的部分變更：  
  
-   **加入新資料**-加入導出資料行中的新資料，透過使用 DAX 公式在圖表中顯示的工作變得更容易的格式建立日期資訊。  
  
-   **隱藏對使用者無用的資料表和資料行** - [隱藏]  屬性會控制資料表和資料表資料行是否會顯示在報表用戶端。 隱藏的項目依然是模型的一部分，而且可供查詢和計算。  
  
-   **啟用單鍵資料表**-根據預設，會發生任何動作如果使用者按一下欄位清單中的資料表。 若要變更這個行為，使得按一下資料表時會將資料表加入至報表中，請在每一個要併入資料表的資料行上設定 [預設欄位集]。 這個屬性會在使用者最可能想要使用的資料表資料行上設定。  
  
-   **視需要設定群組** - [保留唯一資料列]  屬性會決定資料行中的值是否應該依據另一個欄位 (如識別碼欄位) 中的值來分組。 如果是包含類似客戶名稱之重複值的資料行 (例如，有多位客戶命名為 John Smith)，一定要在 [資料列識別碼]  欄位上分組 (保留唯一資料列)，才能為使用者提供正確的結果。  
  
-   **設定資料類型和資料格式** - 根據預設，Power View 會根據資料行資料類型套用規則，以判斷此欄位是否可以當做量值使用。 因為 Power View 中的每一個資料視覺效果皆具有量值與非量值放置位置的相關規則，所以請務必在模型中設定資料類型或是覆寫預設值，以便達成您希望使用者具備的行為。  
  
-   **設定依資料行排序**屬性-**依資料行排序**屬性會指定不同的欄位中的值是否應該依據排序資料行的值。 例如，在包含月份名稱的 [Month Calendar] 資料行上，依據 [Month Number] 資料行排序。  
  
## <a name="hide-tables-from-client-tools"></a>在用戶端工具中隱藏資料表  
 因為 [Product] 資料表中已經有 [Product Category] 導出資料行和 [Product Subcategory] 導出資料行，所以不必讓用戶端應用程式看到 [Product Category] 和 [Product Subcategory] 資料表。  
  
#### <a name="to-hide-the-product-category-and-product-subcategory-tables"></a>若要隱藏 [Product Category] 和 [Product Subcategory] 資料表  
  
1.  在模型設計師中，以滑鼠右鍵按一下 [Product Category]  資料表 (索引標籤)，然後按一下 [在用戶端工具中隱藏]  。  
  
2.  以滑鼠右鍵按一下 [Product Subcategory]  資料表 (索引標籤)，然後按一下 [在用戶端工具中隱藏]  。  
  
## <a name="create-new-data-for-charts"></a>為圖表建立新的資料  
 有時您可能需要在模型中使用 DAX 公式建立新的資料。 在此工作中，您會將兩個新的導出資料行加入至 [Date] 資料表。 這些新的資料行將會以便於在圖表中使用的格式提供日期欄位。  
  
#### <a name="to-create-new-data-for-charts"></a>若要為圖表建立新的資料  
  
1.  在 [Date]  資料表中，捲動到最右邊，然後按一下 [加入資料行]  。  
  
2.  在公式列使用以下公式加入兩個新的導出資料行：  
  
    |資料行名稱|公式|  
    |-----------------|-------------|  
    |Year Quarter|=[Calendar Year] & " Q" & [Calendar Quarter]|  
    |Year Month|=[Calendar Year] & FORMAT([Month],"#00")|  
  
## <a name="default-field-set"></a>預設欄位集  
 [預設欄位集] 是為資料表預先定義的資料行和量值清單，當您按一下報表欄位清單中的資料表時，此清單會自動加入 Power View 報表畫布。 基本上來說，當此資料表在 Power View 報表中視覺化時，您可以指定使用者想要看到的預設資料行、量值和欄位順序。  在 Internet Sales 模型中，您將會針對 Customer、Geography 和 Product 資料表定義預設欄位集和順序。 只包含使用者在使用 Power View 報表分析 Adventure Works Internet Sales 資料時，想要看到的最常見資料行。  
  
 如需 [預設欄位集] 的詳細資訊，請參閱《SQL Server 線上叢書》中的[設定 Power View 報表的預設欄位集 &#40;SSAS 表格式&#41;](tabular-models/power-view-configure-default-field-set-for-reports.md)。  
  
#### <a name="to-set-default-field-set-for-tables"></a>若要為資料表設定預設欄位集  
  
1.  在模型設計師中，按一下 [Customer]  資料表 (索引標籤)。  
  
2.  在 [屬性]  視窗的 [報表屬性]  底下，按一下 [預設欄位集]  屬性中的 [按一下可編輯]  ，即可開啟 [預設欄位集]  對話方塊。  
  
3.  在 [預設欄位集]  對話方塊的 [資料表中的欄位]  清單方塊內按 Ctrl 鍵，並選取以下欄位，然後按一下 [新增]  ：  
  
     [Birth Date]  、[Customer Alternate Id]  、[First Name]  、[Last Name]  。  
  
4.  在 [預設欄位，依照順序]  視窗中，使用上移和下移按鈕進行以下排序：  
  
     **Customer Alternate Id**  
  
     **First Name**  
  
     **Last Name**  
  
     **Birth Date**  
  
5.  按一下 [確定]  ，關閉 [Customer]  資料表的 [預設欄位集]  對話方塊。  
  
6.  針對 [Geography]  資料表執行以上相同步驟，選取以下欄位並依照以下順序排列：  
  
     **城市**， **State Province Code**，**狀態區域碼**。  
  
7.  最後，針對 [Product]  資料表執行以上相同步驟，選取以下欄位並依照以下順序排列。  
  
     [Product Alternate Id]  、[Product Name]  。  
  
## <a name="table-behavior"></a>資料表行為  
 您可以使用 [資料表行為] 屬性來變更不同視覺效果類型的預設行為，以及變更 Power View 報表中使用之資料表的群組行為。 如此可讓識別資訊 (如名稱、影像或標題) 在圖格、卡片和圖表版面配置中有更好的預設位置。  
  
 如需資料表行為屬性的詳細資訊，請參閱《SQL Server 線上叢書》中的[設定 Power View 報表的資料表行為屬性 &#40;SSAS 表格式&#41;](tabular-models/power-view-configure-table-behavior-properties-for-reports.md)。  
  
#### <a name="to-set-table-behavior-for-tables"></a>若要為資料表設定資料表行為  
  
1.  在模型設計師中，按一下 [Customer]  資料表 (索引標籤)。  
  
2.  在 [屬性]  視窗中，按一下 [資料表行為]  屬性的 [按一下可編輯]  ，即可開啟 [資料表行為]  對話方塊。  
  
3.  在 [資料表行為]  對話方塊的 [資料列識別碼]  下拉式清單方塊中，選取 [Customer Id]  資料行。  
  
4.  在 [保留唯一資料列]  清單方塊中，選取 [First Name]  和 [Last Name]  。  
  
     這個屬性設定會指定哪些資料行提供應視為唯一的值，即使是重複值也一樣 (例如，當兩位或多位員工同名時)。  
  
5.  在 [預設標籤]  下拉式清單方塊中，選取 [Last Name]  資料行。  
  
     這個屬性設定會指定哪個資料行提供代表資料列資料的顯示名稱。  
  
6.  請針對 [Geography]  資料表重複以上步驟，選取 [Geography Id]  資料行當做資料列識別碼，並在 [保留唯一資料列]  清單方塊中選取 [City]  資料行。 您不需要為這個資料表設定預設標籤。  
  
7.  請針對 [Product]  資料表重複以上步驟，選取 [Product Id]  資料行當做資料列識別碼，並在 [保留唯一資料列]  清單方塊中選取 [Product Name]  資料行。 為 [預設標籤]  選取 [Product Alternate Id]  。  
  
## <a name="reporting-properties-for-columns"></a>資料行的報表屬性  
 在資料行上可設定許多基本資料行屬性和特定報表屬性來改善模型報表體驗。 例如，使用者可能不需要看到每一個資料表中的每一個資料行。 就像您隱藏 Product Category 和 Product Subcategory 資料表更早版本，使用資料行的 Hidden 屬性，您可以隱藏特定的資料行，否則會顯示資料表中。 其他屬性 (例如 [資料格式] 和 [依資料行排序]) 也會影響資料行資料出現在報表中的方式。 您現在即將在特定資料行上設定部分屬性。 有一些資料行不需要任何動作，所以不會顯示在底下。  
  
 您只會在這裡設定幾個不同的資料行屬性，但是還有許多其他屬性。 如需資料行報表屬性的詳細資訊，請參閱《SQL Server 線上叢書》中的[資料行屬性 &#40;SSAS 表格式&#41;](tabular-models/properties-ssas-tabular.md)。  
  
#### <a name="to-set-properties-for-columns"></a>若要設定資料行的屬性  
  
1.  在模型設計師中，按一下 [Customer]  資料表 (索引標籤)。  
  
2.  按一下 [Customer Id]  資料行，在 [屬性]  視窗中顯示資料行屬性。  
  
3.  在 [屬性]  視窗中，將 [Hidden]  屬性設定為 True。 然後 [Customer Id]  資料行就會在模型設計師中呈現灰色。  
  
4.  針對每一個指定的資料表重複以上步驟，設定以下資料行和報表屬性。 保留所有其他屬性的預設設定。  
  
     **客戶**  
  
    |「資料行」|屬性|值|  
    |------------|--------------|-----------|  
    |Geography Id|Hidden|True|  
    |Birth Date|資料格式|簡短日期|  
  
     **日期**  
  
    > [!NOTE]  
    >  因為 [Date] 資料表選取為模型日期資料表，藉由使用 [標記為日期資料表] 設定，在第 7 課：標記為日期資料表，並在 Date 資料表中的資料行的日期資料行來當做唯一識別碼，也就是日期資料行的資料列識別碼屬性將會自動設定為 True，並無法變更。 當您在 DAX 公式中使用時間智慧函數時，您必須指定日期資料表。 在此模型中，您已使用時間智慧函數建立許多量值，以計算各個不同期間的銷售資料 (例如上一季和當季) 並用於 KPI 中。 如需指定日期資料表的詳細資訊，請參閱《SQL Server 線上叢書》中的[指定標記為日期資料表以搭配時間智慧使用 &#40;SSAS 表格式&#41;](tabular-models/specify-mark-as-date-table-for-use-with-time-intelligence-ssas-tabular.md)。  
  
    |「資料行」|屬性|值|  
    |------------|--------------|-----------|  
    |Date|資料格式|簡短日期|  
    |Day Number of Week|Hidden|True|  
    |Day Name|依資料行排序|Day Number of Week|  
    |Day of Week|Hidden|True|  
    |Day of Month|Hidden|True|  
    |Day of Year|Hidden|True|  
    |Month Name|依資料行排序|Month|  
    |Month|Hidden|True|  
    |Month Calendar|Hidden|True|  
    |Fiscal Quarter|Hidden|True|  
    |Fiscal Year|Hidden|True|  
    |Fiscal Semester|Hidden|True|  
  
     **地理位置**  
  
    |「資料行」|屬性|值|  
    |------------|--------------|-----------|  
    |Geography Id|Hidden|True|  
    |Sales Territory Id|Hidden|True|  
  
     **產品**  
  
    |「資料行」|屬性|值|  
    |------------|--------------|-----------|  
    |Product Id|Hidden|True|  
    |Product Alternate Id|預設標籤|True|  
    |Product Subcategory Id|Hidden|True|  
    |Product Start Date|資料格式|簡短日期|  
    |Product End Date|資料格式|簡短日期|  
    |Large Photo|Hidden|True|  
  
     **網際網路銷售**  
  
    |「資料行」|屬性|值|  
    |------------|--------------|-----------|  
    |Product Id|Hidden|True|  
    |Customer Id|Hidden|True|  
    |Promotion Id|Hidden|True|  
    |Currency Id|Hidden|True|  
    |Sales Territory Id|Hidden|True|  
    |Order Quantity|資料類型<br /><br /> 資料格式<br /><br /> 小數位數|十進位數字<br /><br /> 十進位數字<br /><br /> 0|  
    |Order Date|資料類型|簡短日期|  
    |Due Date|資料類型|簡短日期|  
    |Ship Date|資料類型|簡短日期|  
  
## <a name="redeploy-the-adventure-works-internet-sales-tabular-model"></a>重新部署 Adventure Works Internet Sales 表格式模型  
 因為您已變更此模型，所以必須重新部署。 基本上，您將會重複執行的工作[第 14 課：部署](lesson-13-deploy.md)。  
  
#### <a name="to-redeploy-the-adventure-works-internet-sales-tabular-model"></a>若要重新部署 Adventure Works Internet Sales 表格式模型  
  
-   在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中，按一下 [建立]  功能表，然後按一下 [Deploy Adventure Works Internet Sales Model (部署 Adventure Works Internet Sales Model)]  。  
  
     [部署]  對話方塊隨即出現，並且顯示中繼資料以及模型中每個資料表的部署狀態。  
  
## <a name="next-steps"></a>後續步驟  
 您現在可以使用 Power View 將模型中的資料視覺化。 請確定 SharePoint 網站上的 Analysis Services 和 Reporting Services 帳戶具有模型部署所在之 Analysis Services 執行個體的讀取權限。  
  
 若要建立 Reporting Services 報表資料來源以指向您的模型，請參閱[資料表模型連接類型 (SSRS)](https://msdn.microsoft.com/library/hh270317%28v=SQL.110%29.aspx)。  
  
  
