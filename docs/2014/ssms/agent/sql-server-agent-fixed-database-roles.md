---
title: SQL Server Agent 固定資料庫角色 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dcb939b8eb04fafce163a395b05eb0e272977283
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63245987"
---
# <a name="sql-server-agent-fixed-database-roles"></a>SQL Server Agent 固定資料庫角色
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 具有下列 **msdb** 資料庫固定資料庫角色，讓管理員在存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式時具有更細微的控制權。 以下列出這些角色 (存取權限由少至多排列)：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 當使用者不是這些角色的其中一個成員，而以 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，他們不會在物件總管中看見 [SQL Server Agent] 節點。 使用者必須是這些固定資料庫角色的其中一個成員，或是**系統管理員 (sysadmin)** 固定伺服器角色，才能使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent。  
  
## <a name="permissions-of-sql-server-agent-fixed-database-roles"></a>SQL Server Agent 固定資料庫角色的權限  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 資料庫角色權限是同心而互相關聯的 -- 較多權限的角色繼承較少權限的角色在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 物件上的權限 (包括警示、操作員、作業、排程和 Proxy)。 例如，如果擁有最少權限的 **SQLAgentUserRole** 成員，被授與存取 proxy_A 的權限，而 **SQLAgentReaderRole** 和 **SQLAgentOperatorRole** 兩者的成員自動就會擁有存取此 Proxy 的權限，即使沒有明確授與他們 proxy_A 的存取權限。 如此可能會有安全性的隱含意義，將會在下列章節對於每個角色討論。  
  
### <a name="sqlagentuserrole-permissions"></a>SQLAgentUserRole 權限  
 **SQLAgentUserRole** 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 定資料庫角色中具備最少權限的角色。 它只對操作員、本機作業和作業排程擁有權限。 **SQLAgentUserRole** 的成員只對他們所擁有的本機作業和作業排程擁有權限。 他們無法使用多伺服器作業 (主要和目標伺服器作業)，也無法變更作業擁有權來取得他們尚未擁有之作業的存取權。 **SQLAgentUserRole** 成員只能在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的 [作業步驟屬性] 對話方塊中檢視可用 Proxy 的清單。 **SQLAgentUserRole** 的成員在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 物件總管中只能看見 [作業] 節點。  
  
