---
title: "檢視叢集仲裁 NodeWeight 設定 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- quorum [SQL Server], AlwaysOn and WSFC quorum
ms.assetid: b845e73a-bb01-4de2-aac2-8ac12abebc95
caps.latest.revision: 17
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1bd8e579c3d75e804a552622039053b6700a352a
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="view-cluster-quorum-nodeweight-settings"></a>檢視叢集仲裁 NodeWeight 設定
  本主題說明如何檢視 Windows Server 容錯移轉叢集 (WSFC) 叢集中每個成員節點的 NodeWeight 設定。 在仲裁投票期間，使用 NodeWeight 設定來支援 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體的災害復原和多重子網路案例。  
  
-   **Before you start:**  [Prerequisites](#Prerequisites), [Security](#Security)  
  
-   **To view quorum NodeWeight settings using:** [Using Transact-SQL](#TsqlProcedure), [Using Powershell](#PowerShellProcedure), [Using Cluster.exe](#CommandPromptProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件  
 只有 [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] 或更新版本才支援這項功能。  
  
> [!IMPORTANT]  
>  為了能夠使用 NodeWeight 設定，必須將以下 Hotfix 套用至 WSFC 叢集中的所有伺服器：  
>   
>  [KB2494036](http://support.microsoft.com/kb/2494036)：提供 Hotfix 讓您設定叢集節點，該節點在 [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] 和 [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)]  
  
> [!TIP]  
>  如果未安裝此 Hotfix，本主題的範例會針對 NodeWeight 傳回空的值或 NULL 值。  
  
###  <a name="Security"></a> 安全性  
 使用者必須是屬於 WSFC 叢集之每一個節點上本機 Administrators 群組成員的網域帳戶。  
  
##  <a name="TsqlProcedure"></a> 使用 TRANSACT-SQL  
  
##### <a name="to-view-nodeweight-settings"></a>若要檢視 NodeWeight 設定  
  
1.  連接到叢集中的任何 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體。  
  
2.  查詢 [sys].[dm_hadr_cluster_members] 檢視表。  
  
### <a name="example-transact-sql"></a>範例 (Transact-SQL)  
 下列範例會查詢系統檢視表，以便針對該執行個體叢集中的所有節點傳回值。  
  
```tsql  
SELECT  member_name, member_state_desc, number_of_quorum_votes  
 FROM   sys.dm_hadr_cluster_members;  
```  
  
##  <a name="PowerShellProcedure"></a> 使用 Powershell  
  
##### <a name="to-view-nodeweight-settings"></a>若要檢視 NodeWeight 設定  
  
1.  透過 **[以系統管理員身分執行]**來啟動更高權限的 Windows PowerShell。  
  
2.  匯入 `FailoverClusters` 模組來啟用叢集指令程式。  
  
3.  使用 `Get-ClusterNode` 物件來傳回叢集節點物件的集合。  
  
4.  以可讀格式輸出叢集節點屬性。  
  
### <a name="example-powershell"></a>範例 (Powershell)  
 下列範例會針對名為 “Cluster001” 的叢集輸出某些節點屬性。  
  
```powershell  
Import-Module FailoverClusters  
  
$cluster = "Cluster001"  
$nodes = Get-ClusterNode -Cluster $cluster  
  
$nodes | Format-Table -property NodeName, State, NodeWeight  
```  
  
##  <a name="CommandPromptProcedure"></a> 使用 Cluster.exe  
  
> [!NOTE]  
>  cluster.exe 公用程式在 [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] 版本中已過時。  在未來的開發中，請搭配容錯移轉叢集使用 PowerShell。  下一版的 Windows Server 將會移除 cluster.exe 公用程式。 如需詳細資訊，請參閱 [針對容錯移轉叢集將 Cluster.exe 命令對應到 Windows PowerShell 指令程式](http://technet.microsoft.com/library/ee619744\(WS.10\).aspx)。  
  
##### <a name="to-view-nodeweight-settings"></a>若要檢視 NodeWeight 設定  
  
1.  透過 **[以系統管理員身分執行]**來啟動更高權限的命令提示字元。  
  
2.  使用 **cluster.exe** 傳回節點狀態和 NodeWeight 值  
  
### <a name="example-clusterexe"></a>範例 (Cluster.exe)  
 下列範例會針對名為 “Cluster001” 的叢集輸出某些節點屬性。  
  
```ms-dos  
cluster.exe Cluster001 node /status /properties  
```  
  
## <a name="see-also"></a>另請參閱  
 [WSFC 仲裁模式和投票組態 &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md)   
 [設定叢集仲裁 NodeWeight 設定](../../../sql-server/failover-clusters/windows/configure-cluster-quorum-nodeweight-settings.md)   
 [sys.dm_hadr_cluster_members &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql.md)   
 [Windows PowerShell 中由工作焦點列出的容錯移轉叢集指令程式](http://technet.microsoft.com/library/ee619761\(WS.10\).aspx)  
  
  
