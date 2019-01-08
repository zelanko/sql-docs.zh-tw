---
title: 讓可用性群組離線 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], take offline
ms.assetid: 50f5aad8-0dff-45ef-8350-f9596d3db898
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 28d8279226469b8d7a39c5cf6ec802a393337087
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53371370"
---
# <a name="take-an-availability-group-offline-sql-server"></a>讓可用性群組離線 (SQL Server)
  本主題描述如何使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 和更新版本中的 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] ，將 AlwaysOn 可用性群組從 ONLINE 狀態變成 OFFLINE 狀態。 同步認可資料庫不會有資料遺失，因為如果有任何未同步處理的同步認可複本，OFFLINE 作業就會引發錯誤並且讓可用性群組維持 ONLINE 狀態。 讓可用性群組保持上線可保護未同步處理的同步認可資料庫，避免可能的資料遺失。 在可用性群組離線之後，其資料庫就無法供用戶端使用，而且您無法讓可用性群組恢復上線。 因此，只有在從某一個 WSFC 叢集將可用性群組資源移轉至另一個叢集時，才讓可用性群組離現。  
  
 跨叢集移轉 [!INCLUDE[ssHADR](../includes/sshadr-md.md)]期間，如果任何應用程式直接連接到可用性群組的主要複本，則必須讓可用性群組離線。 [!INCLUDE[ssHADR](../includes/sshadr-md.md)] 的跨叢集移轉支援以最短的可用性群組停機時間進行作業系統升級。 典型的案例是使用 [!INCLUDE[ssHADR](../includes/sshadr-md.md)] 的跨叢集移轉將作業系統升級為 [!INCLUDE[win8](../includes/win8-md.md)] 或 [!INCLUDE[win8srv](../includes/win8srv-md.md)]。 如需詳細資訊，請參閱[針對作業系統升級進行 AlwaysOn 可用性群組的跨叢集移轉](https://msdn.microsoft.com/library/jj873730.aspx)。  
  

  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
> [!CAUTION]  
>  OFFLINE 選項只可用於跨叢集移轉可用性群組資源。  
  
###  <a name="Prerequisites"></a> 必要條件  
  
-   您輸入 OFFLINE 命令所在的伺服器執行個體必須執行 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] 或更新版本 (Enterprise Edition 或更新版本)。  
  
-   可用性群組目前必須在線上。  
  
###  <a name="Recommendations"></a> 建議  
 在您讓可用性群組離線之前，請先刪除可用性群組接聽程式。 如需詳細資訊，請參閱 [移除可用性群組接聽程式 &#40;SQL Server&#41;](availability-groups/windows/remove-an-availability-group-listener-sql-server.md)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 需要可用性群組的 ALTER AVAILABILITY GROUP 權限、CONTROL AVAILABILITY GROUP 權限、ALTER ANY AVAILABILITY GROUP 權限或 CONTROL SERVER 權限。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **讓可用性群組離線**  
  
1.  連接到主控可用性群組之可用性複本的伺服器執行個體。 此複本可以是主要複本或次要複本。  
  
2.  使用 [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) 陳述式，如下所示：  
  
     ALTER AVAILABILITY GROUP *group_name* OFFLINE  
  
     其中 <群組名稱> 是可用性群組的名稱。  
  
### <a name="example"></a>範例  
 下列範例會讓 `AccountsAG` 可用性群組離線。  
  
```  
ALTER AVAILABILITY GROUP AccountsAG OFFLINE;  
```  
  
##  <a name="FollowUp"></a> 後續操作：可用性群組離線之後  
  
-   **OFFLINE 作業記錄：** 起始 OFFLINE 作業所在的 WSFC 節點識別會儲存在 WSFC 叢集記錄檔和 SQL ERRORLOG 中。  
  
-   **如果您未在群組離線之前刪除可用性群組接聽程式：** 如果您將可用性群組移轉至另一個 WSFC 叢集，請刪除的 VNN 和 VIP 的接聽程式。 您可以使用容錯移轉叢集管理主控台、 [Remove-ClusterResource](https://technet.microsoft.com/library/ee461015\(WS.10\).aspx) PowerShell Cmdlet 或 [cluster.exe](https://technet.microsoft.com/library/ee461015\(WS.10\).aspx)刪除它們。 請注意，cluster.exe 在 Windows 8 中已被取代。  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [移除可用性群組接聽程式 &#40;SQL Server&#41;](availability-groups/windows/remove-an-availability-group-listener-sql-server.md)  
  
-   [變更伺服器執行個體的 HADR 叢集內容 &#40;SQL Server&#41;](availability-groups/windows/change-the-hadr-cluster-context-of-server-instance-sql-server.md)  
  
##  <a name="RelatedContent"></a> 相關內容  
  
-   [SQL Server 2012 技術文件](https://msdn.microsoft.com/library/bb418445\(SQL.10\).aspx)  
  
-   [SQL Server AlwaysOn 團隊部落格：官方 SQL Server AlwaysOn 團隊部落格](https://blogs.msdn.com/b/sqlalwayson/)  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組&#40;SQL Server&#41;](availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
