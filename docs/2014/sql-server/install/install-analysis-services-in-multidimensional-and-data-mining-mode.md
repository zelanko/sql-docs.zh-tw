---
title: 安裝 Analysis Services 多維度和資料採礦模式 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Analysis Services, about installing Analysis Services
- installing Analysis Services
- SSAS, installing
- Analysis Services, installing
- SQL Server Analysis Services, installing
ms.assetid: 8a1f33e8-2bd6-4fb8-bd46-c86f2a067f60
author: heidisteen
ms.author: heidist
manager: craigg
ms.openlocfilehash: 92460328b9d85ab5818679b12639618ffe2b0a14
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48149898"
---
# <a name="install-analysis-services-in-multidimensional-and-data-mining-mode"></a>以多維度及資料採礦模式安裝 Analysis Services
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供商業智慧應用程式的線上分析處理 (OLAP) 和資料採礦功能。 在此版本中，OLAP 資料庫和資料採礦模型都提供當您安裝[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中*多維度模式*。 多維度模式是執行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的三種伺服器模式之一， 也是預設模式。 如果您使用預設值安裝 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，則會取得執行多維度資料庫和資料採礦模型的執行個體。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 是一項多執行個體功能，表示您可以在單一電腦上安裝一個以上的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體，或是與舊版並存執行新的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體。 每個執行個體會有特定的伺服器模式。 使用其他模式需要您安裝其他伺服器執行個體。  
  
 您可以單獨安裝 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，或是一併安裝其他元件。 如果您只安裝[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，當您選取時，會安裝下列功能**Analysis Services**上的 [特徵選取] 頁面[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝精靈：  
  
-   用於執行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫和資料採礦模型的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器  
  
-   用於進行來源資料庫之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料存取的資料提供者  
  
-   SQL Server 組態管理員  
  
## <a name="choosing-additional-features"></a>選擇其他功能  
 Analysis Services OLAP 和資料倉儲方案將需要安裝其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件，才能開發、部署和管理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫。 下列其他功能是許多典型使用者案例的選項：  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]，用於建立和檢視 Analysis Services 資料結構和資料採礦模型。  
  
-   用戶端工具連接性元件，用於用戶端和伺服器，包括 Db-library、 ODBC 和 OLE DB 的網路程式庫之間的通訊。  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，用來移動、複製和轉換資料的一組圖形化和可程式化物件。  
  
-   管理工具，包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 和複寫監視器。  
  
## <a name="installation-tasks"></a>安裝工作  
 安裝工作包含下列項目：  
  
|連結|工作|  
|-----------|-----------|  
|[硬體和 Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md)並[設定 Windows 服務帳戶與權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。|執行安裝程式之前，請先檢查安裝 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 所需的必要條件，並決定要用來提供伺服器的帳戶。|  
|[從安裝精靈安裝 SQL Server 2014&#40;安裝程式&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)。|執行 SQL Server 安裝程式，安裝軟體。|  
|[設定 Windows 防火牆以允許 Analysis Services 存取](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|安裝程式結束後，您必須設定防火牆設定，以允許遠端連接伺服器。|  
|[物件和作業的存取權授權 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)|存取 Analysis Services 資料庫的使用者至少必須在伺服器上具有一個資料庫的「讀取」權限。|  
  
## <a name="related-content"></a>相關內容  
 您可以在下列主題中找到其他設定內容：  
  
 [以表格式模式安裝 Analysis Services](../../analysis-services/instances/install-windows/install-analysis-services.md)  
  
 [PowerPivot for SharePoint 2010 安裝](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
 [判斷 Analysis Services 執行個體的伺服器模式](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
 [SQL Server 資料採礦增益集](http://go.microsoft.com/fwlink/?LinkId=197091)  
  
 根據預設，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程序中不會安裝範例資料庫、範例程式碼和用戶端應用程式增益集。 若要安裝範例資料庫和範例程式碼，請參閱 [CodePlex 網站](http://go.microsoft.com/fwlink/?LinkId=87843)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL server 2012 版本支援的功能](http://go.microsoft.com/fwlink/?linkid=232473)   
 [語言和定序&#40;Analysis Services&#41;](../../../2014/analysis-services/languages-and-collations-analysis-services.md)   
 [升級 Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md)  
  
  
