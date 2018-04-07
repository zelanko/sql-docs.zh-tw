---
title: 工作負載管理工作
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/12/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.openlocfilehash: 0a9c3ffd4768d78a4063ad40f7903dfe00b647e5
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="workload-management-tasks"></a>工作負載管理工作

## <a name="view-login-members-of-each-resource-class"></a>檢視登入成員的每個資源類別
描述如何在 SQL Server PDW 中顯示登入每個資源類別伺服器角色的成員。 使用這個查詢，找出允許提交每個登入所要求資源的類別。  
  
資源類別的描述，請參閱[工作負載管理](workload-management.md)。  
  
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
  
如果登入不是這份清單中，其要求將會接收預設資源。 如果登入為一個以上的資源類別的成員，最大類別具有優先順序。  
  
資源配置會列在[工作負載管理](workload-management.md)主題。  
  
## <a name="change-the-system-resources-allocated-to-a-request"></a>變更配置給要求的系統資源
描述如何找出哪些資源類別下，執行 SQL Server PDW 要求以及如何變更該要求的系統資源。 變更資源的要求需要變更使用送出要求的登入的資源類別的成員資格[ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md)陳述式。  
  
### <a name="step-1-determine-the-resource-class-for-the-login-running-the-request"></a>步驟 1： 決定登入正在執行要求的資源類別。  
此查詢會顯示登入的資源類別伺服器角色成員資格的成員。 有三個資源類別， **mediumrc**， **largerc**，和**xlargerc**。  
  
> [!IMPORTANT]  
> 必須由登入，需要執行此查詢**CONTROL SERVER**權限。 如果所沒有的登入執行**CONTROL SERVER**權限，此查詢只會傳回目前登入的角色成員資格。  
  
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
  
如果沒有資源類別的伺服器角色的成員登入，產生的資料表將會是空白。 在此情況下，如果查詢會傳回名為 Ching 登入，然後當 Ching 提交要求，要求會接收預設的系統資源，其小於資源類別系統資源。 如果登入為一個以上的資源類別的成員，最大類別具有優先順序。  
  
如需每個資源類別的資源配置的清單，請參閱[工作負載管理](workload-management.md)主題。  
  
### <a name="step-2-run-the-request-under-a-login-with-different-resource-class-membership"></a>步驟 2： 執行登入要求不同的資源類別的成員資格  
有兩種方式，可能是較大或較小的系統資源以執行要求：  
  
-   這是較大或變小資源類別的成員執行不同的登入要求。  
  
-   將必要的登入加入至其中一個資源類別角色。 選擇此選項時多加注意。變更登入的資源類別，會變更系統資源層級的所有登入所提交的要求。  
  
假設 Ching largerc 伺服器角色的成員。 下列範例會示範如何將登入 Ching 加入 xlargerc 伺服器角色。  
  
```sql  
ALTER SERVER ROLE xlargerc ADD MEMBER Ching;  
```  
  
Ching 現在是 largerc 和 xlargerc 伺服器角色的成員。 當 Ching 提交要求時，要求將會接收 xlargerc 系統資源。  
  
下列範例回到 Ching mediumrc 伺服器角色。  若要這樣做，她必須移除 xlargerc，與 largerc 伺服器 」 角色，並加入至 mediumrc 伺服器角色。  
  
```sql  
-- Move login Ching back to using medium system resources for requests.  
ALTER SERVER ROLE xlargerc DROP MEMBER Ching;  
ALTER SERVER ROLE largerc DROP MEMBER Ching;  
ALTER SERVER ROLE mediumrc ADD MEMBER Ching;  
```  
  
Ching 現在是 mediumrc 伺服器角色的成員。  下列範例會變更 Ching 有其要求的預設系統資源。  
  
```sql  
-- Move login Ching to use the default system resources for requests.  
ALTER SERVER ROLE mediumrc DROP MEMBER Ching;  
```  
  
如需有關如何變更資源類別角色成員資格的詳細資訊，請參閱[ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md)。  

## <a name="change-a-login-to-the-default-system-resources-for-its-requests"></a>變更預設的系統資源，其要求的登入
描述如何變更指派給預設少量的 SQL Server PDW 登入的系統資源配置。 這會影響 SQL Server PDW 將指派給登入所提交要求的系統資源。  
  
資源類別的描述，請參閱[工作負載管理](workload-management.md)  
  
當登入不是任何資源類別的伺服器角色的成員時，登入所提交的要求將會接收預設數量的系統資源。  
  
假設 Matt 目前是所有的資源類別伺服器角色的成員，而且想要還原成具有預設資源會收到其要求的登入。  下列範例將卸除所有的三個資源類別伺服器角色中的其成員資格指派給 Matt 的要求的預設資源。  
  
```sql  
--Give the requests submitted by Matt the default system resources   
--by dropping Matt from all resource class server roles.  
ALTER SERVER ROLE XLargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE LargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE MediumRC DROP MEMBER Matt;  
```  
  
## <a name="display-the-number-of-concurrency-slots-needed-for-a-waiting-request"></a>顯示並行插槽數目所需等候要求
描述如何找出並行位置所需的等候 SQL Server PDW 上執行的要求數目。  
  
如需詳細資訊，請參閱[工作負載管理](workload-management.md)。  
  
要求無法等候太久沒有正在執行。 其中一種方式來疑難排解此問題是查看並行位置需要要求數目。  下列範例示範等待中的每個要求所需的並行存取位置的數目。  
  
```sql  
--Display the number of concurrency slots required   
--for each request that is waiting to run.  
SELECT request_id, concurrency_slots_used AS [Slots Needed], resource_class AS [Resource Class]  
FROM sys.dm_pdw_resource_waits;  
```  
  
  
## <a name="see-also"></a>另請參閱  
[工作負載管理](workload-management.md)  
  