> [!IMPORTANT]  
>  在授與「[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式」資料庫角色 Proxy 存取權之前，需考慮安全性隱含意義。 **SQLAgentReaderRole** 和 **SQLAgentOperatorRole** 自動為 **SQLAgentUserRole** 的成員。 這表示 **SQLAgentReaderRole** 和 **SQLAgentOperatorRole** 的成員可以存取所有授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQLAgentUserRole **的** Agent Proxy，也可以使用這些 Proxy。  
  
 下表摘要出 **SQLAgentUserRole** 對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 物件所擁有的權限。  
  
|動作|操作員|本機作業<br /><br /> (僅擁有的作業)|作業排程<br /><br /> (僅擁有的排程)|Proxy|  
|------------|---------------|----------------------------------------|------------------------------------------------|-------------|  
|建立/修改/刪除|否|是 <sup>1</sup>|是|否|  
|檢視清單 (列舉)|是 <sup>2</sup>|是|是|是 <sup>3</sup>|  
|啟用/停用|否|是|是|不適用|  
|檢視屬性|否|是|是|否|  
|執行/停止/啟動|不適用|是|不適用|不適用|  
|檢視作業記錄|不適用|是|不適用|不適用|  
|刪除作業記錄|不適用|否 <sup>4</sup>|不適用|不適用|  
|附加/卸離|不適用|不適用|是|不適用|  
  
 <sup>1</sup>無法變更作業擁有權。  
  
 <sup>2</sup>可以取得可用操作員的清單，以用於**sp_notify_operator**並**作業屬性**的 Management Studio 對話方塊。  
  
 <sup>3</sup>僅適用於 proxy 的清單**作業步驟屬性**的 Management Studio 對話方塊。  
  
 <sup>4</sup>隸屬**SQLAgentUserRole**必須明確授與 EXECUTE 權限**sp_purge_jobhistory**刪除他們擁有之作業的作業記錄。 他們無法刪除任何其他作業的作業記錄。  
  
### <a name="sqlagentreaderrole-permissions"></a>SQLAgentReaderRole 權限  
 **SQLAgentReaderRole** 包括所有 **SQLAgentUserRole** 的權限，並擁有檢視可用的多伺服器作業清單、其屬性與記錄的權限。 此角色的成員也可以檢視所有可用作業的清單，和作業排程及其屬性，而非只有他們擁有的作業和作業排程。 **SQLAgentReaderRole** 成員無法變更作業擁有權來取得他們尚未擁有之作業的存取權。 **SQLAgentReaderRole** 的成員在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 物件總管中只能看見 [作業] 節點。  
  
> [!IMPORTANT]  
>  在授與「[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式」資料庫角色 Proxy 存取權之前，需考慮安全性隱含意義。 **SQLAgentReaderRole** 的成員自動為 **SQLAgentUserRole** 的成員。 這表示 **SQLAgentReaderRole** 的成員可以存取所有授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQLAgentUserRole **的** Agent Proxy，也可以使用這些 Proxy。  
  
 下表摘要出 **SQLAgentReaderRole** 對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 物件所擁有的權限。  
  
|動作|操作員|本機作業|多伺服器作業|作業排程|Proxy|  
|------------|---------------|----------------|----------------------|-------------------|-------------|  
|建立/修改/刪除|否|[是] <sup>1</sup> （僅擁有的作業）|否|是 (僅擁有的排程)|否|  
|檢視清單 (列舉)|是 <sup>2</sup>|是|是|是|是 <sup>3</sup>|  
|啟用/停用|否|是 (僅擁有的作業)|否|是 (僅擁有的排程)|不適用|  
|檢視屬性|否|是|是|是|否|  
|編輯屬性|否|是 (僅擁有的作業)|否|是 (僅擁有的排程)|否|  
|執行/停止/啟動|不適用|是 (僅擁有的作業)|否|不適用|不適用|  
|檢視作業記錄|不適用|是|是|不適用|不適用|  
|刪除作業記錄|不適用|否 <sup>4</sup>|否|不適用|不適用|  
|附加/卸離|不適用|不適用|不適用|是 (僅擁有的排程)|不適用|  
  
 <sup>1</sup>無法變更作業擁有權。  
  
 <sup>2</sup>可以取得可用操作員的清單，以用於**sp_notify_operator**並**作業屬性**的 Management Studio 對話方塊。  
  
 <sup>3</sup>僅適用於 proxy 的清單**作業步驟屬性**的 Management Studio 對話方塊。  
  
 <sup>4</sup>隸屬**SQLAgentReaderRole**必須明確授與 EXECUTE 權限**sp_purge_jobhistory**刪除他們擁有之作業的作業記錄。 他們無法刪除任何其他作業的作業記錄。  
  
### <a name="sqlagentoperatorrole-permissions"></a>SQLAgentOperatorRole 權限  
 **SQLAgentOperatorRole** 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 固定資料庫角色中具備最多權限的角色。 它包括 **SQLAgentUserRole** 和 **SQLAgentReaderRole**的所有權限。 此角色的成員也可以檢視操作員和 Proxy 的屬性，並列舉出伺服器上可用的 Proxy 和警示。  
  
 **SQLAgentOperatorRole** 成員對本機作業和排程擁有額外的權限。 他們可以執行、停止或啟動所有本機作業，也可以刪除伺服器上任何本機作業的作業記錄。 還可以啟用或停用伺服器上所有本機作業和排程。 若要啟用或停用本機作業或排程，此角色的成員必須使用預存程序 **sp_update_job** 和 **sp_update_schedule**。 只有指定作業或排程名稱或識別碼的參數，以及 **@enabled** 參數可由 **SQLAgentOperatorRole**的成員。 如果他們指定任何其他參數，執行這些預存程序會失敗。 **SQLAgentOperatorRole** 成員無法變更作業擁有權來取得他們尚未擁有之作業的存取權。  
  
 **SQLAgentOperatorRole** 的成員可以看見 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 物件總管中的 [作業]、[警示]、[操作員] 和 [Proxy] 節點。 只有 [錯誤記錄檔] 節點對此角色的成員是不可見的。  
  
> [!IMPORTANT]  
>  在授與「[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式」資料庫角色 Proxy 存取權之前，需考慮安全性隱含意義。 **SQLAgentOperatorRole** 的成員自動為 **SQLAgentUserRole** 和 **SQLAgentReaderRole** 的成員。 這表示 **SQLAgentOperatorRole** 的成員可以存取所有授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQLAgentUserRole **或** SQLAgentReaderRole **的** Agent Proxy，也可以使用這些 Proxy。  
  
 下表摘要出 **SQLAgentOperatorRole** 對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 物件所擁有的權限。  
  
|動作|警示|操作員|本機作業|多伺服器作業|作業排程|Proxy|  
|------------|------------|---------------|----------------|----------------------|-------------------|-------------|  
|建立/修改/刪除|否|否|[是] <sup>2</sup> （僅擁有的作業）|否|是 (僅擁有的排程)|否|  
|檢視清單 (列舉)|是|是 <sup>1</sup>|是|是|是|是|  
|啟用/停用|否|否|是 <sup>3</sup>|否|是<sup>4</sup>|不適用|  
|檢視屬性|是|是|是|是|是|是|  
|編輯屬性|否|否|是 (僅擁有的作業)|否|是 (僅擁有的排程)|否|  
|執行/停止/啟動|不適用|不適用|是|否|不適用|不適用|  
|檢視作業記錄|不適用|不適用|是|是|不適用|不適用|  
|刪除作業記錄|不適用|不適用|是|否|不適用|不適用|  
|附加/卸離|不適用|不適用|不適用|不適用|是 (僅擁有的排程)|不適用|  
  
 <sup>1</sup>可以取得可用操作員的清單，以用於**sp_notify_operator**並**作業屬性**的 Management Studio 對話方塊。  
  
 <sup>2</sup>無法變更作業擁有權。  
  
 <sup>3</sup> **SQLAgentOperatorRole**成員可以啟用或停用本機作業，它們不是由使用預存程序擁有**sp_update_job**指定值和 **@enabled**而**@job_id** (或**@job_name**) 參數。 如果此角色的成員為此預存程序指定任何其他參數，執行程序會失敗。  
  
 <sup>4</sup> **SQLAgentOperatorRole**成員可以啟用或停用的排程，它們不是由使用預存程序擁有**sp_update_schedule**指定值和**@enabled** 並**@schedule_id** (或**@name**) 參數。 如果此角色的成員為此預存程序指定任何其他參數，執行程序會失敗。  
  
## <a name="assigning-users-multiple-roles"></a>指派多個角色給使用者  
 **系統管理員 (sysadmin)** 固定伺服器角色的成員，可存取所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的功能。 如果使用者不是 **系統管理員 (sysadmin)** 角色的成員，但是是多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 固定資料庫角色的成員，請記住這些角色是同心權限模型。 因為較多權限的角色永遠包含較少權限的角色的所有權限，因此使用者若為多個角色的成員，會自動擁有較多權限的角色成員所關聯的權限。  
  
## <a name="see-also"></a>另請參閱  
 [實作 SQL Server Agent 安全性](implement-sql-server-agent-security.md)   
 [sp_update_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql)   
 [sp_update_schedule &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-update-schedule-transact-sql)   
 [sp_notify_operator &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-notify-operator-transact-sql)   
 [sp_purge_jobhistory &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql)  
  
  
