---
title: 工作負載管理工作
description: Analytics Platform System 中的工作負載管理工作。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 88d95eb0a2e0805930cb5f01f5af05b8fc6b3f2e
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "74399408"
---
# <a name="workload-management-tasks-in-analytics-platform-system"></a>Analytics Platform System 中的工作負載管理工作
Analytics Platform System 中的工作負載管理工作。

## <a name="view-login-members-of-each-resource-class"></a>查看每個資源類別的登入成員
描述如何在 SQL Server PDW 中顯示每個資源類別伺服器角色的登入成員。 您可以使用此查詢來找出每個登入所提交之要求所允許的資源類別。  
  
如需資源類別的描述，請參閱 [工作負載管理](workload-management.md)。  
  
此查詢會顯示每個資源類別的成員資格清單。 有三個資源類別： mediumrc、largerc 和 xlargerc。  
  
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
  
如果登入不在此清單中，其要求將會收到預設資源。 如果登入是一個以上資源類別的成員，則最大的類別具有優先順序。  
  
資源配置會列在 [ [工作負載管理](workload-management.md)] 中。  
  
## <a name="change-the-system-resources-allocated-to-a-request"></a>變更配置給要求的系統資源
說明如何找出 SQL Server PDW 要求執行所在的資源類別，以及如何變更該要求的系統資源。 變更要求的資源需要使用 [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md) 語句變更登入提交要求的資源類別成員資格。  
  
### <a name="step-1-determine-the-resource-class-for-the-login-running-the-request"></a>步驟1：判斷執行要求之登入的資源類別。  
此查詢會顯示屬於資源類別伺服器角色成員資格成員的登入。 有三個資源類別： **mediumrc**、 **largerc**和 **xlargerc**。  
  
> [!IMPORTANT]  
> 此查詢必須由具有 **CONTROL SERVER** 許可權的登入執行。 如果沒有 **CONTROL SERVER** 許可權的登入執行，此查詢只會傳回目前登入的角色成員資格。  
  
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
  
如果沒有資源類別伺服器角色成員的登入，則產生的資料表將會是空的。 在此情況下，如果查詢傳回名為正航的登入，則當正航提交要求時，要求將會收到小於資源類別系統資源的預設系統資源。 如果登入是一個以上資源類別的成員，則最大的類別具有優先順序。  
  
如需每個資源類別的資源配置清單，請參閱 [工作負載管理](workload-management.md)。  
  
### <a name="step-2-run-the-request-under-a-login-with-different-resource-class-membership"></a>步驟2：在具有不同資源類別成員資格的登入下執行要求  
有兩種方式可以使用較大或較小的系統資源來執行要求：  
  
-   在屬於較大或較小資源類別成員的不同登入下執行要求。  
  
-   將必要的登入新增至其中一個資源類別角色。 請謹慎選擇此選項;變更登入的資源類別將會變更登入所提交之所有要求的系統資源層級。  
  
假設正航是 largerc 伺服器角色的成員。 下列範例示範如何將登入正航新增至 xlargerc 伺服器角色。  
  
```sql  
ALTER SERVER ROLE xlargerc ADD MEMBER Ching;  
```  
  
正航現在是 largerc 和 xlargerc 伺服器角色的成員。 正航提交要求時，要求將會收到 xlargerc 系統資源。  
  
下列範例會將正航移回 mediumrc 伺服器角色。  若要變更為新的角色，必須從 xlargerc、largerc 伺服器角色中移除登入，並將其新增至 mediumrc 伺服器角色。  
  
```sql  
-- Move login Ching back to using medium system resources for requests.  
ALTER SERVER ROLE xlargerc DROP MEMBER Ching;  
ALTER SERVER ROLE largerc DROP MEMBER Ching;  
ALTER SERVER ROLE mediumrc ADD MEMBER Ching;  
```  
  
正航現在是 mediumrc 伺服器角色的成員。  下列範例會將正航變更為具有要求的預設系統資源。  
  
```sql  
-- Move login Ching to use the default system resources for requests.  
ALTER SERVER ROLE mediumrc DROP MEMBER Ching;  
```  
  
如需變更資源類別角色成員資格的詳細資訊，請參閱 [ALTER SERVER role](../t-sql/statements/alter-server-role-transact-sql.md)。  

## <a name="change-a-login-to-the-default-system-resources-for-its-requests"></a>將登入變更為其要求的預設系統資源
說明如何將指派給 SQL Server PDW 登入的系統資源配置變更為預設數量。 
  
如需資源類別的描述，請參閱 [工作負載管理](workload-management.md)  
  
當登入不是任何資源類別伺服器角色的成員時，登入所提交的要求將會收到預設的系統資源量。  
  
假設登入 Matt 目前是所有資源類別伺服器角色的成員，而且想要還原回讓要求只接收預設資源。  下列範例會藉由卸載所有三個資源類別伺服器角色的成員資格，將預設資源指派給 Matt 的要求。  
  
```sql  
--Give the requests submitted by Matt the default system resources   
--by dropping Matt from all resource class server roles.  
ALTER SERVER ROLE XLargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE LargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE MediumRC DROP MEMBER Matt;  
```  
  
## <a name="display-the-number-of-concurrency-slots-needed-for-a-waiting-request"></a>顯示等候要求所需的平行存取插槽數目
描述如何找出等候在 SQL Server PDW 上執行的要求所需的平行存取插槽數目。  
  
如需詳細資訊，請參閱 [工作負載管理](workload-management.md)。  
  
要求可能等候太久而未執行。 疑難排解要求的其中一種方式，就是查看要求所需的平行存取插槽數目。  下列範例顯示每個等待要求所需的平行存取插槽數目。  
  
```sql  
--Display the number of concurrency slots required   
--for each request that is waiting to run.  
SELECT request_id, concurrency_slots_used AS [Slots Needed], resource_class AS [Resource Class]  
FROM sys.dm_pdw_resource_waits;  
```  
  
  
## <a name="see-also"></a>另請參閱  
[工作負載管理](workload-management.md)  
  
