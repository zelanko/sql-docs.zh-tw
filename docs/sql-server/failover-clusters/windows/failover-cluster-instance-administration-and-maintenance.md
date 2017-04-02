---
title: "容錯移轉叢集執行個體管理及維護 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "使用者帳戶 [SQL Server], 容錯移轉叢集"
  - "叢集 [SQL Server], 維護"
  - "節點 [容錯移轉叢集]"
  - "容錯移轉叢集 [SQL Server], 維護"
  - "加入節點"
  - "虛擬伺服器 [SQL Server], 移除節點"
  - "SQL Server 的叢集執行個體"
  - "節點 [容錯移轉叢集], 移除"
  - "節點 [容錯移轉叢集], 加入"
  - "服務帳戶 [SQL Server]"
  - "移除節點"
  - "虛擬伺服器 [SQL Server], 加入節點"
ms.assetid: 2d5c63e9-8061-45c3-94db-8dd3100b8a91
caps.latest.revision: 35
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 35
---
# 容錯移轉叢集執行個體管理及維護
  從現有 AlwaysOn 容錯移轉叢集執行個體 (FCI) 中加入或移除節點這類的維護工作是使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式來完成。 其他管理工作 (例如變更 IP 位址資源、從特定 FCI 案例復原) 則是使用容錯移轉叢集管理員嵌入式管理單元 (Windows Server 容錯移轉叢集 (WSFC) 服務的嵌入式管理單元) 來完成。  
  
## 維護容錯移轉叢集執行個體  
 安裝 FCI 之後，您可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式變更或修復該叢集。 例如，您可以將額外的節點新增到 FCI、執行 FCI 做為獨立的執行個體，或從 FCI 組態中移除節點。  
  
### 將節點加入現有的容錯移轉叢集執行個體  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式提供維護現有 FCI 的選項。 如果選擇這個選項，則可以在要加入 FCI 的電腦上執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式，將其他的節點加入 FCI。 如需詳細資訊，請參閱[建立新的 SQL Server 容錯移轉叢集 &#40;Setup&#41;](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md) 和[在 SQL Server 容錯移轉叢集中加入或移除節點 &#40;Setup&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)。  
  
### 從現有的容錯移轉叢集執行個體移除節點  
 您可以在要從 FCI 移除的電腦上執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式，以從 FCI 移除節點。 FCI 內的每個節點都視為與 FCI 上其他節點無相依性的對等，而您可以將任何節點移除。 損毀的節點即使無法使用也可移除，而且移除程序將不會從無法使用的節點中解除安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 二進位編碼檔案。 已移除的節點可以隨時再加入 FCI。 如需詳細資訊，請參閱[在 SQL Server 容錯移轉叢集中加入或移除節點 &#40;Setup&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)。  
  
### 變更服務帳戶  
 當 FCI 節點關閉或離線時，您不可以變更任何 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務帳戶的密碼。 如果您變更了帳戶密碼，就必須在所有的節點都恢復連線工作時，使用「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 組態管理員」重新設定密碼。  
  
 如果 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的服務帳戶並不是叢集中的系統管理員，就無法刪除叢集中任何節點的管理共用。 叢集中的管理共用必須可供使用， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 才能運作。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務帳戶與 WSFC 服務帳戶請不要使用相同的帳戶。 如果變更 WSFC 服務帳戶的密碼， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝將會失敗。  
  
 在 [!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)]上，服務 SID 用於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務帳戶。 如需詳細資訊，請參閱[設定 Windows 服務帳戶與權限](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。  
  
## 管理容錯移轉叢集執行個體  
  
|工作描述|主題連結|  
|----------------------|----------------|  
|描述如何加入 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資源的相依性。|[加入 SQL Server 資源的相依性](../../../sql-server/failover-clusters/windows/add-dependencies-to-a-sql-server-resource.md)|  
|Kerberos 是一種網路驗證通訊協定，可為用戶端/伺服器應用程式提供強大的驗證功能。 Kerberos 可做為交互操作的基礎，並且協助提升整個企業的網路驗證安全性。 您可以搭配使用 Kerberos 驗證與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 獨立執行個體或AlwaysOn FCI。|[註冊 Kerberos 連接的服務主體名稱](../../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)。|  
|提供描述如何啟用 Kerberos 驗證之內容的連結||  
|描述用以從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集失敗中復原的程序。|[從容錯移轉叢集執行個體失敗的狀況復原](../../../sql-server/failover-clusters/windows/recover-from-failover-cluster-instance-failure.md)|  
|描述用於變更 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體之 IP 位址資源的程序。|[變更容錯移轉叢集執行個體的 IP 位址](../../../sql-server/failover-clusters/windows/change-the-ip-address-of-a-failover-cluster-instance.md)|  
  
## 另請參閱  
 [設定 HealthCheckTimeout 屬性設定](../../../sql-server/failover-clusters/windows/configure-healthchecktimeout-property-settings.md)   
 [設定 FailureConditionLeve 屬性設定](../../../sql-server/failover-clusters/windows/configure-failureconditionlevel-property-settings.md)   
 [檢視及閱讀容錯移轉叢集執行個體診斷記錄檔](../../../sql-server/failover-clusters/windows/view-and-read-failover-cluster-instance-diagnostics-log.md)  
  
  