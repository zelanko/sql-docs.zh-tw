---
title: 應用裝置安裝和設定-Analytics Platform System |Microsoft 文件
description: 將逐步引導 Analytics Platform System (APS) 應用裝置系統管理員可以透過設定和開始使用新的裝置的初始步驟。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5b6aa75cdab85fce9ef308d3e853ddb0107c28ee
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/19/2018
ms.locfileid: "31538618"
---
# <a name="appliance-installation-and-configuration-for-analytics-platform-system"></a>Analytics Platform System 的應用裝置安裝和設定
將逐步引導 Analytics Platform System (APS) 應用裝置系統管理員可以透過設定和開始使用新的裝置的初始步驟。  
  
<!-- MISSING LINKS ## <a name="BeforeYouBegin"></a>Before You Begin  
Before you begin to install, configure, and use your new appliance, we recommend reviewing information about the appliance components. Review the following to familiarize yourself with the appliance:  
  
-   Review [Understanding the Appliance Nodes and Hardware (SQL Server PDW)](assetId:///f60f419f-d1e1-403d-8cf9-07e7ef6d6627) to be sure you understand the components included in your new appliance.  
  
-   Review [Connecting to SQL Server PDW (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808) to understand how and when appliance administrators will connect to each appliance node.  
-->

## <a name="InstallHardware"></a>1.安裝的硬體  
若要停駐在您的資料中心的其他項目的傳遞新的裝置。  
  
> [!IMPORTANT]  
> 在某些情況下，您 IHV 將解除封裝、 機架，並在資料中心連接您的應用裝置。 如果因此不需要這些指示，而您可以跳到[3。設定設備](#ConfigureAppliance)下一節。  
  
如果您 IHV 未執行硬體安裝時，請使用下列步驟來安裝的硬體。  
  
|||  
|-|-|  
|**工作**|**說明**|  
|確認文件|確認您已從您的獨立硬體廠商 (IHV) 收到所有必要的文件和資訊。 請參閱[資訊，以取得從您 IHV &#40;Analytics Platform System&#41;](information-to-obtain-from-your-ihv.md)。|  
|安裝硬體|確認資料中心可以容納應用裝置。 將應用裝置元件移到資料中心。 機架網路交換器，多個 Pdu，及連接纜線。 請參閱[硬體安裝&#40;Analytics Platform System&#41;](hardware-installation.md)。|  
  
## <a name="PowerOnAppliance"></a>2.應用裝置上的電源  
  
|||  
|-|-|  
|**工作**|**說明**|  
|應用裝置上的電源|必要的順序，確認 會發生任何錯誤視等候每個應用裝置元件節點上的電源。|  
  
## <a name="ConfigureAppliance"></a>3.設定應用裝置  
  
|||  
|-|-|  
|**工作**|**說明**|  
|||  
|設定使用 SQL Server PDW 應用裝置**Configuration Manager**|使用組態管理員來設定您的應用裝置上的應用裝置密碼、 時區、 網路和防火牆設定、 安全性憑證，以及效能和其他設定。 請參閱[應用裝置組態&#40;Analytics Platform System&#41;](appliance-configuration.md)。|  
  
> [!WARNING]  
> 組態變更只應該可以使用 SQL Server PDW**Configuration Manager**。 變更不會公開透過**Configuration Manager**不支援。 例如，SQL Server PDW 應用裝置僅支援英文 （美國） 語言設定。  
  
## <a name="SoftwareServicing"></a>4.設定軟體服務  
  
|||  
|-|-|  
|**工作**|**說明**|  
|適用於 SQL Server PDW 更新|（選擇性）您可能需要一或多個 SQL Server PDW 將更新套用至您的 SQL Server PDW 軟體更新為最新版本。 請參閱[套用 Analytics Platform System Hotfix &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)。|  
|設定 Windows Server Update Services|設定應用裝置，以接收來自 Windows Server Update Services 支援軟體更新。 請參閱[下載並套用 Microsoft 更新&#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md)。|  
  
## <a name="NextSteps"></a>接下來的步驟  
您已完成所有先前的步驟之後，您的應用裝置可供使用。 您或您所在位置的其他人員可以進行下列工作。  
  
|||  
|-|-|  
|**工作**|**說明**|  
|安裝 SQL Server PDW 驅動程式，以及設定連接性|設定使用 SQL Server Data Tools、 sqlcmd、 business intelligence 軟體或其他工具連接到 SQL Server PDW 的本機電腦。 <!-- MISSING LINKS See [Client Tools (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808).-->|  
|建立登入與伺服器角色並指派權限|規劃並建立可讓使用者登入 SQL Server PDW 的適當權限的登入與伺服器角色。 <!-- MISSING LINKS See [PDW Permissions &#40;SQL Server PDW&#41;](../sqlpdw/pdw-permissions-sql-server-pdw.md).-->|  
|設定 Azure 資料管理閘道|閘道器可讓 Azure 的使用者存取內部部署 AP 資料公開 AP 安全 OData 摘要的資料。 閘道已安裝的控制節點上。 Microsoft 尋求協助的組態。|  
|監視查詢和應用裝置的使用者|若要監視的查詢和應用裝置的使用者使用系統管理員主控台和其他資源。 請參閱[使用管理主控台來監視設備&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)<!-- MISSING LINKS and [User Sessions &#40;SQL Server PDW&#41;](../sqlpdw/user-sessions-sql-server-pdw.md)-->。|  
|將資料載入 SQL Server PDW|資料載入至您的應用裝置。 <!-- MISSING LINKS See [Load &#40;SQL Server PDW&#41;](../sqlpdw/load-sql-server-pdw.md).-->|  
|建立嚴重損壞復原計畫|規劃如何將保護您的資料，從硬體故障或資料會覆寫。 建立計劃使用定期備份和還原計畫，如果發生資料損毀或遺失。 <!-- MISSING LINKS See [Create a Disaster Recovery Plan &#40;SQL Server PDW&#41;](../sqlpdw/create-a-disaster-recovery-plan-sql-server-pdw.md).-->|  
|監視應用裝置|使用系統檢視表，記錄檔和系統管理員主控台監視應用裝置狀態、 運行狀況和效能。 請更正或報告任何問題。 請參閱[應用裝置健康情況監視&#40;Analytics Platform System&#41;](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md)。|  
