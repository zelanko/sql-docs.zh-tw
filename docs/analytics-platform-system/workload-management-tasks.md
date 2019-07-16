---
title: 工作負載管理工作-Analytics Platform System |Microsoft Docs
description: Analytics Platform System 中的工作負載管理工作。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: ea6b3785914781e73a8570c1282741f7c4b56298
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959750"
---
# <a name="workload-management-tasks-in-analytics-platform-system"></a>Analytics Platform System 中的工作負載管理工作
Analytics Platform System 中的工作負載管理工作。

## <a name="view-login-members-of-each-resource-class"></a>檢視登入成員的每個資源類別
描述如何在 SQL Server PDW 中顯示登入每個資源類別伺服器角色的成員。 您可以使用這項查詢來找出允許每個登入所提出之要求的資源類別。  
  
如需資源類別的描述，請參閱[工作負載管理](workload-management.md)。  
  
此查詢會顯示每個資源類別的成員資格清單。 有三個資源類別、 mediumrc、 largerc 和 xlargerc。  
  
```sql  
SELECT l.name AS [member], r.name AS [server role]  
FROM sys.server_role_members AS rm  
JOIN sys.server_principals AS l  
  ON l.principal_id = rm.member_principal_id  
JOIN  
  sys.server_principals AS r  
  ON r.principal_id = rm.role_principal_id  
WHERE  
  ( l.[type] = 'S' OR l.[type] = 'U' OR l.[type] = 'G' )  
  AND r.[type] = 'R'  
  AND r.[name] in ('mediumrc', 'largerc', 'xlargerc');  
```  
  
如果登入不在此清單中，它的要求會收到的預設資源。 如果登入多個資源類別的成員，最大類別的優先順序較高。  
  
資源配置所述[工作負載管理](workload-management.md)。  
  
## <a name="change-the-system-resources-allocated-to-a-request"></a>變更配置給要求的系統資源
描述如何找出哪一個資源的 SQL Server PDW 要求在其下執行的類別以及如何變更該要求的系統資源。 變更資源要求需要變更提交要求時，所使用的登入的資源類別成員資格[ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md)陳述式。  
  
### <a name="step-1-determine-the-resource-class-for-the-login-running-the-request"></a>步驟 1：判斷執行要求的登入的資源類別。  
此查詢會顯示的資源類別伺服器角色成員資格的成員登入。 有三個資源類別： **mediumrc**， **largerc**，並**xlargerc**。  
  
> [!IMPORTANT]  
> 必須由登入，需要執行這項查詢**CONTROL SERVER**權限。 如果執行不含登入所**CONTROL SERVER**權限，此查詢只傳回目前的登入的角色成員資格。  
  
```sql  
SELECT l.name AS [member], r.name AS [server role]  
FROM sys.server_role_members AS rm  
JOIN sys.server_principals AS l  
  ON l.principal_id = rm.member_principal_id  
JOIN  
  sys.server_principals AS r  
  ON r.principal_id = rm.role_principal_id  
WHERE  
  l.[type] = 'S'   
  AND r.[type] = 'R'  
  AND r.[name] in ('mediumrc', 'largerc', 'xlargerc');  
GO  
```  
  
如果沒有登入的資源類別的伺服器角色的成員，產生的資料表會是空的。 在此情況下，如果查詢會傳回名為 Ching 登入，然後當 Ching 提交要求，要求將會收到預設系統資源，也就是小於資源類別系統資源。 如果登入多個資源類別的成員，最大類別的優先順序較高。  
  
如需每個資源類別的資源配置的清單，請參閱 <<c0> [ 工作負載管理](workload-management.md)。  
  
### <a name="step-2-run-the-request-under-a-login-with-different-resource-class-membership"></a>步驟 2：執行下登入要求具有不同的資源類別的成員資格  
有兩種方式可使用其中一個較大或較小的系統資源來執行要求：  
  
-   這是大型或小型資源類別的成員執行在不同的登入要求。  
  
-   新增必要的登入其中一種資源類別角色。 選擇此選項，小心;變更登入的資源類別會變更系統資源層級的登入所提交的所有要求。  
  
假設 Ching 為 largerc 伺服器角色的成員。 下列範例示範如何將登入 Ching 加入 xlargerc 伺服器角色。  
  
```sql  
ALTER SERVER ROLE xlargerc ADD MEMBER Ching;  
```  
  
Ching 現 largerc 和 xlargerc 伺服器角色的成員。 當 Ching 提交要求時，要求將會接收 xlargerc 系統資源。  
  
下列範例會 Ching 設為 mediumrc 伺服器角色。  若要變更至新的角色，必須從 xlargerc 和 largerc 的伺服器角色中移除並加入 mediumrc 伺服器角色的登入。  
  
```sql  
-- Move login Ching back to using medium system resources for requests.  
ALTER SERVER ROLE xlargerc DROP MEMBER Ching;  
ALTER SERVER ROLE largerc DROP MEMBER Ching;  
ALTER SERVER ROLE mediumrc ADD MEMBER Ching;  
```  
  
Ching 現在是 mediumrc 伺服器角色的成員。  下列範例會變更 Ching 擁有要求的預設系統資源。  
  
```sql  
-- Move login Ching to use the default system resources for requests.  
ALTER SERVER ROLE mediumrc DROP MEMBER Ching;  
```  
  
如需變更資源類別角色成員資格的詳細資訊，請參閱 < [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md)。  

## <a name="change-a-login-to-the-default-system-resources-for-its-requests"></a>變更預設的系統資源，其要求的登入
描述如何變更指派給預設少量的 SQL Server PDW 登入的系統資源配置。 
  
如需資源類別的描述，請參閱[工作負載管理](workload-management.md)  
  
當登入不是任何資源類別的伺服器角色的成員時，登入所提交的要求會收到預設的系統資源量。  
  
假設 Matt 是目前所有的資源類別伺服器角色的成員，而且想要還原成具有接收預設資源的要求的登入。  下列範例會卸除所有的三個資源類別伺服器角色中的其成員資格，將預設資源指派給 Matt 的要求。  
  
```sql  
--Give the requests submitted by Matt the default system resources   
--by dropping Matt from all resource class server roles.  
ALTER SERVER ROLE XLargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE LargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE MediumRC DROP MEMBER Matt;  
```  
  
## <a name="display-the-number-of-concurrency-slots-needed-for-a-waiting-request"></a>顯示並行存取插槽數目所需等候的要求
描述如何找出位置所需的要求，正在等候 SQL Server PDW 上執行的並行數目。  
  
如需詳細資訊，請參閱 <<c0> [ 工作負載管理](workload-management.md)。  
  
要求無法等候太久沒有正在執行。 其中一個疑難排解要求的方法是查看需要要求的並行存取插槽數目。  下列範例會顯示每個等候要求所需的並行存取插槽數目。  
  
```sql  
--Display the number of concurrency slots required   
--for each request that is waiting to run.  
SELECT request_id, concurrency_slots_used AS [Slots Needed], resource_class AS [Resource Class]  
FROM sys.dm_pdw_resource_waits;  
```  
  
  
## <a name="see-also"></a>另請參閱  
[工作負載管理](workload-management.md)  
  
