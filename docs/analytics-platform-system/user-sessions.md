---
title: 使用者工作階段 (SQL Server PDW)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0425cef2-de4d-4f42-91c5-cb1cd4bb1265
caps.latest.revision: 15
ms.openlocfilehash: 4ed0fab1fae1fe2d1a5a3ebb961d6c4d4747764f
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="user-sessions"></a>使用者工作階段
具有適當的權限的登入可以管理 SQL Server PDW 應用裝置，包括在執行這些動作上的所有登入工作的階段：  
  
-   檢視目前的工作階段上的應用裝置，包括作用中和閒置工作階段。  
  
-   檢視工作階段的作用中和最近的查詢。  
  
-   結束使用中工作階段。  
  
可以使用執行這些動作[使用管理主控台來監視設備](monitor-the-appliance-by-using-the-admin-console.md)或[系統檢視表](tsql-system-views.md)透過 SQL 命令，如下所示。  
  
若要使用哪一種方法來管理工作階段所需的權限都一樣，和所述[管理登入、 使用者和資料庫角色授與權限](grant-permissions.md#grant-permissions-to-manage-logins-users-and-database-roles)。  
  
## <a name="manage-sessions-by-using-the-admin-console"></a>使用管理主控台來管理工作階段  
  
### <a name="to-view-current-sessions-by-using-the-admin-console"></a>若要使用管理主控台來檢視目前的工作階段  
  
1.  在上方功能表中，按一下 **工作階段**。  
  
2.  結果清單會顯示所有最近的工作階段。 若要檢視僅 'Active' 或 '閒置' 的工作階段，請按一下**狀態**資料行標頭，依狀態排序結果。  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-the-admin-console"></a>若要檢視作用中和最近的查詢工作階段，使用系統管理員主控台  
  
1.  在上方功能表中，按一下 **工作階段**。  
  
2.  在 [結果] 清單中，按一下所需的工作階段的工作階段識別碼。  
  
3.  產生的查詢清單會顯示最近的查詢工作階段。 如需檢視查詢的詳細資訊，請參閱[監視使用中查詢](monitoring-active-queries.md)。  
  
### <a name="to-end-sessions-by-using-the-admin-console"></a>若要結束工作階段使用系統管理員主控台  
  
1.  在上方功能表中，按一下 **工作階段**。  
  
2.  尋找要取消工作階段的工作階段識別碼。  
  
3.  按一下紅色**X**左邊的 結束工作階段的工作階段識別碼。 只有工作階段狀態為 'Active' 或 '閒置' 將會有紅色**X**; 僅可以結束這些工作階段。  
  
## <a name="manage-sessions-by-using-system-views-and-sql-commands"></a>使用系統檢視表和 SQL 命令來管理工作階段  
  
### <a name="to-view-current-sessions-by-using-system-views"></a>若要使用系統檢視表來檢視目前的工作階段  
使用[sys.dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)來產生一份目前的工作階段。  
  
這個範例會傳回所有工作階段狀態為 'Active' 或 '閒置' session_id、 login_name 和狀態。  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions WHERE status='Active' OR status='Idle';  
```  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-system-views"></a>若要使用系統檢視表檢視作用中和最近的查詢工作階段  
若要查看工作階段相關聯的作用中和最近完成的查詢，您使用[sys.dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)和[sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)檢視。 此查詢會傳回一份所有作用中或閒置工作階段，再加上與每個工作階段識別碼相關聯的任何作用中或新查詢  
  
```sql  
SELECT es.session_id, es.login_name, es.status AS sessionStatus,   
er.request_id, er.status AS requestStatus, er.command   
FROM sys.dm_pdw_exec_sessions es   
LEFT OUTER JOIN sys.dm_pdw_exec_requests er   
ON (es.session_id=er.session_id)   
WHERE (es.status='Active' OR es.status='Idle') AND   
(er.status!= 'Completed' AND er.status!= 'Failed' AND er.status!= 'Cancelled');  
```  
  
### <a name="to-end-sessions-by-using-sql-commands"></a>若要使用 SQL 命令來結束工作階段  
使用[KILL](../t-sql/language-elements/kill-transact-sql.md)命令來結束目前的工作階段。 您必須處理序結束，這可以使用取得的工作階段識別碼[sys.dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)檢視。  
  
在此範例中，選取 login_name、 session_id 和狀態的值，以尋找工作階段為基礎的登入名稱。  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions;  
```  
  
可以使用 KILL 命令結束工作階段的 'Active' 或 '閒置' 狀態。  
  
```sql  
KILL 'SID137';  
```  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
