---
title: 使用 Analysis Services 教學課程專案的修改版本 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 685aa217-de1b-4df2-bf22-095228c40775
author: minewiskan
ms.author: owend
ms.openlocfilehash: b6c55141db6491fe1532dfcdc37a6d7a688c7274
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84543360"
---
# <a name="using-a-modified-version-of-the-analysis-services-tutorial-project"></a>使用 Analysis Services 教學課程專案的已修改版本
  本教學課程的其餘課程是依據您在前面三課所完成之 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程專案的增強型版本。 更多的資料表和具名計算已新增至 **Adventure Works DW 2012** 資料來源檢視、更多的維度已新增至專案，而且這些新維度已新增至 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程 Cube。 此外，已加入第二個量值群組，它包含第二個事實資料表的量值。 這個增強型專案可讓您繼續學習如何在商業智慧應用程式中加入功能，而不必重複已學過的技巧。  
  
 在您繼續這個教學課程之前，必須先下載、解壓縮、載入和處理 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程專案的增強型版本。  使用本課程中的指示，以確保您已經執行所有步驟。  
  
## <a name="downloading-and-extracting-the-project-file"></a>下載並解壓縮專案檔案  
  
1.  [按一下這裡](https://go.microsoft.com/fwlink/?LinkID=221866) 前往下載頁面，此頁面會提供此教學課程隨附的範例專案。 本教學課程專案已包含於 **Analysis Services Tutorial SQL Server 2012** 下載中。  
  
2.  按一下 [Analysis Services Tutorial SQL Server 2012]****，下載包含適用於此教學課程之專案的套件。  
  
     根據預設，.zip 檔案會儲存至 [下載] 資料夾。 您必須將 .zip 檔案移至路徑較短的位置 (例如，建立 C:\Tutorials 資料夾來儲存檔案)。  接著，您可以解壓縮包含在 .zip 檔案中的檔案。 如果您嘗試從路徑較長的 [下載] 資料夾解壓縮檔案，將會獲得課程 1。  
  
3.  在根磁碟機上或附近建立一個子資料夾，例如 C:\Tutorial。  
  
4.  將 **Analysis Services Tutorial SQL Server 2012.zip** 移動到子資料夾。  
  
5.  以滑鼠右鍵按一下該檔案，然後選取 [Extract All(全部解壓縮)]****。  
  
6.  瀏覽至 **Lesson 4 Start** 資料夾以尋找 **Analysis Services Tutorial.sln** 檔案。  
  
## <a name="loading-and-processing-the-enhanced-project"></a>載入和處理增強型專案  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 的 [檔案**File** ] 功能表上，按一下 [**關閉方案**] 以關閉您不會使用的檔案。  
  
2.  在 [檔案]**** 功能表上，指向 [開啟舊檔]****，再按一下 [專案/方案]****。  
  
3.  瀏覽到您解壓縮教學課程專案檔案的位置。  
  
     尋找名為 **Lesson 4 Start**的資料夾，然後按兩下 Analysis Services Tutorial.sln。  
  
4.  將 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程專案的增強型版本部署到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的本機執行個體，或另一個執行個體，並確認處理已順利完成。  
  
## <a name="understanding-the-enhancements-to-the-project"></a>了解專案的增強功能  
 這個專案的增強型版本與您在前面 3 課所完成的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程專案的版本不同。 下列章節將描述其差異。 在繼續本教學課程的其餘課程之前，請檢閱這項資訊。  
  
### <a name="data-source-view"></a>[資料來源檢視]  
 增強型專案中的資料來源檢視多包含一個事實資料表及四個維度資料表，它們來自 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 資料庫。  
  
 請注意，資料來源檢視中的十個資料表使得 \<All Tables> 圖表變得很擁擠， 以致於不容易了解資料表之間的關聯性及尋找特定資料表。 為了解決這個問題，資料表分成兩個邏輯圖表：[網際網路銷售]**** 圖表和 [轉售商銷售]**** 圖表。 這些圖表各以單一事實資料表為中心。 建立邏輯圖表可讓您檢視及使用資料來源檢視中的資料表的特定子集，而不是檢視單一圖表中的所有資料表及其關聯性。  
  
#### <a name="internet-sales-diagram"></a>Internet Sales 圖表  
 [網際網路銷售]**** 圖表包含透過網際網路直接向客戶銷售 [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] 產品之相關資料表。 圖表中的資料表為 4 個維度資料表和 1 個事實資料表，這些是您在第 1 課新增至 **Adventure Works DW 2012** 資料來源檢視中的資料表。 這些資料表如下：  
  
-   **地理位置**  
  
-   **客戶**  
  
-   **日期**  
  
-   **產品**  
  
-   **InternetSales**  
  
#### <a name="reseller-sales-diagram"></a>轉售商銷售圖表  
 [轉售商銷售]**** 圖表包含與轉售商銷售 [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] 產品有關的資料表。 此圖表包含下列七個維度資料表及一個事實資料表，它們來自 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 資料庫：  
  
-   **轉售商**  
  
-   **促銷**  
  
-   **SalesTerritory**  
  
-   **地理位置**  
  
-   **日期**  
  
-   **產品**  
  
-   **員工**  
  
-   **ResellerSales**  
  
 請注意，**DimGeography**、**DimDate** 和 **DimProduct** 資料表同時用於 [網際網路銷售額]**** 圖表和 [轉售商銷售]**** 圖表。 維度資料表可連結至多個事實資料表。  
  
### <a name="database-and-cube-dimensions"></a>資料庫和 Cube 維度  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程專案包含 5 個新資料庫維度， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程 Cube 包含這 5 個與 Cube 維度相同的維度。 這些維度已定義為具有階層和屬性，這些已使用具名計算、構成要素成員索引鍵和顯示資料夾來修改過。 下列清單描述的是新的維度。  
  
 Reseller 維度  
 Reseller 維度是依據 **Adventure Works DW 2012** 資料來源檢視中的 **Reseller** 資料表。  
  
 Promotion 維度  
 Promotion 維度是依據 **Adventure Works DW 2012** 資料來源檢視中的 **Promotion** 資料表。  
  
 Sales Territory 維度  
 Sales Territory 維度是依據 **Adventure Works DW 2012** 資料來源檢視中的 **SalesTerritory** 資料表。  
  
 Employee 維度  
 Employee 維度是依據 **Adventure Works DW 2012** 資料來源檢視中的 **Employee** 資料表。  
  
 Geography 維度  
 Geography 維度是依據 **Adventure Works DW 2012** 資料來源檢視中的 **Geography** 資料表。  
  
#### <a name="analysis-services-cube"></a>Analysis Services Cube  
 **Analysis Services Tutorial** Cube 現在包含兩個量值群組：以 **InternetSales** 資料表為基礎的原始量值群組，和以 **Adventure Works DW 2012** 資料來源檢視中的 **ResellerSales** 資料表為基礎的另一個量值群組。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [定義父子式階層中父屬性 (Attribute) 的屬性 (Property)](lesson-4-2-defining-parent-attribute-properties-in-a-parent-child-hierarchy.md) 
  
## <a name="see-also"></a>另請參閱  
 [部署 Analysis Services 專案](lesson-2-5-deploying-an-analysis-services-project.md)  
  
  
