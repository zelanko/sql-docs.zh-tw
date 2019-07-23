---
title: 變更可用性群組內複本的工作階段逾時期限
description: 描述如何設定 Always On 可用性群組內複本的工作階段逾時期限。
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], session timeout
- session timeout [SQL Server]
ms.assetid: e23c6e06-1cd1-4d4a-9bc2-e3e06ab2933d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d0c75e9264187ed6a351c162276253ff58be45a0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67991315"
---
# <a name="change-the-session-timeout-period-for-a-replica-within-an-always-on-availability-group"></a>變更 Always On 可用性群組內複本的工作階段逾時期限
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中的 [!INCLUDE[tsql](../../../includes/tsql-md.md)]、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]或 PowerShell 來設定 AlwaysOn 可用性複本的工作階段逾時期限。 工作階段逾時期限是複本屬性，它會控制可用性複本將連接視為失敗之前等候連接複本發出 Ping 回應的秒數 (以秒為單位)。 根據預設，複本會等候 Ping 回應的時間為 10 秒。 這個複本屬性只適用於可用性群組之給定次要複本與主要複本之間的連接。 如需工作階段逾時期間的詳細資訊，請參閱 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
   
##  <a name="Prerequisites"></a> 必要條件  
  
-   您必須連接到裝載主要複本的伺服器執行個體。  
  
##  <a name="Recommendations"></a> 建議  
 我們建議您讓逾時期限保持在 10 秒或更久。 將這個值設定為小於 10 秒，可能會使負荷重的系統遺漏 PING 以及宣告假失敗。  
  
  
## <a name="Permissions"></a> 權限  
 需要可用性群組的 ALTER AVAILABILITY GROUP 權限、CONTROL AVAILABILITY GROUP 權限、ALTER ANY AVAILABILITY GROUP 權限或 CONTROL SERVER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **若要變更可用性複本的工作階段逾時期限**  
  
1.  在 [物件總管] 中，連接到裝載主要複本的伺服器執行個體，然後展開伺服器樹狀目錄。  
  
2.  依序展開 [Always On 高可用性]  節點和 [可用性群組]  節點。  
  
3.  按一下您想要設定其可用性複本的可用性群組。  
  
4.  以滑鼠右鍵按一下要設定的複本，然後按一下 **[屬性]** 。  
  
5.  在 **[可用性複本屬性]** 對話方塊中，使用 **[工作階段逾時 (秒)]** 欄位來變更此複本之工作階段逾時期限的秒數。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **若要變更可用性複本的工作階段逾時期限**  
  
1.  連接到裝載主要複本的伺服器執行個體。  
  
2.  使用 [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) 陳述式，如下所示：  
  
     ALTER AVAILABILITY GROUP *group_name*  
  
     MODIFY REPLICA ON '*instance_name*' WITH ( SESSION_TIMEOUT =*seconds* )  
  
     其中 *group_name* 是可用性群組的名稱、 *instance_name* 是裝載要修改之可用性複本的伺服器執行個體名稱，而 *seconds* 會指定複本將記錄套用至資料庫 (做為次要複本) 之前必須等候的最小秒數。 預設值為 0 秒，表示沒有套用延遲。  
  
     下列範例 (在 `AccountsAG` 可用性群組的主要複本上輸入) 會針對位於 `15` 伺服器執行個體上的複本，將工作階段逾時值變更為 `INSTANCE09` 秒。  
  
    ```  
    ALTER AVAILABILITY GROUP AccountsAG   
       MODIFY REPLICA ON 'INSTANCE09' WITH (SESSION_TIMEOUT = 15);  
    ```  
  
##  <a name="PowerShellProcedure"></a> 使用 PowerShell  
 **若要變更可用性複本的工作階段逾時期限**  
  
1.  變更目錄 (**cd**) 為裝載主要複本的伺服器執行個體。  
  
2.  使用 **Set-SqlAvailabilityReplica** Cmdlet 搭配 **SessionTimeout** 參數來變更指定可用性複本之工作階段逾時期限的秒數。  
  
     例如，下列命令會將工作階段逾時期限設定為 15 秒。  
  
    ```  
    Set-SqlAvailabilityReplica -SessionTimeout 15 `   
    -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
    > [!NOTE]  
    >  若要檢視 Cmdlet 的語法，請在 **PowerShell 環境中使用** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Cmdlet。 如需詳細資訊，請參閱 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)。  
  
 **若要設定和使用 SQL Server PowerShell 提供者**  
  
-   [SQL Server PowerShell 提供者](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
