---
title: "設定 HealthCheckTimeout 屬性設定 | Microsoft Docs"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3bbeb979-e6fc-4184-ad6e-cca62108de74
caps.latest.revision: 31
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: fe45e057f3e8a9a4cd105cad16ef773c2aed0928
ms.lasthandoff: 04/11/2017

---
# <a name="configure-healthchecktimeout-property-settings"></a>設定 HealthCheckTimeout 屬性設定
  HealthCheckTimeout 設定會用來指定將 AlwaysOn 容錯移轉叢集執行個體 (FCI) 回報為沒有回應之前，SQL Server 資源 DLL 應該等候 [sp_server_diagnostics](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) 預存程序傳回資訊的時間長度 (以毫秒為單位)。 針對逾時設定值所做的變更會立即生效，且不需要重新啟動 SQL Server 資源。  
  
-   **開始之前：**[限制事項](#Limits)、[安全性](#Security)  
  
-   **使用下列項目設定 HeathCheckTimeout 設定：**[PowerShell](#PowerShellProcedure)、[容錯移轉叢集管理員](#WSFC)、[Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Limits"></a> 限制事項  
 此屬性的預設值為 30,000 毫秒 (30 秒)。 最小值為 15,000 毫秒 (15 秒)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要 ALTER SETTINGS 及 VIEW SERVER STATE 權限。  
  
##  <a name="PowerShellProcedure"></a> 使用 PowerShell  
  
##### <a name="to-configure-healthchecktimeout-settings"></a>設定 HealthCheckTimeout 設定  
  
1.  透過 **[以系統管理員身分執行]**來啟動更高權限的 Windows PowerShell。  
  
2.  匯入 **FailoverClusters** 模組來啟用叢集指令程式。  
  
3.  使用 **Get-ClusterResource** Cmdlet 尋找 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資源，然後使用 **Set-ClusterParameter** Cmdlet 設定容錯移轉叢集執行個體的 **HealthCheckTimeout** 屬性。  
  
> [!TIP]  
>  每次開啟新的 PowerShell 視窗時，都需要匯入 **FailoverClusters** 模組。  
  
### <a name="example-powershell"></a>範例 (PowerShell)  
 下列範例會將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資源 "`SQL Server (INST1)`" 上的 HealthCheckTimeout 設定變更為 60000 毫秒。  
  
```powershell  
Import-Module FailoverClusters  
  
$fci = "SQL Server (INST1)"  
Get-ClusterResource $fci | Set-ClusterParameter HealthCheckTimeout 60000  
  
```  
  
### <a name="related-content-powershell"></a>相關內容 (PowerShell)  
  
-   [Clustering and High-Availability](http://blogs.msdn.com/b/clustering/archive/2009/05/23/9636665.aspx) (叢集和高可用性 - 容錯移轉叢集和網路負載平衡團隊部落格)  
  
-   [在容錯移轉叢集上開始使用 Windows PowerShell](http://technet.microsoft.com/library/ee619762\(WS.10\).aspx)  
  
-   [叢集資源命令和對等的 Windows PowerShell 指令程式](http://msdn.microsoft.com/library/ee619744.aspx#BKMK_resource)  
  
##  <a name="WSFC"></a> 使用容錯移轉叢集管理員嵌入式管理單元  
 **設定 HealthCheckTimeout 設定**  
  
1.  開啟 [容錯移轉叢集管理員] 嵌入式管理單元。  
  
2.  展開 **[服務及應用程式]** 並選取 FCI。  
  
3.  以滑鼠右鍵按一下 [其他資源] 下方的 [SQL Server 資源]，並從滑鼠右鍵功能表中選取 [屬性]。 SQL Server 資源的 **[屬性]** 對話方塊隨即開啟。  
  
4.  選取 **[屬性]** 索引標籤，輸入需要的 **[HealthCheckTimeout]** 屬性值，然後按一下 **[確定]** 套用變更。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 使用 [ALTER SERVER CONFIGURATION](../../../t-sql/statements/alter-server-configuration-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式可以指定 HealthCheckTimeOut 屬性值。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 下列範例會將 HealthCheckTimeout 選項設定為 15,000 毫秒 (15 秒)。  
  
```  
ALTER SERVER CONFIGURATION   
SET FAILOVER CLUSTER PROPERTY HealthCheckTimeout = 15000;  
```  
  
## <a name="see-also"></a>另請參閱  
 [容錯移轉叢集執行個體的容錯移轉原則](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)  
  
  

