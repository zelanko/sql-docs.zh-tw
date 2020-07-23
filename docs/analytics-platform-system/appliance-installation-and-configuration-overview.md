---
title: 設備安裝和設定
description: 引導分析平臺系統（AP）裝置管理人員完成設定並開始使用新設備的初始步驟。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 49ed0f26f20d081f4f9b307e6be90a3f5bd8c372
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942200"
---
# <a name="appliance-installation-and-configuration-for-analytics-platform-system"></a>分析平臺系統的設備安裝和設定
引導分析平臺系統（AP）裝置管理人員完成設定並開始使用新設備的初始步驟。  
  
<!-- MISSING LINKS ## <a name="BeforeYouBegin"></a>Before You Begin  
Before you begin to install, configure, and use your new appliance, we recommend reviewing information about the appliance components. Review the following to familiarize yourself with the appliance:  
  
-   Review [Understanding the Appliance Nodes and Hardware (SQL Server PDW)](assetId:///f60f419f-d1e1-403d-8cf9-07e7ef6d6627) to be sure you understand the components included in your new appliance.  
  
-   Review [Connecting to SQL Server PDW (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808) to understand how and when appliance administrators will connect to each appliance node.  
-->

## <a name="1-install-the-hardware"></a><a name="InstallHardware"></a>1. 安裝硬體  
您的新設備將會在您的資料中心上傳遞至 dock 的託盤上。  
  
> [!IMPORTANT]  
> 在某些情況下，您的 IHV 會在您的資料中心內解除包裝、機架，並為您連接設備。 若是如此，則不需要這些指示，而且您可以跳至[3。設定以下的 [設備](#ConfigureAppliance)] 區段。  
  
如果您的 IHV 未執行硬體安裝，請使用下列步驟來安裝硬體。  
  
|工作|描述|  
|-|-|  
|確認檔|確認您已從獨立硬體廠商（IHV）收到所有必要的檔和資訊。 請參閱[從您的 IHV &#40;分析平臺系統&#41;取得的資訊](information-to-obtain-from-your-ihv.md)。|  
|安裝硬體|確認資料中心可以容納設備。 將設備元件移至資料中心。 機架網路交換器、Pdu 和纜線。 請參閱[&#40;分析平臺系統&#41;的硬體安裝](hardware-installation.md)。|  
  
## <a name="2-power-on-the-appliance"></a><a name="PowerOnAppliance"></a>2. 設備上的電源  
  
|工作|描述|  
|-|-|  
|設備電源|以必要順序開啟每個設備元件節點上的電源，並視需要等候以確認未發生任何錯誤。|  
  
## <a name="3-configure-the-appliance"></a><a name="ConfigureAppliance"></a>3. 設定設備  
  
|工作|描述|  
|-|-|  
|使用 [SQL Server PDW**Configuration Manager**設定設備|使用 [Configuration Manager] 設定設備上的裝置密碼、時區、網路和防火牆設定、安全性憑證，以及效能及其他設定。 請參閱[設備設定 &#40;分析平臺系統&#41;](appliance-configuration.md)。|  
  
> [!WARNING]  
> 只能使用 SQL Server PDW**Configuration Manager**來進行設定變更。 不支援透過**Configuration Manager**公開的變更。 例如，SQL Server PDW 設備只支援美國-英文的語言設定。  
  
## <a name="4-set-up-software-servicing"></a><a name="SoftwareServicing"></a>4. 設定軟體服務  
  
|工作|描述|  
|-|-|  
|套用 SQL Server PDW 更新|選擇性您可能需要套用一或多個 SQL Server PDW 更新，以將您的 SQL Server PDW 軟體更新為最新版本。 請參閱[將分析平臺系統修補程式 &#40;分析平臺系統&#41;](apply-analytics-platform-system-hotfixes.md)。|  
|設定 Windows Server Update Services|設定設備以接收來自 Windows Server Update Services 的更新，以支援軟體。 請參閱[下載並套用 Microsoft Updates &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md)。|  
  
## <a name="next-steps"></a><a name="NextSteps"></a>後續步驟  
完成上述所有步驟之後，您的設備就可供使用。 您或您的位置中的其他人員可以繼續執行下列工作。  
  
|工作|描述|  
|-|-|  
|安裝 SQL Server PDW 驅動程式並設定連線能力|使用 SQL Server Data Tools、sqlcmd、商業智慧軟體或其他工具，將本機電腦設定為連接到 SQL Server PDW。 <!-- MISSING LINKS See [Client Tools (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808).-->|  
|建立登入和伺服器角色，並指派許可權|規劃並建立登入和伺服器角色，讓使用者可以使用適當的許可權登入 SQL Server PDW。 <!-- MISSING LINKS See [PDW Permissions &#40;SQL Server PDW&#41;](../sqlpdw/pdw-permissions-sql-server-pdw.md).-->|  
|設定 Azure 資料管理閘道|閘道可讓 Azure 使用者藉由將 AP 資料公開為安全的 OData 摘要，來存取內部部署 AP 資料。 閘道已安裝在控制節點上。 請向 Microsoft 尋求設定的協助。|  
|監視查詢和設備使用者|使用管理主控台和其他資源來監視查詢和設備使用者。 請參閱[使用管理主控台 &#40;分析平臺系統來監視設備&#41;](monitor-the-appliance-by-using-the-admin-console.md)<!-- MISSING LINKS and [User Sessions &#40;SQL Server PDW&#41;](../sqlpdw/user-sessions-sql-server-pdw.md)-->.|  
|將資料載入至 SQL Server PDW|將資料載入至您的應用裝置。 <!-- MISSING LINKS See [Load &#40;SQL Server PDW&#41;](../sqlpdw/load-sql-server-pdw.md).-->|  
|建立嚴重損壞修復計畫|規劃如何保護您的資料不受硬體故障或資料覆寫。 在資料損毀或遺失時，使用定期備份和還原計劃來建立計畫。 <!-- MISSING LINKS See [Create a Disaster Recovery Plan &#40;SQL Server PDW&#41;](../sqlpdw/create-a-disaster-recovery-plan-sql-server-pdw.md).-->|  
|監視設備|使用系統檢視、記錄和管理主控台來監視設備狀態、健全狀況和效能。 更正或報告任何問題。 請參閱[監視設備健全狀況狀態 &#40;分析平臺系統&#41;](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md)。|  
