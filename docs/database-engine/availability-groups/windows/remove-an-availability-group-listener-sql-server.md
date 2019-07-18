---
title: 移除可用性群組接聽程式 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygroup.removeaglistener.default.f1
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
ms.assetid: fd9bba9a-d29f-4c23-8ecd-aaa049ed5f1b
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: 67648accafa07d3814e066f7202f9e8d273ffee7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66800995"
---
# <a name="remove-an-availability-group-listener-sql-server"></a>移除可用性群組接聽程式 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../../includes/tsql-md.md)]或 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]PowerShell，從 AlwaysOn 可用性群組中移除可用性群組接聽程式。  
  
  
##  <a name="Prerequisites"></a> 必要條件  
  
-   您必須連接到裝載主要複本的伺服器執行個體。  
  
##  <a name="Recommendations"></a> 建議  
 刪除可用性群組接聽程式之前，我們建議您先確定沒有應用程式正在使用接聽程式。  
 
  
##  <a name="Permissions"></a> 權限  
 需要可用性群組的 ALTER AVAILABILITY GROUP 權限、CONTROL AVAILABILITY GROUP 權限、ALTER ANY AVAILABILITY GROUP 權限或 CONTROL SERVER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **若要移除可用性群組接聽程式**  
  
1.  在 [物件總管] 中，連接到裝載主要複本的伺服器執行個體，然後按一下伺服器名稱以展開伺服器樹狀目錄。  
  
2.  依序展開 [Always On 高可用性] 節點和 [可用性群組] 節點。  
  
3.  展開可用性群組的節點，然後展開 **[可用性群組接聽程式]** 節點。  
  
4.  以滑鼠右鍵按一下要移除的接聽程式，然後選取 **[刪除]** 命令。  
  
5.  這樣就會開啟 **[從可用性群組移除接聽程式]** 對話方塊。 如需詳細資訊，請參閱本主題稍後的＜ [從可用性群組移除接聽程式](#AgListenerPropertiesDialog)＞。  
  
###  <a name="AgListenerPropertiesDialog"></a> 從可用性群組移除接聽程式 (對話方塊)  
 **名稱**  
 要移除的接聽程式名稱。  
  
 **結果**  
 顯示連結 ( **[成功]** 或 **[錯誤]**)，而且按一下即可取得詳細資訊。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **若要移除可用性群組接聽程式**  
  
1.  連接到裝載主要複本的伺服器執行個體。  
  
2.  使用 [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) 陳述式，如下所示：  
  
     ALTER AVAILABILITY GROUP *group_name* REMOVE LISTENER **'**_dns_name_**'**  
  
     *group_name* 是可用性群組的名稱， *dns_name* 是可用性群組接聽程式的 DNS 名稱。  
  
     下列範例會刪除 `AccountsAG` 可用性群組的接聽程式。 DNS 名稱是 AccountsAG_Listener。  
  
    ```  
    ALTER AVAILABILITY GROUP AccountsAG REMOVE LISTENER 'AccountsAG_Listener';  
    ```  
  
##  <a name="PowerShellProcedure"></a> 使用 PowerShell  
 **若要移除可用性群組接聽程式**  
  
1.  設定預設值 (**cd**) 為裝載主要複本的伺服器執行個體。  
  
2.  使用內建的 **Remove-Item** Cmdlet 移除接聽程式。 例如，下列命令會從名為 `MyListener` 的可用性群組中移除名為 `MyAg`的接聽程式。  
  
    ```  
    Remove-Item `   
    SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AGListeners\MyListener  
    ```  
  
    > [!NOTE]  
    >  若要檢視 Cmdlet 的語法，請在 **PowerShell 環境中使用** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Cmdlet。 如需詳細資訊，請參閱 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)。  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [建立或設定可用性群組接聽程式 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [檢視可用性群組接聽程式屬性 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-listener-properties-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [可用性群組接聽程式、用戶端連接及應用程式容錯移轉 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)  
  
  
