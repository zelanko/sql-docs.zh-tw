---
title: 使用已修改的版本的 Analysis Services 教學課程專案 |Microsoft Docs
ms.date: 05/06/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 89674116f8f41dbfca3041f3378e384b581be61f
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2019
ms.locfileid: "65403920"
---
# <a name="lesson-4-1---using-a-modified-version-of-the-analysis-services-tutorial-project"></a>課程 4-1-使用 Analysis Services 教學課程專案的修改的版本
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

本教學課程的其餘課程是依據您在前面三課所完成之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 教學課程專案的增強型版本。 更多的資料表和具名計算已新增至 **Adventure Works DW 2012** 資料來源檢視、更多的維度已新增至專案，而且這些新維度已新增至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 教學課程 Cube。 此外，已加入第二個量值群組，它包含第二個事實資料表的量值。 這個增強型專案可讓您繼續學習如何在商業智慧應用程式中加入功能，而不必重複已學過的技巧。  
  
在您繼續這個教學課程之前，必須先下載、解壓縮、載入和處理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 教學課程專案的增強型版本。  使用本課程中的指示，以確保您已經執行所有步驟。  
  
## <a name="downloading-and-extracting-the-project-file"></a>下載並解壓縮專案檔案  
  
1.  [按一下這裡](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks-analysis-services) 前往下載頁面，此頁面會提供此教學課程隨附的範例專案。 教學課程專案已包含於**adventure-運作方式-多維度-教學課程-projects.zip**下載。  
  
2.  按一下  **adventure-運作方式-多維度-教學課程-projects.zip** ，下載包含本教學課程專案的封裝。  
  
    根據預設，.zip 檔案會儲存至 [下載] 資料夾。 您必須將 .zip 檔案移至路徑較短的位置 (例如，建立 C:\Tutorials 資料夾來儲存檔案)。  接著，您可以解壓縮包含在 .zip 檔案中的檔案。 如果您嘗試從路徑較長的 [下載] 資料夾解壓縮檔案，將會獲得課程 1。  
  
3.  在根磁碟機上或附近建立一個子資料夾，例如 C:\Tutorial。  
  
4.  移動**adventure-運作方式-多維度-教學課程-projects.zip**到子資料夾。  
  
5.  以滑鼠右鍵按一下該檔案，然後選取 [Extract All(全部解壓縮)]。  
  
6.  瀏覽至 **Lesson 4 Start** 資料夾以尋找 **Analysis Services Tutorial.sln** 檔案。  
  
## <a name="loading-and-processing-the-enhanced-project"></a>載入和處理增強型專案  
  
1.  在[!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]上**檔案**功能表上，按一下 **關閉方案**關閉您不會使用的檔案。  
  
2.  在 [檔案] 功能表上，指向 [開啟舊檔]，再按一下 [專案/方案]。  
  
3.  瀏覽到您解壓縮教學課程專案檔案的位置。  
  
    尋找名為 **Lesson 4 Start**的資料夾，然後按兩下 Analysis Services Tutorial.sln。  
  
4.  將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 教學課程專案的增強型版本部署到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的本機執行個體，或另一個執行個體，並確認處理已順利完成。  
  
## <a name="understanding-the-enhancements-to-the-project"></a>了解專案的增強功能  
這個專案的增強型版本與您在前面 3 課所完成的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 教學課程專案的版本不同。 下列章節將描述其差異。 在繼續本教學課程的其餘課程之前，請檢閱這項資訊。  
  
### <a name="data-source-view"></a>[資料來源檢視]  
增強型專案中的資料來源檢視多包含一個事實資料表及四個維度資料表，它們來自 [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)] 資料庫。  
  
請注意，資料來源檢視中的十個資料表使得 <All Tables> 圖表變得很擁擠， 以致於不容易了解資料表之間的關聯性及尋找特定資料表。 為了解決這個問題，資料表分成兩個邏輯圖表：[網際網路銷售] 圖表和 [轉售商銷售] 圖表。 這些圖表各以單一事實資料表為中心。 建立邏輯圖表可讓您檢視及使用資料來源檢視中的資料表的特定子集，而不是檢視單一圖表中的所有資料表及其關聯性。  
  
#### <a name="internet-sales-diagram"></a>Internet Sales 圖表  
[網際網路銷售] 圖表包含透過網際網路直接向客戶銷售 [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] 產品之相關資料表。 圖表中的資料表為 4 個維度資料表和 1 個事實資料表，這些是您在第 1 課新增至 **Adventure Works DW 2012** 資料來源檢視中的資料表。 這些資料表如下：  
  
-   **地理位置**  
  
-   **客戶**  
  
-   **日期**  
  
-   **產品**  
  
-   **InternetSales**  
  
#### <a name="reseller-sales-diagram"></a>轉售商銷售圖表  
[轉售商銷售] 圖表包含與轉售商銷售 [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] 產品有關的資料表。 此圖表包含下列七個維度資料表及一個事實資料表，它們來自 [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)] 資料庫：  
  
-   **轉售商**  
  
-   **促銷**  
  
-   **SalesTerritory**  
  
-   **Geography**  
  
-   **日期**  
  
-   **產品**  
  
-   **員工**  
  
-   **ResellerSales**  
  
請注意，**DimGeography**、**DimDate** 和 **DimProduct** 資料表同時用於 [網際網路銷售額] 圖表和 [轉售商銷售] 圖表。 維度資料表可連結至多個事實資料表。  
  
### <a name="database-and-cube-dimensions"></a>資料庫和 Cube 維度  
[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 教學課程專案包含 5 個新資料庫維度，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 教學課程 Cube 包含這 5 個與 Cube 維度相同的維度。 這些維度已定義為具有階層和屬性，這些已使用具名計算、構成要素成員索引鍵和顯示資料夾來修改過。 下列清單描述的是新的維度。  
  
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
  
