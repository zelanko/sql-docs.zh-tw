---
title: Integration Services (SSIS) 專案和方案 | Microsoft Docs
ms.custom: ''
ms.date: 09/20/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: vanto
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.importprojectwizard.f1
helpviewer_keywords:
- projects [Integration Services], creating
- folders [Integration Services], projects
- files [Integration Services], projects
- folders [Integration Services]
- projects [Integration Services], about projects
ms.assetid: 28ea8120-0a79-4029-93f0-07d521b32bee
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 50938fe4f3be40f280340fff5bfbca23ac8b1b44
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "71680979"
---
# <a name="integration-services-ssis-projects-and-solutions"></a>Integration Services (SSIS) 專案及解決方案

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 以用於開發 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝。  
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 套件位在專案中。 若要建立及使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案，您必須安裝 [SQL Server Data Tools](../ssdt/download-sql-server-data-tools-ssdt.md)。 如需詳細資訊，請參閱[安裝 Integration Services](../integration-services/install-windows/install-integration-services.md)。  
  
 當您在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中建立新的 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 專案時，[新增專案]  對話方塊將包含 [Integration Services 專案]  範本。 此專案範本會建立包含單一封裝的新專案。
  
## <a name="projects-and-solutions"></a>專案和方案  
 專案會儲存在方案中。 您可以先建立方案，然後將 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案加入方案。 如果沒有方案存在， [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 會在您第一次建立專案時自動為您建立一個方案。 方案可以包含多個不同類型的專案。  
  
> [!TIP]  
>  根據預設，當您在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中建立新的專案時，方案不會顯示在方案總管  窗格中。 若要變更這個預設行為，請按一下 [工具]  功能表上的 [選項]  。 在 [選項]  對話方塊中，展開 [專案和方案]  ，然後按一下 [一般]  。 在 [一般]  頁面上，選取 [永遠顯示方案]  。  

## <a name="solutions-contain-projects"></a>方案包含專案  
 方案是將您在開發端對端商務方案時所使用的專案分組，並對其進行管理的一個容器。 方案可讓您將多個專案當做一個單位來處理，並將對商務方案有幫助的一個或多個相關專案集合在一起。  
  
 方案可包含不同類型的專案。 若要使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師建立 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝，請在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 所提供的解決方案中利用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]專案來進行。  
  
 當您建立新的解決方案時， [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 會將 [解決方案] 資料夾加入方案總管中，並建立副檔名為 .sln 和 .suo 的檔案：  
  
-   *.sln 檔案包含方案組態的相關資訊，並列出方案中的專案。  
  
-   *.suo 檔案包含關於使用方案之喜好設定的資訊。  
  
 雖然 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 會在您新建專案時自動建立解決方案，但是您也可以建立空白的解決方案，並在稍後加入專案。  
   
## <a name="integration-services-projects-contain-packages"></a>Integration Services 專案包含封裝  
 專案是讓您開發 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝的容器。  
  
 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案會儲存及分組與此封裝有關的檔案。 例如，專案會包含建立特定擷取、轉送和載入 (ETL) 方案時所需的檔案。  
  
 在您建立 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案之前，您應該先熟悉這一種專案的基本內容。 在您了解專案所包含的內容之後，您可以開始建立及使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
## <a name="folders-in-integration-services-projects"></a>Integration Services 專案中的資料夾  
 下圖顯示 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中位於 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]專案內的資料夾。  
  
![ssis-solution-explorer.png](media/ssis-solution-explorer.png)
  
 下表描述顯示在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案中的資料夾。  
  
|資料夾|描述|  
|------------|-----------------|
|連接管理員|包含專案連線管理員。 如需詳細資訊，請參閱 [Integration Services (SSIS) 連線](../integration-services/connection-manager/integration-services-ssis-connections.md)。|
|[!INCLUDE[ssIS](../includes/ssis-md.md)] Packages|包含封裝。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 封裝](../integration-services/integration-services-ssis-packages.md)。|  
|套件組件|包含可以重複使用或匯入的套件組件。 如需詳細資訊，請參閱[使用控制流程套件組件在套件之間重複使用控制流程](reuse-control-flow-across-packages-by-using-control-flow-package-parts.md)
|其他|包含封裝檔案之外的檔案。|  
  
