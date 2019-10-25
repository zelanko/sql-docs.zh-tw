---
title: 設定 HealthCheckTimeout 屬性設定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 3bbeb979-e6fc-4184-ad6e-cca62108de74
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4106de497a43404cb44606259d53beb1ed8f5a58
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797448"
---
# <a name="configure-healthchecktimeout-property-settings"></a>設定 HealthCheckTimeout 屬性設定
  HealthCheckTimeout 設定是用來指定在報告 AlwaysOn 容錯移轉叢集之前，SQL Server 資源 DLL 應該等候[sp_server_diagnostics](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql)預存程式傳回信息的時間長度（以毫秒為單位）實例（FCI）為沒有回應。 針對逾時設定值所做的變更會立即生效，且不需要重新啟動 SQL Server 資源。  
  
-   **開始之前：** [限制事項](#Limits)、[安全性](#Security)  
  
-   **使用下列項目設定 HeathCheckTimeout 設定：** [PowerShell](#PowerShellProcedure)、[容錯移轉叢集管理員](#WSFC)、[Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Limits"></a> 限制事項  
 此屬性的預設值為 60,000 毫秒 (60 秒)。 最小值為 15,000 毫秒 (15 秒)。  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> Permissions  
 需要 ALTER SETTINGS 及 VIEW SERVER STATE 權限。  
  
##  <a name="PowerShellProcedure"></a> 使用 PowerShell  
  
### <a name="to-configure-healthchecktimeout-settings"></a>設定 HealthCheckTimeout 設定  
  
1.  透過 **[以系統管理員身分執行]** 來啟動更高權限的 Windows PowerShell。  
  
2.  匯入 `FailoverClusters` 模組來啟用叢集指令程式。  
  
3.  使用 `Get-ClusterResource` Cmdlet 來尋找 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資源，然後使用 `Set-ClusterParameter` Cmdlet 來設定容錯移轉叢集實例的**HealthCheckTimeout**屬性。  
  
> [!TIP]  
>  每次開啟新的 PowerShell 視窗時，都需要匯入 `FailoverClusters` 模組。  

 下列範例會將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資源 "`SQL Server (INST1)`" 上的 HealthCheckTimeout 設定變更為 60000 毫秒。  
  
```powershell  
Import-Module FailoverClusters  
  
$fci = "SQL Server (INST1)"  
Get-ClusterResource $fci | Set-ClusterParameter HealthCheckTimeout 60000  
```  
  
### <a name="related-content-powershell"></a>相關內容 (PowerShell)  
  
-   [Clustering and High-Availability](https://blogs.msdn.com/b/clustering/archive/2009/05/23/9636665.aspx) (叢集和高可用性 - 容錯移轉叢集和網路負載平衡團隊部落格)  
  
-   [在容錯移轉叢集上開始使用 Windows PowerShell](https://technet.microsoft.com/library/ee619762\(WS.10\).aspx)  
  
-   [叢集資源命令和對等的 Windows PowerShell 指令程式](https://msdn.microsoft.com/library/ee619744.aspx#BKMK_resource)  
  
##  <a name="WSFC"></a> 使用容錯移轉叢集管理員嵌入式管理單元  
 **設定 HealthCheckTimeout 設定**  
  
1.  開啟 [容錯移轉叢集管理員] 嵌入式管理單元。  
  
2.  展開 **[服務及應用程式]** 並選取 FCI。  
  
3.  以滑鼠右鍵按一下 [其他資源] 下方的 [SQL Server 資源]，並從滑鼠右鍵功能表中選取 [屬性]。 SQL Server 資源的 **[屬性]** 對話方塊隨即開啟。  
  
4.  選取 **[屬性]** 索引標籤，輸入需要的 **[HealthCheckTimeout]** 屬性值，然後按一下 **[確定]** 套用變更。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 使用 [ALTER SERVER CONFIGURATION](/sql/t-sql/statements/alter-server-configuration-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式可以指定 HealthCheckTimeOut 屬性值。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 下列範例會將 HealthCheckTimeout 選項設定為 15,000 毫秒 (15 秒)。  
  
```sql
ALTER SERVER CONFIGURATION   
SET FAILOVER CLUSTER PROPERTY HealthCheckTimeout = 15000;  
```  
  
## <a name="see-also"></a>請參閱  
 [容錯移轉叢集執行個體的容錯移轉原則](failover-policy-for-failover-cluster-instances.md)  
