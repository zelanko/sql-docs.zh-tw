---
title: 設定叢集仲裁 NodeWeight 設定 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: failover-clusters
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- quorum [SQL Server], AlwaysOn and WSFC quorum
ms.assetid: cb3fd9a6-39a2-4e9c-9157-619bf3db9951
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 75d81e8e19e2ee1cf4efe62da164caf0e337e5ab
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="configure-cluster-quorum-nodeweight-settings"></a>設定叢集仲裁 NodeWeight 設定
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題說明如何設定 Windows Server 容錯移轉叢集 (WSFC) 叢集中成員節點的 NodeWeight 設定。 在仲裁投票期間，使用 NodeWeight 設定來支援 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體的災害復原和多重子網路案例。  
  
-   **開始之前：**  [必要條件](#Prerequisites)、 [安全性](#Security)  
  
-   **使用下列工具檢視仲裁 NodeWeight 設定︰**[使用 Powershell](#PowerShellProcedure)、[使用 Cluster.exe](#CommandPromptProcedure)。  
  
-   [相關內容](#RelatedContent)  
  
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
  
##  <a name="PowerShellProcedure"></a> 使用 Powershell  
  
##### <a name="to-configure-nodeweight-settings"></a>若要設定 NodeWeight 設定  
  
1.  透過 **[以系統管理員身分執行]** 來啟動更高權限的 Windows PowerShell。  
  
2.  匯入 `FailoverClusters` 模組來啟用叢集指令程式。  
  
3.  使用 `Get-ClusterNode` 物件來設定叢集中每個節點的 `NodeWeight` 屬性。  
  
4.  以可讀格式輸出叢集節點屬性。  
  
### <a name="example-powershell"></a>範例 (Powershell)  
 下列範例會變更 NodeWeight 設定，以便移除 “AlwaysOnSrv1” 節點的仲裁投票，然後輸出叢集中所有節點的設定。  
  
```powershell  
Import-Module FailoverClusters  
  
$node = “Always OnSrv1”  
(Get-ClusterNode $node).NodeWeight = 0  
  
$cluster = (Get-ClusterNode $node).Cluster  
$nodes = Get-ClusterNode -Cluster $cluster  
  
$nodes | Format-Table -property NodeName, State, NodeWeight  
```  
  
##  <a name="CommandPromptProcedure"></a> 使用 Cluster.exe  
  
> [!NOTE]  
>  cluster.exe 公用程式在 [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] 版本中已過時。  在未來的開發中，請搭配容錯移轉叢集使用 PowerShell。  下一版的 Windows Server 將會移除 cluster.exe 公用程式。 如需詳細資訊，請參閱 [針對容錯移轉叢集將 Cluster.exe 命令對應到 Windows PowerShell 指令程式](http://technet.microsoft.com/library/ee619744\(WS.10\).aspx)。  
  
##### <a name="to-configure-nodeweight-settings"></a>若要設定 NodeWeight 設定  
  
1.  透過 **[以系統管理員身分執行]** 來啟動更高權限的命令提示字元。  
  
2.  使用 **cluster.exe** 設定 `NodeWeight` 值。  
  
### <a name="example-clusterexe"></a>範例 (Cluster.exe)  
 下列範例會變更 NodeWeight 值，以便在 “Cluster001” 叢集中移除 “AlwaysOnSrv1” 節點的仲裁投票。  
  
```ms-dos  
cluster.exe Cluster001 node Always OnSrv1 /prop NodeWeight=0  
```  
  
##  <a name="RelatedContent"></a> 相關內容  
  
-   [檢視容錯移轉叢集的事件和記錄檔](http://technet.microsoft.com/library/cc772342\(WS.10\).aspx)  
  
-   [Get-ClusterLog 容錯移轉叢集指令程式](http://technet.microsoft.com/library/ee461045.aspx)  
  
## <a name="see-also"></a>另請參閱  
 [WSFC 仲裁模式和投票組態 &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md)   
 [檢視叢集仲裁 NodeWeight 設定](../../../sql-server/failover-clusters/windows/view-cluster-quorum-nodeweight-settings.md)   
 [Windows PowerShell 中由工作焦點列出的容錯移轉叢集指令程式](http://technet.microsoft.com/library/ee619761\(WS.10\).aspx)  
  
  
