---
title: SQL Server Agent 固定資料庫角色
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- roles [SQL Server], SQL Server Agent
- SQL Server Agent, roles
- SQLAgentUserRole database role
- SQLAgentReaderRole database role
- multiple roles
- security [SQL Server Agent], fixed database roles
- fixed database roles [SQL Server]
- SQLAgentOperatorRole database role
ms.assetid: 719ce56b-d6b2-414a-88a8-f43b725ebc79
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5395642ed6df8f8e6c1fd01e0599ca50c36e4b3f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75242727"
---
# <a name="sql-server-agent-fixed-database-roles"></a>SQL Server Agent 固定資料庫角色
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 具有下列 **msdb** 資料庫固定資料庫角色，讓管理員在存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式時具有更細微的控制權。 以下列出這些角色 (存取權限由少至多排列)：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
當使用者不是這些角色的其中一個成員，而以 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，他們不會在物件總管中看見 [SQL Server Agent]  節點。 使用者必須是這些固定資料庫角色的其中一個成員，或是 **系統管理員 (sysadmin)** 固定伺服器角色，才能使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent。  
  
## <a name="permissions-of-sql-server-agent-fixed-database-roles"></a>SQL Server Agent 固定資料庫角色的權限  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 資料庫角色權限是同心而互相關聯的 -- 較多權限的角色繼承較少權限的角色在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 物件上的權限 (包括警示、操作員、作業、排程和 Proxy)。 例如，如果擁有最少權限的 **SQLAgentUserRole** 成員，被授與存取 proxy_A 的權限，而 **SQLAgentReaderRole** 和 **SQLAgentOperatorRole** 兩者的成員自動就會擁有存取此 Proxy 的權限，即使沒有明確授與他們 proxy_A 的存取權限。 如此可能會有安全性的隱含意義，將會在下列章節對於每個角色討論。  
  
### <a name="sqlagentuserrole-permissions"></a>SQLAgentUserRole 權限  
**SQLAgentUserRole** 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 定資料庫角色中具備最少權限的角色。 它只對操作員、本機作業和作業排程擁有權限。 **SQLAgentUserRole** 的成員只對他們所擁有的本機作業和作業排程擁有權限。 他們無法使用多伺服器作業 (主要和目標伺服器作業)，也無法變更作業擁有權來取得他們尚未擁有之作業的存取權。 **SQLAgentUserRole** 成員只能在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的 [作業步驟屬性]  對話方塊中檢視可用 Proxy 的清單。 **SQLAgentUserRole** 的成員在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 物件總管中只能看見 [作業]  節點。  
  
> [!IMPORTANT]  
> 在將 Proxy 存取權授與  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**Agentdatabaseroles** 的成員之前，需注意安全性考量。 **SQLAgentReaderRole** 和 **SQLAgentOperatorRole** 自動為 **SQLAgentUserRole**的成員。 這表示 **SQLAgentReaderRole** 和 **SQLAgentOperatorRole** 的成員可以存取所有授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQLAgentUserRole **的** Agent Proxy，也可以使用這些 Proxy。  
  
下表摘要出 **SQLAgentUserRole** 對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 物件所擁有的權限。  
  
|動作|操作員|本機作業<br /><br />(僅擁有的作業)|作業排程<br /><br />(僅擁有的排程)|Proxy|  
|----------|-------------|-----------------------------------|-------------------------------------------|-----------|  
|建立/修改/刪除|否|是<br /><br />無法變更作業擁有權。|是|否|  
|檢視清單 (列舉)|是<br /><br />可以取得可用操作員的清單，以便在 **sp_notify_operator** 和 Management Studio 的 [作業屬性]  對話方塊中使用。|是|是|是<br /><br />只在 Management Studio 的 [作業步驟屬性]  對話方塊中可用的 Proxy 清單。|  
|啟用/停用|否|是|是|不適用|  
|檢視屬性|否|是|是|否|  
|執行/停止/啟動|不適用|是|不適用|不適用|  
|檢視作業記錄|不適用|是|不適用|不適用|  
|刪除作業記錄|不適用|否<br /><br />**SQLAgentUserRole** 的成員必須明確被授與對 **sp_purge_jobhistory** 的 EXECUTE 權限，才能對他們擁有的作業刪除作業記錄。 他們無法刪除任何其他作業的作業記錄。|不適用|不適用|  
|附加/卸離|不適用|不適用|是|不適用|  
  
