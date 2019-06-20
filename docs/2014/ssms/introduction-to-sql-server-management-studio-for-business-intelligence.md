---
title: Business Intelligence for SQL Server Management Studio 簡介 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio for Integration Services
- SQL Server Management Studio for Reporting Services
- SQL Server Management Studio for Analysis Services
ms.assetid: ffaa77b7-03d0-4d7a-aa42-c5091a4f2ceb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ab38a4465ec03415f9c1d903419ccbe2b07e6a86
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63015902"
---
# <a name="introduction-to-sql-server-management-studio-for-business-intelligence"></a>適用於商業智慧的 SQL Server Management Studio 簡介
  若要存取、設定及管理 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 和 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]，請使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。 雖然這三種商業智慧技術全都依賴 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]，但是與每一項技術有關的管理工作則會有些微的差異。  
  
> [!NOTE]  
>  若要建立及修改 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]和 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 解決方案，請使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，而不要使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 是一個以 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[vsprvs](../includes/vsprvs-md.md)]為根據的開發環境。  
  
## <a name="managing-analysis-services-solutions-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 管理 Analysis Services 解決方案  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 可讓您管理 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件，例如執行備份及處理物件。  
  
 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 會提供一個 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 指令碼專案，您可在其中開發及儲存使用多維度運算式 (MDX)、資料採礦延伸模組 (DMX) 和 XML for Analysis (XMLA) 所撰寫的指令碼。 您可以使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 指令碼專案來執行管理工作或是在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體上重新建立物件，例如資料庫和 Cube。 例如，您可以在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 指令碼專案中開發 XMLA 指令碼，該指令碼會直接在現有的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體上建立新的物件。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 指令碼專案可儲存成為方案的一部分，並與原始程式碼控制整合。  
  
 如需有關如何使用[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]，請參閱 < [SQL Server Management Studio 中的 Analysis Services 指令碼專案](../analysis-services/instances/analysis-services-scripts-project-in-sql-server-management-studio.md)。  
  
## <a name="managing-integration-services-solutions-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 管理 Integration Services 解決方案  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 可讓您使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務來管理套件及監視執行中的套件。 您也可以使用 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 將封裝組織成資料夾、執行封裝、匯入及匯出封裝、移轉 Data Transformation Services (DTS) 封裝及升級 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝。  
  
## <a name="managing-reporting-services-projects-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 來管理 Reporting Services 專案  
 使用 SQL Server Management Studio 可啟用 Reporting Services 功能、管理服務和資料庫，以及管理角色和作業。  
  
 您可使用 [共用排程] 資料夾來管理共用排程，並管理報表伺服器資料庫 (ReportServer、ReportServerTempdb)。 當您將報表伺服器資料庫移到新的或另一個 SQL Server Database Engine ([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)]) 時，您也會在 Master 系統資料庫中建立 RSExecRole。 如需有關這些工作的詳細資訊，請參閱下列主題：  
  
-   [SQL Server Management Studio 中的 Reporting Services &#40;SSRS&#41;](../reporting-services/tools/reporting-services-in-sql-server-management-studio-ssrs.md)  
  
-   [管理報表伺服器資料庫&#40;SSRS 原生模式&#41;](../reporting-services/report-server/report-server-database-ssrs-native-mode.md)  
  
-   [建立 RSExecRole](../reporting-services/security/create-the-rsexecrole.md)  
  
 您也可以透過以下方式來管理伺服器：啟用及設定各種功能、設定伺服器預設值及管理角色和作業。 如需有關這些工作的詳細資訊，請參閱下列主題：  
  
-   [設定報表伺服器屬性 &#40;Management Studio&#41;](../reporting-services/tools/set-report-server-properties-management-studio.md)  
  
-   [建立、刪除或修改角色 &#40;Management Studio&#41;](../reporting-services/security/role-definitions-create-delete-or-modify.md)  
  
-   [啟用和停用 Reporting Services 的用戶端列印功能](../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用 SQL Server 資料工具 &#40;SSDT&#41; 建立多維度模型](../analysis-services/multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)   
 [SQL Server Data Tools 中的 reporting Services &#40;SSDT&#41;](../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md)  
  
  