## <a name="files-in-integration-services-projects"></a>Integration Services 專案中的檔案  
 當您將新或現有的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案新增至解決方案時，[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 會建立副檔名為 .dtproj、.dtproj.user、.database 和 Project.params 的專案檔案。 
  
-   *.dtproj 檔案包含有關專案組態以及封裝之類項目的資訊。  
  
-   *.dtproj.user 檔案包含有關您在使用專案時的偏好設定之資訊。  
  
-   *.database 檔案包含 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 在開啟 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案時所需的資訊。

-   Project.params 檔案包含與[專案參數](integration-services-ssis-package-and-project-parameters.md)相關的資訊。
  
## <a name="version-targeting-in-integration-services-projects"></a>Integration Services 專案中的目標版本  
 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，您可以建立、維護和執行目標為 SQL Server 2017、SQL Server 2016、SQL Server 2014 或 SQL Server 2012 的套件。  
  
 在方案總管中，在 Integration Services 專案上按一下滑鼠右鍵，然後選取 [屬性]  以開啟專案的屬性頁。 在 [設定屬性]  的 [一般]  索引標籤中，選取 TargetServerVersion  屬性，然後選擇 SQL Server 2017、SQL Server 2016、SQL Server 2014 或 SQL Server 2012。  
  
 ![專案屬性對話方塊中的 TargetServerVersion 屬性](../integration-services/media/targetserverversion2.png "專案屬性對話方塊中的 TargetServerVersion 屬性")  

## <a name="create-a-new-integration-services-project"></a>建立新的 Integration Services 專案  
  
1.  開啟 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]。  
  
2.  在 **[檔案]** 功能表上，指向 **[開新檔案]** ，然後按一下 **[專案]** 。  
  
3.  在 [新增專案]  對話方塊中，選取 [商業智慧]  ，然後選取 [Integration Services 專案]  範本。  
  
     **[Integration Services 專案]** 範本會建立一個包含單一、空白封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。

  ![ssis-ssdt-new-project.png](media/ssis-ssdt-new-project.png)
  
4.  (選擇性) 編輯專案名稱和位置。  
  
     方案名稱會自動更新為符合專案名稱。  
  
5.  若要為方案檔建立個別的資料夾，請選取 **[為方案建立目錄]** 。 這是預設選項。  
  
6.  如果電腦上安裝了原始檔控制軟體，請選取 **[加入至原始檔控制]**  以將專案與原始檔控制相關聯。  
  
7.  如果原始檔控制軟體是 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe，則 **[Visual SourceSafe 登入]** 對話方塊會開啟。 請在 **[Visual SourceSafe 登入]** 中，提供使用者名稱、密碼，以及 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe 資料庫的名稱。 按一下 **[瀏覽]** 找出資料庫。  
  
    > **注意**：若要檢視和變更選取的原始檔控制外掛程式，以及設定原始檔控制環境，請按一下 [工具]  功能表上的 [選項]  ，然後展開 [原始檔控制]  節點。  
  
8.  按一下 [確定]  ，將方案加入 **方案總管** 中，並將專案加入方案中。  

## <a name="import-an-existing-project-with-the-import-project-wizard"></a>使用匯入專案精靈匯入現有專案
  
1.  在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中，按一下 [檔案]  功能表上的 [新增] >   [專案]  。  
  
2.  在 **[新增專案]** 視窗的 **[已安裝的範本]** 區域中，展開 **[Business Intelligence]** ，然後按一下 **[Integration Services]** 。  
  
3.  從專案類型清單中選取 **[Integration Services 匯入專案精靈]** 。  
  
4.  在 **[名稱]** 文字方塊中，為要建立的新專案輸入一個名稱。  
  
5.  在 **[位置]** 文字方塊中輸入專案的路徑或位置，或按一下 **[瀏覽]** 來選取一個路徑或位置。  
  
6.  在 **[方案名稱]** 文字方塊中輸入方案的名稱。  
  
7.  按一下 **[確定]** ，啟動 **[Integration Services 匯入專案精靈]** 對話方塊。  
  
8.  按 **[下一步]** ，切換到 **[選取來源]** 頁面。  
  
9. 如果您要從 **.ispac** 檔匯入，請在 [路徑]  文字方塊中鍵入路徑，包括檔案名稱。 按一下 **[瀏覽]** 導覽到您希望儲存方案的資料夾，並在 **[檔案名稱]** 文字方塊中輸入檔案名稱，然後按一下 **[開啟]** 。  
  
     如果您要從 [Integration Services 目錄]  匯入，請在 [伺服器名稱]  文字方塊中鍵入資料庫執行個體名稱，或按一下 [瀏覽]  ，然後選取包含該目錄的資料庫執行個體。  
  
     按一下 **[路徑]** 文字方塊旁的 **[瀏覽]** 、展開目錄中的資料夾、選取您要匯入的專案，然後按一下 **[確定]** 。  
  
     按 **[下一步]** ，切換到 **[檢閱]** 頁面。  
  