### <a name="sqlagentreaderrole-permissions"></a>SQLAgentReaderRole 權限  
**SQLAgentReaderRole** 包括所有 **SQLAgentUserRole** 的權限，並擁有檢視可用的多伺服器作業清單、其屬性與記錄的權限。 此角色的成員也可以檢視所有可用作業的清單，和作業排程及其屬性，而非只有他們擁有的作業和作業排程。 **SQLAgentReaderRole** 成員無法變更作業擁有權來取得他們尚未擁有之作業的存取權。 **SQLAgentReaderRole** 的成員在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 物件總管中只能看見 [作業]  節點。  
  
> [!IMPORTANT]  
> 在將 Proxy 存取權授與  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**Agentdatabaseroles** 的成員之前，需注意安全性考量。 **SQLAgentReaderRole** 的成員自動為 **SQLAgentUserRole**的成員。 這表示 **SQLAgentReaderRole** 的成員可以存取所有授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQLAgentUserRole **的** Agent Proxy，也可以使用這些 Proxy。  
  
下表摘要出 **SQLAgentReaderRole** 對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 物件所擁有的權限。  
  
|動作|操作員|本機作業|多伺服器作業|作業排程|Proxy|  
|----------|-------------|--------------|--------------------|-----------------|-----------|  
|建立/修改/刪除|否|是 (僅擁有的作業)<br /><br />無法變更作業擁有權。|否|是 (僅擁有的排程)|否|  
|檢視清單 (列舉)|是<br /><br />可以取得可用操作員的清單，以便在 **sp_notify_operator** 和 Management Studio 的 [作業屬性]  對話方塊中使用。|是|是|是|是<br /><br />只在 Management Studio 的 [作業步驟屬性]  對話方塊中可用的 Proxy 清單。|  
|啟用/停用|否|是 (僅擁有的作業)|否|是 (僅擁有的排程)|不適用|  
|檢視屬性|否|是|是|是|否|  
|編輯屬性|否|是 (僅擁有的作業)|否|是 (僅擁有的排程)|否|  
|執行/停止/啟動|不適用|是 (僅擁有的作業)|否|不適用|不適用|  
|檢視作業記錄|不適用|是|是|不適用|不適用|  
|刪除作業記錄|不適用|否<br /><br />**SQLAgentReaderRole** 的成員必須明確被授與對 **sp_purge_jobhistory** 的 EXECUTE 權限，才能對他們擁有的作業刪除作業記錄。 他們無法刪除任何其他作業的作業記錄。|否|不適用|不適用|  
|附加/卸離|不適用|不適用|不適用|是 (僅擁有的排程)|不適用|  
  
### <a name="sqlagentoperatorrole-permissions"></a>SQLAgentOperatorRole 權限  
**SQLAgentOperatorRole** 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 固定資料庫角色中具備最多權限的角色。 它包括 **SQLAgentUserRole** 和 **SQLAgentReaderRole**的所有權限。 此角色的成員也可以檢視操作員和 Proxy 的屬性，並列舉出伺服器上可用的 Proxy 和警示。  
  
**SQLAgentOperatorRole** 成員對本機作業和排程擁有額外的權限。 他們可以執行、停止或啟動所有本機作業，也可以刪除伺服器上任何本機作業的作業記錄。 還可以啟用或停用伺服器上所有本機作業和排程。 若要啟用或停用本機作業或排程，此角色的成員必須使用預存程序 **sp_update_job** 和 **sp_update_schedule**。 只有指定作業或排程名稱或識別碼的參數，以及 **\@enabled** 參數可由 **SQLAgentOperatorRole** 的成員指定。 如果他們指定任何其他參數，執行這些預存程序會失敗。 **SQLAgentOperatorRole** 成員無法變更作業擁有權來取得他們尚未擁有之作業的存取權。  
  
