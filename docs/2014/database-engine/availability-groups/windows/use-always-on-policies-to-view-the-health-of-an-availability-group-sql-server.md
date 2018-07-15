---
title: 使用 AlwaysOn 原則檢視可用性群組 (SQL Server) 的健康情況 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 6f1bcbc3-1220-4071-8e53-4b957f5d3089
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4189c70c8e4cf9e3d2fce378dbbb039ae2c0c601
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37297138"
---
# <a name="use-alwayson-policies-to-view-the-health-of-an-availability-group-sql-server"></a>使用 AlwaysOn 原則檢視可用性群組的健全狀況 (SQL Server)
  此主題描述如何使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 中的 AlwaysOn 原則或 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]中的 PowerShell，判斷 AlwaysOn 可用性群組的作業健全狀況。 如需 AlwaysOn 原則式管理資訊，請參閱[AlwaysOn 可用性群組 (SQL Server) 操作問題適用的 AlwaysOn 原則](always-on-policies-for-operational-issues-always-on-availability.md)。  
  
> [!IMPORTANT]  
>  對於 AlwaysOn 原則，類別目錄名稱會做為識別碼。 變更 AlwaysOn 類別目錄的名稱會破壞其健全狀況評估功能。 因此，永遠不應修改 AlwaysOn 類別目錄的名稱。  
  

  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 需要 CONNECT、VIEW SERVER STATE 和 VIEW ANY DEFINITION 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 AlwaysOn 儀表板  
 **若要開啟 AlwaysOn 儀表板**  
  
1.  在 [物件總管] 中，連接到裝載其中一個可用性複本的伺服器執行個體。 若要檢視可用性群組中所有可用性複本的相關資訊，請用於裝載主要複本的伺服器執行個體。  
  
2.  按一下伺服器名稱展開伺服器樹狀目錄。  
  
3.  展開 **[AlwaysOn 高可用性]** 節點。  
  
     以滑鼠右鍵按一下 [可用性群組] 節點，或展開此節點，然後以滑鼠右鍵按一下特定的可用性群組。  
  
4.  選取 **[顯示儀表板]** 命令。  
  
 如需如何使用 AlwaysOn 儀表板的相關資訊，請參閱[使用 AlwaysOn 儀表板 &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)。  
  
##  <a name="PowerShellProcedure"></a> 使用 PowerShell  
 **使用 AlwaysOn 原則檢視可用性群組的健全狀況**  
  
1.  設為預設值 (`cd`) 裝載其中一個可用性複本的伺服器執行個體。 若要檢視可用性群組中所有可用性複本的相關資訊，請用於裝載主要複本的伺服器執行個體。  
  
2.  使用下列指令程式：  
  
     `Test-SqlAvailabilityGroup`  
     透過評估 SQL Server 原則式管理 (PBM) 原則，評估可用性群組的健全狀況。 您必須擁有 CONNECT、VIEW SERVER STATE 和 VIEW ANY DEFINITION 權限，才能執行這個 Cmdlet。  
  
     例如，下列命令會顯示伺服器執行個體 `Computer\Instance`上健全狀態為 "Error" 的所有可用性群組。  
  
    ```  
    Get-ChildItem SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups `   
    | Test-SqlAvailabilityGroup | Where-Object { $_.HealthState -eq "Error" }  
    ```  
  
     `Test-SqlAvailabilityReplica`  
     透過評估 SQL Server 原則式管理 (PBM) 原則，評估可用性複本的健全狀況。 您必須擁有 CONNECT、VIEW SERVER STATE 和 VIEW ANY DEFINITION 權限，才能執行這個 Cmdlet。  
  
     例如，下列命令會評估可用性群組 `MyReplica` 中名為 `MyAg` 之可用性複本的健全狀況並且輸出簡短摘要。  
  
    ```  
    Test-SqlAvailabilityReplica `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
     `Test-SqlDatabaseReplicaState`  
     透過評估 SQL Server 原則式管理 (PBM) 原則，評估所有聯結可用性複本之可用性資料庫的健全狀況。  
  
     例如，下列命令會評估可用性群組 `MyAg` 中所有可用性資料庫的健全狀況並且輸出每個資料庫的簡短摘要。  
  
    ```  
    Get-ChildItem SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\DatabaseReplicaStates `   
     | Test-SqlDatabaseReplicaState  
    ```  
  
     這些指令程式接受下列選項：  
  
    |選項|描述|  
    |------------|-----------------|  
    |`AllowUserPolicies`|執行 AlwaysOn 原則類別目錄中的使用者原則。|  
    |`InputObject`|表示可用性群組、可用性複本或可用性資料庫狀態的物件集合 (依據使用的指令程式而定)。 指令程式會計算指定之物件的健全狀況。|  
    |`NoRefresh`|設定此參數時，此 cmdlet 不會手動重新整理所指定的物件`-Path`或`-InputObject`參數。|  
    |`Path`|可用性群組、一個或多個可用性複本，或可用性資料庫之資料庫複本叢集狀態的路徑 (依據使用的指令程式而定)。 這是選擇性參數。 如果未指定，此參數的值預設為目前的工作位置。|  
    |`ShowPolicyDetails`|顯示此 Cmdlet 執行之各項原則評估的結果。 Cmdlet 針對每項原則評估輸出一個物件，此物件的欄位描述評估結果 (原則通過或失敗、原則名稱和類別目錄等等)。|  
  
     例如，下列 `Test-SqlAvailabilityGroup` 命令會指定 `-ShowPolicyDetails` 參數，針對在可用性群組 `MyAg` 上執行的每個原則式管理 (PBM) 原則，顯示此指令程式執行的每個原則評估結果。  
  
    ```  
    Test-SqlAvailabilityGroup `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\AgName `  
    -ShowPolicyDetails  
  
    ```  
  
    > [!NOTE]  
    >  若要檢視 cmdlet 的語法，請使用`Get-Help`指令程式在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]PowerShell 環境。 如需詳細資訊，請參閱 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)。  
  
 **若要設定和使用 SQL Server PowerShell 提供者**  
  
-   [SQL Server PowerShell 提供者](../../../powershell/sql-server-powershell-provider.md)  
  
-   [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)  
  
##  <a name="RelatedContent"></a> 相關內容  
 **SQL Server AlwaysOn 團隊部落格： 監視 AlwaysOn 健全狀況，使用 PowerShell:**  
  
-   [第 1 部：基本指令程式概觀](http://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/monitoring-alwayson-health-with-powershell-part-1.aspx)  
  
-   [第 2 部：進階指令程式使用](http://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/monitoring-alwayson-health-with-powershell-part-2.aspx)  
  
-   [第 3 部：簡單監控應用程式](http://blogs.msdn.com/b/sqlalwayson/archive/2012/02/15/monitoring-alwayson-health-with-powershell-part-3.aspx)  
  
-   [第 4 部：與 SQL Server Agent 整合](http://blogs.msdn.com/b/sqlalwayson/archive/2012/02/15/the-always-on-health-model-part-4.aspx)  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組概觀&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [可用性群組的管理 &#40;SQL Server&#41;](administration-of-an-availability-group-sql-server.md)   
 [監視可用性群組 &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)   
 [與 AlwaysOn 可用性群組 (SQL Server) 的操作問題適用的 AlwaysOn 原則](always-on-policies-for-operational-issues-always-on-availability.md) 
  
  
