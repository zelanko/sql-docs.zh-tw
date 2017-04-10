---
title: "Integration Services (SSIS) 專案及解決方案 | Microsoft Docs"
ms.custom: ""
ms.date: "08/24/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.importprojectwizard.f1"
helpviewer_keywords: 
  - "專案 [Integration Services], 建立"
  - "資料夾 [Integration Services], 專案"
  - "檔案 [Integration Services], 專案"
  - "資料夾 [Integration Services]"
  - "專案 [Integration Services], 關於專案"
ms.assetid: 28ea8120-0a79-4029-93f0-07d521b32bee
caps.latest.revision: 63
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 62
---
# Integration Services (SSIS) 專案及解決方案
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 以用於開發 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝。  
  
 當您將封裝部署到 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫或 [!INCLUDE[ssIS](../includes/ssis-md.md)] 封裝存放區時，便要使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務來管理封裝。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務只可以在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中使用。 如需服務的詳細資訊，請參閱 [Integration Services 服務 &#40;SSIS 服務&#41;](../integration-services/service/integration-services-service-ssis-service.md)。 如需封裝部署的詳細資訊，請參閱[舊版封裝部署 &#40;SSIS&#41;](../integration-services/packages/legacy-package-deployment-ssis.md)。  
  
 當您將 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器時，則是在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中使用 Transact-SQL 檢視和預存程序來管理專案。 如需專案部署的詳細資訊，請參閱[部署 Integration Services (SSIS) 專案和封裝](https://msdn.microsoft.com/library/hh213290.aspx)。 如需 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器的詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 伺服器](https://msdn.microsoft.com/library/ms137731.aspx)。  
  
 如需 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 和 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 的概觀，請參閱 [Integration Services &#40;SSIS&#41; 開發和管理工具](https://msdn.microsoft.com/library/ms140028.aspx)%20and%20Studio%20Environments.md)。  
  
## Integration Services 專案包含封裝  
 專案是讓您開發 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝的容器。  
  
 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案會儲存及分組與此封裝有關的檔案。 例如，專案會包含建立特定擷取、轉送和載入 (ETL) 方案時所需的檔案。  
  
 在您建立 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案之前，您應該先熟悉這一種專案的基本內容。 在您了解專案所包含的內容之後，您可以開始建立及使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
## Integration Services 專案中的資料夾  
 下圖顯示 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中位於 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 專案內的資料夾。  
  
 ![Integration Services 專案中的資料夾](../integration-services/media/solutionexplorer.gif "Integration Services 專案中的資料夾")  
  
 下表描述顯示在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案中的資料夾。  
  
|資料夾|說明|  
|------------|-----------------|  
|[!INCLUDE[ssIS](../includes/ssis-md.md)] Packages|包含封裝。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 封裝](../integration-services/integration-services-ssis-packages.md)。|  
|其他|包含封裝檔案之外的檔案。|  
  
## Integration Services 專案中的檔案  
 當您將新的或現有的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案加入方案時，[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 會建立副檔名為 .dtproj、.dtproj.user 和 .database 的專案檔案。  
  
-   *.dtproj 檔案包含有關專案組態以及封裝之類項目的資訊。  
  
-   *.dtproj.user 檔案包含有關您在使用專案時的偏好設定之資訊。  
  
-   *.database 檔案包含 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 在開啟 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案時所需的資訊。  
  
## Integration Services 專案中的目標版本  
 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，您可以建立、維護和執行目標為 SQL Server 2016、SQL Server 2014 或 SQL Server 2012 的封裝。  
  
 在方案總管中，在 Integration Services 專案上按一下滑鼠右鍵，然後選取 [屬性] 以開啟專案的屬性頁。 在 [組態屬性]  的 [一般] 索引標籤中，選取 [TargetServerVersion]  屬性，然後選擇 SQL Server 2016、SQL Server 2014 或 SQL Server 2012。  
  
 ![TargetServerVersion property in project properties dialog box](../integration-services/media/targetserverversion2.png "TargetServerVersion property in project properties dialog box")  
  
## 方案包含專案  
 方案是將您在開發端對端商務方案時所使用的專案分組，並對其進行管理的一個容器。 方案可讓您將多個專案當做一個單位來處理，並將對商務方案有幫助的一個或多個相關專案集合在一起。  
  
 方案可包含不同類型的專案。 若要使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師建立 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝，請在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 所提供的解決方案中利用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案來進行。  
  
 當您建立新的解決方案時，[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 會將 [解決方案] 資料夾加入方案總管中，並建立副檔名為 .sln 和 .suo 的檔案：  
  
-   *.sln 檔案包含方案組態的相關資訊，並列出方案中的專案。  
  
-   *.suo 檔案包含關於使用方案之喜好設定的資訊。  
  
 雖然 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 會在您新建專案時自動建立解決方案，但是您也可以建立空白的解決方案，並在稍後加入專案。  
  
> **注意**：依預設，當您在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中建立新的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案時，此解決方案不會顯示在 [專案總管] 窗格中。 若要變更這個預設行為，請按一下 [工具] 功能表上的 [選項]。 在 [選項] 對話方塊中，展開 [專案和方案]，然後按一下 [一般]。 在 [一般] 頁面上，選取 [永遠顯示方案]。  
  
## 相關工作  
 [在方案中加入或移除 Integration Services 專案](../Topic/Add%20or%20Remove%20an%20Integration%20Services%20Project%20in%20a%20Solution.md)  
  
 [建立新的 Integration Services 專案](../Topic/Create%20a%20New%20Integration%20Services%20Project.md)  
  
 [將項目加入 Integration Services 專案](../Topic/Add%20an%20Item%20to%20an%20Integration%20Services%20Project.md)  
  
 [複製專案項目](../Topic/Copy%20Project%20Items.md)  
  
## 相關內容  
 [部署 Integration Services 專案](../Topic/Development%20of%20an%20Integration%20Services%20Project.md)  
  
  