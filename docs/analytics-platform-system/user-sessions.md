---
title: 使用者工作階段
description: 分析平臺系統的平行處理資料倉儲中的使用者會話。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: a0e5b338cc616be214ef39527551ee4a6ffd8f56
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "74399403"
---
# <a name="user-sessions-in-analytics-platform-system"></a>Analytics Platform System 中的使用者會話
具有適當許可權的登入可以管理 SQL Server PDW 設備上所有登入的會話，包括執行下列動作：  
  
-   查看設備上目前的會話，包括作用中和閒置會話。  
  
-   查看會話的使用中和最近的查詢。  
  
-   結束使用中的會話。  
  
您可以使用 [[使用管理主控台來監視設備](monitor-the-appliance-by-using-the-admin-console.md)] 或 [透過 SQL 命令的[系統檢視](tsql-system-views.md)] 來執行這些動作，如下所示。  
  
使用任一種方法來管理會話所需的許可權都相同，並在[授與管理登入、使用者和資料庫角色的許可權](grant-permissions.md#grant-permissions-to-manage-logins-users-and-database-roles)中說明。  
  
## <a name="manage-sessions-by-using-the-admin-console"></a>使用管理主控台管理會話  
  
### <a name="to-view-current-sessions-by-using-the-admin-console"></a>使用管理主控台來查看目前的會話  
  
1.  在頂端功能表上，按一下 [**會話**]。  
  
2.  產生的清單會顯示所有最近的會話。 若只要查看「作用中」或「閒置」會話，請按一下 [**狀態**] 欄標題，依狀態排序結果。  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-the-admin-console"></a>使用管理主控台來查看會話的作用中和最近查詢  
  
1.  在頂端功能表上，按一下 [**會話**]。  
  
2.  在結果清單中，按一下所需會話的會話識別碼。  
  
3.  [產生的查詢] 清單會顯示會話最近的查詢。 如需有關查看查詢詳細資料的資訊，請參閱監視使用中的[查詢](monitoring-active-queries.md)。  
  
### <a name="to-end-sessions-by-using-the-admin-console"></a>使用管理主控台來結束會話  
  
1.  在頂端功能表上，按一下 [**會話**]。  
  
2.  尋找要取消之會話的會話識別碼。  
  
3.  按一下 [會話識別碼] 左邊的紅色**X**來結束會話。 只有狀態為「作用中」或「閒置」的會話才會有紅色**X**;只有這些會話可以結束。  
  
## <a name="manage-sessions-by-using-system-views-and-sql-commands"></a>使用系統檢視和 SQL 命令管理會話  
  
### <a name="to-view-current-sessions-by-using-system-views"></a>使用系統檢視來查看目前的會話  
使用[dm_pdw_exec_sessions sys.databases](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)來產生目前會話的清單。  
  
這個範例會針對狀態為「作用中」或「閒置」的所有會話，傳回 session_id、login_name 和狀態。  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions WHERE status='Active' OR status='Idle';  
```  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-system-views"></a>若要使用系統檢視來查看會話的現用和最近查詢  
若要查看與會話相關聯的作用中和最近完成的查詢，請使用[dm_pdw_exec_sessions sys.databases](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)和[sys.databases dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md) views。 此查詢會傳回所有作用中或閒置會話的清單，以及與每個會話識別碼相關聯的任何作用中或最近的查詢。  
  
```sql  
SELECT es.session_id, es.login_name, es.status AS sessionStatus,   
er.request_id, er.status AS requestStatus, er.command   
FROM sys.dm_pdw_exec_sessions es   
LEFT OUTER JOIN sys.dm_pdw_exec_requests er   
ON (es.session_id=er.session_id)   
WHERE (es.status='Active' OR es.status='Idle') AND   
(er.status!= 'Completed' AND er.status!= 'Failed' AND er.status!= 'Cancelled');  
```  
  
### <a name="to-end-sessions-by-using-sql-commands"></a>使用 SQL 命令結束會話  
使用[KILL](../t-sql/language-elements/kill-transact-sql.md)命令來結束目前的會話。 您將需要終止進程的會話識別碼，您可以使用 [ [dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) ] 視圖來取得該程式。  
  
在此範例中，選取 [login_name]、[session_id] 和 [狀態值]，以根據登入名稱來尋找會話。  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions;  
```  
  
具有「作用中」或「閒置」狀態的會話可以使用 KILL 命令來結束。  
  
```sql  
KILL 'SID137';  
```  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