10. 檢閱資訊，然後按一下 **[匯入]** ，即可根據您所選取的現有專案建立一個專案。  
  
11. 選擇性：按一下 **[儲存報表]** ，將結果儲存到檔案中。  
  
12. 按一下 **[關閉]** ，關閉 **[Integration Services 匯入專案精靈]** 對話方塊。  

## <a name="add-a-project-to-a-solution"></a>將專案新增至方案 
 當您加入專案時，可以讓 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 建立全新的空白專案，也可以加入已經針對不同方案建立的專案。 只有當您可以在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中看到方案時，才能將專案加入至現有的方案。  
  
### <a name="add-a-new-project-to-a-solution"></a>將新專案加入方案  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，開啟您要在其中加入新 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案的方案，並執行下列其中之一：  
  
    -   以滑鼠右鍵按一下方案，再按一下 [加入]  ，然後按一下 [新增專案]  。  
  
    -   在 [檔案]  功能表上，指向 [加入]  ，然後按一下 [新增專案]  。  
  
2.  在 [加入新專案]  對話方塊中，按一下 [範本]  窗格內的 [Integration Services 專案]  。  
  
3.  (選擇性) 編輯專案名稱及位置。  
  
4.  按一下 [確定]  。  
  
### <a name="add-an-existing-project-to-a-solution"></a>將現有專案加入方案  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，開啟您要在其中加入現有 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案的方案，並執行下列其中之一：  
  
    -   以滑鼠右鍵按一下方案，指向 [加入]  ，然後按一下 [現有專案]  。  
  
    -   在 [檔案]  功能表上，按一下 [加入]  ，然後按一下 [現有專案]  。  
  
2.  在 [加入現有專案]  對話方塊中，瀏覽以找出您要加入的專案，然後按一下 [開啟]  。  
  
3.  專案會加入方案總管  中的方案資料夾。  
  
## <a name="remove-a-project-from-a-solution"></a>移除方案中的專案
 只有當您可以在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中看到方案時，才能從方案中移除專案。 看見方案之後，您就可以只保留一個專案，並移除其他所有專案。 等到只剩下一個專案之後，[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 就不會再顯示方案資料夾，而且您也不能移除最後一個專案。  
   
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，開啟您要從中移除 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案的方案。  
  
2.  在方案總管中，以滑鼠右鍵按一下專案，然後按一下 [卸載專案]  。  
  
3.  按一下 [確定]  確認移除。  

## <a name="add-an-item-to-a-project"></a>將項目新增至專案  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，開啟包含要在其中加入項目之 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案的方案。  
  
2.  在方案總管中，以滑鼠右鍵按一下專案，指向 [加入]  ，然後執行下列其中之一：  
  
    -   按一下 [新增項目]  ，然後從 [加入新項目]  對話方塊的 [範本]  窗格中選取範本。  
  
    -   按一下 [現有項目]  ，在 [加入現有項目]  對話方塊中瀏覽，以找到您要加入專案的項目，然後按一下 [加入]  。  
  
3.  新項目便會出現在 [方案總管] 中適當的資料夾內。  

## <a name="copy-project-items"></a>複製專案項目  
您可以在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案內或 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案之間複製物件。 您也可以在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 專案的其他類型之間、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 和 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]之間複製物件。 若要在兩個專案之間進行複製，專案必須在同一個 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 方案中。

1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟您要使用的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案或方案。  
  
2.  展開要從中進行複製的專案和項目資料夾。  
  
3.  以滑鼠右鍵按一下項目，然後按一下 [複製]  。  
  
4.  以滑鼠右鍵按一下要複製到其中的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案，然後按一下 [貼上]  。  
  
     這些項目會自動複製到正確的資料夾。 如果您將項目複製到不是套件的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案，則這些項目會複製到 [其他]  資料夾中。  

## <a name="next-steps"></a>後續步驟

- 下載並安裝 [SQL Server Data Tools](../ssdt/download-sql-server-data-tools-ssdt.md)。
- [SSIS 如何建立 ETL 封裝](ssis-how-to-create-an-etl-package.md)