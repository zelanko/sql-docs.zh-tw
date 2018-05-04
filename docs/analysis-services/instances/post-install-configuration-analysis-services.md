---
title: 後續安裝組態 (Analysis Services) |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6993aa4cea9c21b41e71048497cf524335b72366
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="post-install-configuration-analysis-services"></a>後續安裝組態 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  安裝 Analysis Services 之後，還必須進一步設定才能讓伺服器可完整運作並可供一般使用。 本節將介紹完成安裝所需的這些額外設定工作。 視連接需求而定，您可能還必須設定驗證 (請參閱 [連接到 Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md))。  
  
 之後，如果您的資料庫已就緒可供部署，就必須執行額外的工作。 也就是說，您必須為資料庫設定角色成員資格讓使用者能存取資料、設計資料庫備份和復原策略，以及判斷是否需要排程處理工作負載來定期重新整理資料。 可以在這些連結中找到資料庫部署和管理的詳細資訊：[多維度模型資料庫](../../analysis-services/multidimensional-models/multidimensional-model-databases-ssas.md)和[表格式模型資料庫](../../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md)。  
  
## <a name="instance-configuration"></a>執行個體組態  
 Analysis Services 是可複寫的服務，表示您可以在單一伺服器上安裝多個服務執行個體。 每一個額外執行個體都是以具名執行個體的形式使用 SQL Server 安裝程式個別安裝，然後個別加以設定以支援原先預期的用途。 例如，開發伺服器可能會執行飛行記錄器或使用預設值進行資料儲存，但是在支援實際執行工作負載的伺服器上，您可能會變更這些設定。 此外，在其他服務所共用的硬體上安裝 Analysis Services 執行個體也是另一個需要調整系統組態的範例。 在同一個硬體上主控多個資料密集的應用程式時，您可能想設定伺服器屬性降低記憶體臨界值，以便最佳化所有應用程式之間的可用資源。  
  
## <a name="post-installation-tasks"></a>後續安裝工作  
  
|連結|工作描述|  
|----------|----------------------|  
|[設定 Windows 防火牆以允許 Analysis Services 存取](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|在 Windows 防火牆中建立輸入規則，以便透過 Analysis Services 執行個體所使用的 TCP 通訊埠來傳送要求。 這是必要的工作。 除非定義輸入防火牆規則，否則就無法從遠端電腦存取 Analysis Services。|  
|[將伺服器系統管理員權限授與 Analysis Services 執行個體](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)|在安裝期間，您必須將至少一個使用者帳戶加入至 Analysis Services 執行個體的管理員角色。 許多例行伺服器作業 (例如從外部關聯式資料庫處理資料) 都需要管理權限。 請透過本主題中的資訊來加入或修改管理員角色的成員資格。|
|[在執行 SQL Server 的電腦上設定防毒軟體](https://support.microsoft.com/kb/309422) |您可能需要設定掃描軟體，例如防毒和反間諜軟體應用程式，以排除 SQL Server 資料夾和檔案類型。 如果掃描軟體在 Analysis Services 需要使用程式或資料檔案時鎖定它，就會發生服務中斷或資料損毀。 |
|[設定服務帳戶 &#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md)|在安裝期間，會佈建 Analysis Services 服務帳戶，並提供適當權限以允許對程式可執行檔和資料庫檔案進行控制存取。 做為後續安裝工作，您現在應該考慮在執行其他工作時，是否允許使用服務帳戶。 處理和查詢工作負載都可以在服務帳戶下執行。 只有在服務帳戶具有適當的權限時，這些作業才會成功。|  
|[註冊伺服器群組中的 Analysis Services 執行個體](../../analysis-services/instances/register-an-analysis-services-instance-in-a-server-group.md)|SQL Server Management Studio (SSMS) 可讓您建立伺服器群組，方便組織 SQL Server 執行個體。 包含多個伺服器執行個體的可延展部署在伺服器群組中更容易管理。 請透過本主題的資訊，在 SSMS 中將 Analysis Services 執行個體組織成群組。|  
|[判斷 Analysis Services 執行個體的伺服器模式](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)|在安裝期間，您必須選擇在伺服器上執行的伺服器模式，這個模式會決定模型的類型 (多維度或表格式)。 如果您不確定伺服器模式，請透過本主題中的資訊來判斷已安裝的模式。|  
|[重新命名 Analysis Services 執行個體](../../analysis-services/instances/rename-an-analysis-services-instance.md)|如果多個執行個體的伺服器模式都不相同，您可以使用描述性名稱加以區別，也可以區分組織中的部門或小組主要使用的執行個體。 如果希望變更執行個體名稱讓您在管理安裝時更容易，請透過本主題中的資訊來了解要如何變更名稱。|  
  
## <a name="next-steps"></a>後續步驟  
 了解如何使用用戶端程式庫，從 Microsoft 應用程式或自訂應用程式連接至 Analysis Services。 視方案需求而定，您可能還必須為服務設定 Kerberos 驗證。 有跨網域界限需求的連接就需要 HTTP 存取。 如需有關後續步驟的指示，請參閱＜ [Connect to Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md) ＞。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2016 安裝](../../database-engine/install-windows/installation-for-sql-server-2016.md)   
 [以多維度及資料採礦模式安裝 Analysis Services](http://msdn.microsoft.com/library/8a1f33e8-2bd6-4fb8-bd46-c86f2a067f60)   
 [安裝 Analysis Services](../../analysis-services/instances/install-windows/install-analysis-services.md)   
 [以 Power Pivot 模式安裝 Analysis Services](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
  
