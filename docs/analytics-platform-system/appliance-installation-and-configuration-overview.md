---
title: 設備安裝和設定-Analytics Platform System |Microsoft Docs
description: Analytics Platform System (APS) 設備系統管理員可以透過設定和開始使用您新的應用裝置的初始步驟將逐步引導。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5b6aa75cdab85fce9ef308d3e853ddb0107c28ee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63276344"
---
# <a name="appliance-installation-and-configuration-for-analytics-platform-system"></a>Analytics Platform System 的設備安裝和設定
Analytics Platform System (APS) 設備系統管理員可以透過設定和開始使用您新的應用裝置的初始步驟將逐步引導。  
  
<!-- MISSING LINKS ## <a name="BeforeYouBegin"></a>Before You Begin  
Before you begin to install, configure, and use your new appliance, we recommend reviewing information about the appliance components. Review the following to familiarize yourself with the appliance:  
  
-   Review [Understanding the Appliance Nodes and Hardware (SQL Server PDW)](assetId:///f60f419f-d1e1-403d-8cf9-07e7ef6d6627) to be sure you understand the components included in your new appliance.  
  
-   Review [Connecting to SQL Server PDW (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808) to understand how and when appliance administrators will connect to each appliance node.  
-->

## <a name="InstallHardware"></a>1.安裝硬體  
您新的應用裝置會傳遞到您的資料中心在 dock 拖板上。  
  
> [!IMPORTANT]  
> 在某些情況下，ihv 提供會打開封裝、 機架，並連線為您的設備，在資料中心。 如果是，這些指示不需要，您可以跳到[3。設定設備](#ConfigureAppliance)下一節。  
  
如果 ihv 提供未執行硬體安裝時，使用下列步驟來安裝的硬體。  
  
|||  
|-|-|  
|**工作**|**說明**|  
|確認文件|請確認您已從您的獨立硬體廠商 (IHV) 接收所有必要的文件和資訊。 請參閱[ihv 提供的資訊&#40;Analytics Platform System&#41;](information-to-obtain-from-your-ihv.md)。|  
|安裝硬體|確認資料中心可以容納應用裝置。 將設備元件移到資料中心。 機架的網路交換器，Pdu，並將纜線。 請參閱[硬體安裝&#40;Analytics Platform System&#41;](hardware-installation.md)。|  
  
## <a name="PowerOnAppliance"></a>2.在應用裝置上的電源  
  
|||  
|-|-|  
|**工作**|**說明**|  
|在應用裝置上的電源|等待確認，未發生錯誤的所需的必要順序，每個設備元件節點上的電源。|  
  
## <a name="ConfigureAppliance"></a>3.設定設備  
  
|||  
|-|-|  
|**工作**|**說明**|  
|||  
|使用 SQL Server PDW 設定設備**Configuration Manager**|使用 Configuration Manager 來設定您的應用裝置上的應用裝置密碼、 時區、 網路和防火牆設定、 安全性憑證，以及效能和其他設定。 請參閱[設備設定&#40;Analytics Platform System&#41;](appliance-configuration.md)。|  
  
> [!WARNING]  
> 組態變更只應在使用 SQL Server PDW**Configuration Manager**。 變更不會透過公開**Configuration Manager**不支援。 例如，SQL Server PDW 應用裝置僅支援英文 （美國） 語言設定。  
  
## <a name="SoftwareServicing"></a>4.設定軟體服務  
  
|||  
|-|-|  
|**工作**|**說明**|  
|適用於 SQL Server PDW 更新|（選擇性）您可能需要一或多個 SQL Server PDW 將更新套用至您的 SQL Server PDW 軟體更新為最新版本。 請參閱[套用 Analytics Platform System Hotfix &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)。|  
|設定 Windows Server Update Services|設定設備，以接收來自 Windows Server Update Services，支援軟體更新。 請參閱[下載並套用 Microsoft 更新&#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md)。|  
  
## <a name="NextSteps"></a>接下來的步驟  
您已完成所有上述步驟之後，您的應用裝置可供使用。 您或您所在位置的其他人員可以繼續執行下列工作。  
  
|||  
|-|-|  
|**工作**|**說明**|  
|安裝 SQL Server PDW 驅動程式和設定連線|設定本機電腦連接到 SQL Server PDW 中，使用 SQL Server Data Tools、 sqlcmd、 business intelligence 軟體或其他工具。 <!-- MISSING LINKS See [Client Tools (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808).-->|  
|建立登入和伺服器角色，並指派權限|規劃並建立可讓使用者登入 SQL Server PDW 的適當權限的登入和伺服器角色。 <!-- MISSING LINKS See [PDW Permissions &#40;SQL Server PDW&#41;](../sqlpdw/pdw-permissions-sql-server-pdw.md).-->|  
|設定 Azure 資料管理閘道|閘道會啟用 Azure 的使用者存取內部 AP 資料公開 AP 安全 OData 摘要的資料。 閘道已安裝在控制節點上。 Microsoft 尋求協助。|  
|監視查詢和應用裝置使用者|使用在管理主控台和其他資源來監視查詢和應用裝置的使用者。 請參閱[使用管理主控台來監視設備&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)<!-- MISSING LINKS and [User Sessions &#40;SQL Server PDW&#41;](../sqlpdw/user-sessions-sql-server-pdw.md)-->.|  
|將資料載入至 SQL Server PDW|將資料載入至您的應用裝置。 <!-- MISSING LINKS See [Load &#40;SQL Server PDW&#41;](../sqlpdw/load-sql-server-pdw.md).-->|  
|建立嚴重損壞復原計畫|規劃如何將保護您的資料不受硬體故障或資料會覆寫。 建立計劃使用定期備份及還原計劃，如果發生資料損毀或遺失。 <!-- MISSING LINKS See [Create a Disaster Recovery Plan &#40;SQL Server PDW&#41;](../sqlpdw/create-a-disaster-recovery-plan-sql-server-pdw.md).-->|  
|監視設備|使用系統檢視表、 記錄和系統管理員主控台來監視設備狀態、 健全狀況和效能。 請更正或報告任何問題。 請參閱[監視設備健全狀況狀態&#40;Analytics Platform System&#41;](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md)。|  
