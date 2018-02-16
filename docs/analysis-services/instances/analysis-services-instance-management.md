---
title: "Analysis Services 執行個體管理 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0455fa4f-b92d-4a8b-a8f0-f2a268a5c84e
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 1540e9a5422b3a15081b1a25c813ef87ed8d6c0c
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="analysis-services-instance-management"></a>Analysis Services 執行個體管理

  Analysis Services 的執行個體是當做作業系統服務執行之 **msmdsrv.exe** 可執行檔的複本。 每一個執行個體與相同伺服器上的其他執行個體之間完全獨立，而且擁有它自己的組態設定、權限、通訊埠、啟動帳戶、檔案儲存體和伺服器模式屬性。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的每一個執行個體都會在所定義之登入帳戶的安全性內容中，以 Windows 服務 Msmdsrv.exe 執行。  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 預設執行個體的服務名稱是 MSSQLServerOLAPService。  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 之每一個具名執行個體的服務名稱是 MSOLAP$InstanceName。  
  
> [!NOTE]  
>  如果安裝了多個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體，安裝程式就會同時安裝重新導向程式服務，這會與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務進行整合。 重新導向程式服務會負責將用戶端導向 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的適當具名執行個體。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務一律會在本機服務帳戶的安全性內容中執行，本機服務帳戶是 Windows 針對不會存取本機電腦外部資源的服務所使用的受限使用者帳戶。  
  
 多重執行個體表示您可以在相同硬體上安裝多個伺服器執行個體來進行擴充。 尤其對於 Analysis Services 而言，這也表示您可以在相同伺服器上安裝多個執行個體 (每個執行個體都設定為在特定模式下執行) 來支援不同的伺服器模式。  
  
 伺服器模式是一種伺服器屬性，可決定用於該執行個體的儲存體和記憶體架構。 在多維度模式下執行的伺服器會使用針對多維度 Cube 資料庫和資料採礦模型所建立的資源管理層。 相較之下，表格式伺服器模式會使用 VertiPaq 記憶體中分析引擎和資料壓縮，在要求時彙總資料。  
  
 儲存體和記憶體架構之間的差異表示單一 Analysis Services 執行個體將會執行表格式資料庫或多維度資料庫，但不會兩者都執行。 伺服器模式屬性會決定哪一種類型的資料庫在執行個體上執行。  
  
 在安裝過程中，當您指定將在伺服器上執行的資料庫類型時，將會設定伺服器模式。 若要支援所有可用模式，您可以安裝多個 Analysis Services 執行個體，每個執行個體都使用與您建立之專案相對應的伺服器模式來部署。  
  
 通常，您必須執行的大部分管理工作不會因模式而改變。 您身為 Analysis Services 系統管理員，可以使用相同的程序和指令碼來管理網路上的任何 Analysis Services 執行個體，不論其安裝方式為何。  
  
> [!NOTE]  
>  例外狀況是 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 部署的伺服器管理一定會在 SharePoint 伺服陣列的內容中進行。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 與其他伺服器模式不同之處在於它永遠都是單一執行個體，而且一定會透過 SharePoint 管理中心或 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 組態工具來管理。 雖然可在 SQL Server Management Studio 或 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 中連接到 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]for SharePoint，但是不需要這樣做。 SharePoint 伺服器陣列包含的基礎結構會同步處理伺服器狀態及監視伺服器可用性。 使用其他工具可能會干擾這些作業。 如需 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 伺服器管理的詳細資訊，請參閱 [Power Pivot for SharePoint &#40;SSAS&#41;](../../analysis-services/power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
|連結|工作描述|  
|----------|----------------------|  
|[後續安裝組態 &#40;Analysis Services &#41;](../../analysis-services/instances/post-install-configuration-analysis-services.md)|描述完成或修改 Analysis Services 安裝的必要工作和選擇性工作。|  
|[連接到 Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)|描述建立或清除連接時所用的連接字串屬性、用戶端程式庫、驗證方法和步驟。|  
|[監視 Analysis Services 執行個體](../../analysis-services/instances/monitor-an-analysis-services-instance.md)|描述用於監視伺服器執行個體的工具和技術，包括如何使用效能監視器和 SQL Server Profiler。|  
|[高可用性與延展性](../../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md)|說明提高 Analysis Services 資料庫可用性與延展性的最常用技術。 |  
|[Analysis Services 的全球化案例](../../analysis-services/globalization-scenarios-for-analysis-services.md)|說明語言和定序支援、變更這兩個屬性的步驟，以及設定和測試語言和定序行為的秘訣。|  
|[Analysis Services 中的記錄作業](../../analysis-services/instances/log-operations-in-analysis-services.md)|描述記錄檔並說明如何設定它們。|  
  
  
## <a name="see-also"></a>另請參閱  
 [比較表格式和多維度解決方案 &#40;SSAS&#41;](../../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)   
 [Power Pivot 組態工具](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)   
 [管理中心的 PowerPivot 伺服器管理和組態](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [判斷 Analysis Services 執行個體的伺服器模式](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
