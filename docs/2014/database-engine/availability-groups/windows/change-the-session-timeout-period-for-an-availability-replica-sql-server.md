---
title: 變更可用性複本的工作階段逾時期限 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 1408d970093fde0e2efea9662b56b9f099d6b0b4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "72783024"
---
# <a name="change-the-session-timeout-period-for-an-availability-replica-sql-server"></a>變更可用性複本的工作階段逾時期限 (SQL Server)
  本主題描述如何使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中的 [!INCLUDE[tsql](../../../includes/tsql-md.md)]、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]或 PowerShell 來設定 AlwaysOn 可用性複本的工作階段逾時期限。 工作階段逾時期限是複本屬性，它會控制可用性複本將連接視為失敗之前等候連接複本發出 Ping 回應的秒數 (以秒為單位)。 根據預設，複本會等候 Ping 回應的時間為 10 秒。 這個複本屬性只適用於可用性群組之給定次要複本與主要複本之間的連接。 如需工作階段逾時期間的詳細資訊，請參閱 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
-   **開始之前：**  
  
     [先決條件](#Prerequisites)  
  
     [建議](#Recommendations)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目變更工作階段逾時期限：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 必要條件  
  
-   您必須連接到裝載主要複本的伺服器執行個體。  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建議  
 我們建議您讓逾時期限保持在 10 秒或更久。 將這個值設定為小於 10 秒，可能會使負荷重的系統遺漏 PING 以及宣告假失敗。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要可用性群組的 ALTER AVAILABILITY GROUP 權限、CONTROL AVAILABILITY GROUP 權限、ALTER ANY AVAILABILITY GROUP 權限或 CONTROL SERVER 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **若要變更可用性複本的工作階段逾時期限**  
  
1.  在 [物件總管] 中，連接到裝載主要複本的伺服器執行個體，然後展開伺服器樹狀目錄。  
  
2.  依序展開 **[AlwaysOn 高可用性]** 節點和 **[可用性群組]** 節點。  
  
3.  按一下您想要設定其可用性複本的可用性群組。  
  
4.  以滑鼠右鍵按一下要設定的複本，然後按一下 **[屬性]**。  
  
5.  在 **[可用性複本屬性]** 對話方塊中，使用 **[工作階段逾時 (秒)]** 欄位來變更此複本之工作階段逾時期限的秒數。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **若要變更可用性複本的工作階段逾時期限**  
  
1.  連接到裝載主要複本的伺服器執行個體。  
  
2.  使用 [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) 陳述式，如下所示：  
  
     ALTER AVAILABILITY GROUP *group_name*  
  
     MODIFY REPLICA ON '*instance_name*' WITH ( SESSION_TIMEOUT =*seconds* )  
  
     其中 *group_name* 是可用性群組的名稱、 *instance_name* 是裝載要修改之可用性複本的伺服器執行個體名稱，而 *seconds* 會指定複本將記錄套用至資料庫 (做為次要複本) 之前必須等候的最小秒數。 預設值為 0 秒，表示沒有套用延遲。  
  
     下列範例 (在 `AccountsAG` 可用性群組的主要複本上輸入) 會針對位於 `15` 伺服器執行個體上的複本，將工作階段逾時值變更為 `INSTANCE09` 秒。  
  
    ```  
    ALTER AVAILABILITY GROUP AccountsAG   
       MODIFY REPLICA ON 'INSTANCE09' WITH (SESSION_TIMEOUT = 15);  
    ```  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> 使用 PowerShell  

### <a name="to-change-the-session-timeout-period-for-an-availability-replica"></a>若要變更可用性複本的工作階段逾時期限
  
1.  變更目錄 (`cd`) 為裝載主要複本的伺服器執行個體。  
  
2.  使用 `Set-SqlAvailabilityReplica` 指令程式搭配 `SessionTimeout` 參數來變更指定可用性複本之工作階段逾時期限的秒數。  
  
     例如，下列命令會將工作階段逾時期限設定為 15 秒。  
  
    ```powershell
    Set-SqlAvailabilityReplica -SessionTimeout 15 -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
    > [!NOTE]  
    >  若要檢視指令程式的語法，請在 `Get-Help` PowerShell 環境中使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 指令程式。 如需詳細資訊，請參閱 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)。  
  
若要設定及使用 SQL Server PowerShell 提供者，請參閱[SQL Server PowerShell 提供者](../../../powershell/sql-server-powershell-provider.md)。
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組 &#40;SQL Server 的總覽&#41;](overview-of-always-on-availability-groups-sql-server.md)  