**SQLAgentOperatorRole** 的成員可以看見 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 物件總管中的 [作業]  、[警示]  、[操作員]  和 [Proxy]  節點。 只有 [錯誤記錄檔]  節點對此角色的成員是不可見的。  
  
> [!IMPORTANT]  
> 在將 Proxy 存取權授與  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**Agentdatabaseroles** 的成員之前，需注意安全性考量。 **SQLAgentOperatorRole** 的成員自動為 **SQLAgentUserRole** 和 **SQLAgentReaderRole**的成員。 這表示 **SQLAgentOperatorRole** 的成員可以存取所有授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQLAgentUserRole **或** SQLAgentReaderRole **的** Agent Proxy，也可以使用這些 Proxy。  
  
下表摘要出 **SQLAgentOperatorRole** 對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 物件所擁有的權限。  
  
|動作|警示|操作員|本機作業|多伺服器作業|作業排程|Proxy|  
|----------|----------|-------------|--------------|--------------------|-----------------|-----------|  
|建立/修改/刪除|否|否|是 (僅擁有的作業)<br /><br />無法變更作業擁有權。|否|是 (僅擁有的排程)|否|  
|檢視清單 (列舉)|是|是<br /><br />可以取得可用操作員的清單，以便在 **sp_notify_operator** 和 Management Studio 的 [作業屬性]  對話方塊中使用。|是|是|是|是|  
|啟用/停用|否|否|是<br /><br />**SQLAgentOperatorRole** 成員可以使用預存程序 **sp_update_job** 並指定 **\@enabled** 和 **\@job_id** (或 **\@job_name**) 參數的值，來啟用或停用非其擁有的本機作業。 如果此角色的成員為此預存程序指定任何其他參數，執行程序會失敗。|否|是<br /><br />**SQLAgentOperatorRole** 成員可以使用預存程序 **sp_update_schedule** 並指定 **\@enabled** 和 **\@schedule_id** (或 **\@name**) 參數的值，來啟用或停用非其擁有的排程。 如果此角色的成員為此預存程序指定任何其他參數，執行程序會失敗。|不適用|  
|檢視屬性|是|是|是|是|是|是|  
|編輯屬性|否|否|是 (僅擁有的作業)|否|是 (僅擁有的排程)|否|  
|執行/停止/啟動|不適用|不適用|是|否|不適用|不適用|  
|檢視作業記錄|不適用|不適用|是|是|不適用|不適用|  
|刪除作業記錄|不適用|不適用|是|否|不適用|不適用|  
|附加/卸離|不適用|不適用|不適用|不適用|是 (僅擁有的排程)|不適用|  
  
## <a name="assigning-users-multiple-roles"></a>指派多個角色給使用者  
**系統管理員 (sysadmin)** 固定伺服器角色的成員，可存取所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的功能。 如果使用者不是 **系統管理員 (sysadmin)** 角色的成員，但是是多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 固定資料庫角色的成員，請記住這些角色是同心權限模型。 因為較多權限的角色永遠包含較少權限的角色的所有權限，因此使用者若為多個角色的成員，會自動擁有較多權限的角色成員所關聯的權限。  
  
## <a name="see-also"></a>另請參閱  
[實作 SQL Server Agent 安全性](../../ssms/agent/implement-sql-server-agent-security.md)  
[sp_update_job (Transact-SQL)](https://msdn.microsoft.com/cbdfea38-9e42-47f3-8fc8-5978b82e2623)  
[sp_update_schedule (Transact-SQL)](https://msdn.microsoft.com/97b3119b-e43e-447a-bbfb-0b5499e2fefe)  
[sp_notify_operator (Transact-SQL)](https://msdn.microsoft.com/c440f5c9-9884-4196-b07c-55d87afb17c3)  
[sp_purge_jobhistory (Transact-SQL)](https://msdn.microsoft.com/237f9bad-636d-4262-9bfb-66c034a43e88)  
  
