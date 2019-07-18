---
title: 建立多維度模型使用 SQL Server Data Tools (SSDT) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SSAS, environments
- Analysis Services, development
- SQL Server Analysis Services, environments
- projects [Analysis Services]
- solutions [Analysis Services]
ms.assetid: 132ed779-3ec8-4734-9698-802116d1b017
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 915ce0ebc6ff9ecd68647deb1653bfab0e1c956d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66076172"
---
# <a name="creating-multidimensional-models-using-sql-server-data-tools-ssdt"></a>使用 SQL Server 資料工具 (SSDT) 建立多維度模型
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會提供兩個不同環境來建立、部署及管理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 方案： [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 這兩個環境都會實作專案系統。 如需有關 Visual Studio 專案的詳細資訊，請參閱 MSDN Library 中的 [以專案做為容器](https://go.microsoft.com/fwlink/?LinkId=63960) 。  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 是一個以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio 2010 為基礎的開發環境，用於建立及修改商業智慧方案。 運用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]，您可以建立包含 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件之定義 (Cube、維度等等) 的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案，這些都儲存在包含 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 指令碼語言 (ASSL) 元素的 XML 檔案中。 包含這些專案的方案也可以包含其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件的專案，其中包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，您可以開發 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案，成為方案中獨立於任何特定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的部分。 您可以將物件部署到測試伺服器上的執行個體，在開發期間進行測試，然後使用相同的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案，將物件部署到一或多個暫存或實際執行伺服器上的執行個體。 包括 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 在內之方案中的專案和項目，可以與原始程式碼控制整合在一起，例如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual SourceSafe。 如需使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中建立 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]專案的詳細資訊，請參閱 [建立 Analysis Services 專案 &#40;SSDT&#41;](create-an-analysis-services-project-ssdt.md)。 您也可以使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 直接連接到現有的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體，以便建立及修改 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件，而不需要使用專案以及在 XML 檔案中儲存物件定義。 如需詳細資訊，請參閱 [多維度模型資料庫 &#40;SSAS&#41;](multidimensional-model-databases-ssas.md)和 [在連線模式下連接至 Analysis Services 資料庫](connect-in-online-mode-to-an-analysis-services-database.md)。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 是主要是用於管理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]之執行個體的管理環境。 您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]來管理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件 (執行備份、處理等作業)，也可以使用 XMLA 指令碼直接在現有的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上建立新的物件。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 會提供一個 Analysis Server 指令碼專案，您可在其中開發及儲存使用多維度運算式 (MDX)、資料採礦延伸模組 (DMX) 和 XML for Analysis (XMLA) 所撰寫的指令碼。 通常 Analysis Server 指令碼專案是用於在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上 (例如資料庫和 Cube)，執行管理工作或重新建立物件。 這種專案可儲存成為方案的一部分，並與原始程式碼控制整合。 如需使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中建立 Analysis Server 指令碼專案的詳細資訊，請參閱 [SQL Server Management Studio 中的 Analysis Services 指令碼專案](../instances/analysis-services-scripts-project-in-sql-server-management-studio.md)。  
  
## <a name="introducing-solutions-projects-and-items"></a>方案、專案和項目的簡介  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 都提供專案，專案再組成方案。 方案可以包含多個專案，而專案通常包含多個項目。 當您建立專案時，會自動產生新方案，您可以視需要將其他專案加入現有的方案中。 專案包含的物件會視專案的類型而定。 每一個專案容器中的項目會以檔案儲存在檔案系統的專案資料夾中。  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 會在 [商業智慧專案] 專案類型之下包含下列專案。  
  
|專案|描述|  
|-------------|-----------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案|包含單一 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的物件定義。 如需如何建立 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案的詳細資訊，請參閱 [建立 Analysis Services 專案 &#40;SSDT&#41;](create-an-analysis-services-project-ssdt.md)。|  
|匯入 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 2008 資料庫|提供一個精靈，您可以用於建立新的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案，方法是從現有的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫匯入物件定義。|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案|包含一組 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的物件定義。 如需詳細資訊，請參閱 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)。|  
|報表專案精靈|提供精靈引導您使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]來建立報表專案。 如需詳細資訊，請參閱 [Reporting Services &#40;SSRS&#41;](../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)。|  
|報表模型專案|包含 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表模型的物件定義。 如需詳細資訊，請參閱 [Reporting Services &#40;SSRS&#41;](../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)。|  
|報表伺服器專案|包含一或多個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表的物件定義。 如需詳細資訊，請參閱 [Reporting Services &#40;SSRS&#41;](../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)。|  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 也包含數個專案類型，這些類型著重於各種查詢或指令碼，如下表所示。  
  
|專案|描述|  
|-------------|-----------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 指令碼|包含 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的 DMX、MDX 和 XMLA 指令碼，以及執行這些指令碼之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的連接。 如需詳細資訊，請參閱 [SQL Server Management Studio 中的 Analysis Services 指令碼專案](../instances/analysis-services-scripts-project-in-sql-server-management-studio.md)。|  
|SQL Server Compact 指令碼|包含 SQL Server Compact 的 SQL 指令碼，以及執行這些指令碼之 SQL Server Compact 執行個體的連接。|  
|SQL Server 指令碼|包含 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體的 XQuery 指令碼，以及執行這些指令碼之 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體的連接。 如需詳細資訊，請參閱 [SQL Server Database Engine](../../database-engine/sql-server-database-engine-overview.md)。|  
  
 如需有關方案和專案的詳細資訊，請參閱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] .NET 文件集或 MSDN Library 中的＜管理方案、專案和檔案＞。  
  
## <a name="choosing-between-sql-server-management-studio-and-sql-server-data-tools"></a>在 SQL Server Management Studio 和 SQL Server 資料工具之間做選擇  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的設計目的在於管理和設定 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]及 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中現有的物件。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的設計目的在於開發商業智慧方案，提供包含 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的功能。  
  
 下列是 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 與 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]之間的某些差異。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 會提供一個整合式環境來連接 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的執行個體，以便設定及管理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體內的物件。 透過指令碼的使用，也可以利用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 建立或修改 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件本身，但是 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 未針對物件設計和定義提供圖形介面。  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 提供一個整合式開發環境來開發商業智慧方案， 您可以在專案模式中使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ，此模式會使用專案和方案中所含之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 物件的 XML 架構定義。 在專案模式中使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ，也就代表 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 物件的變更會針對這些 XML 架構物件定義來進行，而且要等到部署方案之後，這些變更才會直接套用到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上的物件。 您也可以在線上模式中使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ，也就是說，直接連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體並使用現有資料庫中的物件。  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 會增強商業智慧應用程式的開發，因為您可以在有原始檔控制的多重使用者環境下處理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案，而不需要 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的作用中連接。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 會提供直接存取現有物件的方式來進行查詢和測試，並可用於快速實作先前撰寫之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的指令碼。 不過，一旦專案已經部署到生產環境後，搭配 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]資料庫及其物件時就必須小心。 這是為了避免直接在現有資料庫中複寫針對物件所進行的變更，以及針對原始產生之部署方案的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案所進行的變更。 如需詳細資訊，請參閱 [在開發階段使用 Analysis Services 專案和資料庫](work-with-analysis-services-projects-and-databases-in-development.md)和 [在實際執行環境中搭配 Analysis Services 專案及資料庫使用](work-with-analysis-services-projects-and-databases-in-production.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [建立 Analysis Services 專案 &#40;SSDT&#41;](create-an-analysis-services-project-ssdt.md)  
  
-   [設定 Analysis Services 專案屬性 &#40;SSDT&#41;](configure-analysis-services-project-properties-ssdt.md)  
  
-   [建立 Analysis Services 專案 &#40;SSDT&#41;](build-analysis-services-projects-ssdt.md)  
  
-   [部署 Analysis Services 專案 &#40;SSDT&#41;](deploy-analysis-services-projects-ssdt.md)  
  
-   [在開發階段使用 Analysis Services 專案和資料庫](work-with-analysis-services-projects-and-databases-in-development.md)  
  
-   [在實際執行環境中搭配 Analysis Services 專案及資料庫使用](work-with-analysis-services-projects-and-databases-in-production.md)  
  
## <a name="see-also"></a>另請參閱  
 [建立 Analysis Services 專案 &#40;SSDT&#41;](create-an-analysis-services-project-ssdt.md)   
 [SQL Server Management Studio 中的 Analysis Services 指令碼專案](../instances/analysis-services-scripts-project-in-sql-server-management-studio.md)   
 [多維度模型資料庫 &#40;SSAS&#41;](multidimensional-model-databases-ssas.md)  
  
  
