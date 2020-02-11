---
title: sp_who （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_who_TSQL
- sp_who
dev_langs:
- TSQL
helpviewer_keywords:
- sp_who
ms.assetid: 132dfb08-fa79-422e-97d4-b2c4579c6ac5
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 5d758c7ca2d21183b9486030704c31b9d5f621d0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67950510"
---
# <a name="sp_who-transact-sql"></a>sp_who (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  提供實例[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]中目前使用者、會話和進程的相關資訊。 您可以篩選資訊，只傳回屬於特定使用者或屬於特定工作階段的非閒置處理序。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_who [ [ @loginame = ] 'login' | session ID | 'ACTIVE' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @loginame = ] 'login' | session ID | 'ACTIVE'`用來篩選結果集。  
  
 *login*是**sysname** ，可識別屬於特定登入的進程。  
  
 *會話識別碼*是屬於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實例的會話識別碼。 *會話識別碼*為**Smallint**。  
  
 [作用中]**會排除等待**使用者下一個命令的會話。  
  
 如果沒有提供任何值，程序會報告屬於執行個體的所有工作階段。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 **sp_who**會傳回包含下列資訊的結果集。  
  
|資料行|資料類型|描述|  
|------------|---------------|-----------------|  
|**spid**|**smallint**|工作階段識別碼。|  
|**ecid**|**smallint**|特定工作階段識別碼所關聯之給定執行緒的執行內容識別碼。<br /><br /> ECID = {0，1，2，3，.。。*n*}，其中0一律代表主要或父執行緒，{1，2，3，.。。*n*} 代表子執行緒。|  
|**狀態**|**Nchar （30）**|處理序狀態。 可能的值包括：<br /><br /> **休眠**。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在重設工作階段。<br /><br /> **正在**執行。 工作階段正在執行一或多個批次。 啟用 Multiple Active Result Set (MARS) 之後，工作階段就可以執行多個批次。 如需詳細資訊，請參閱[使用 Multiple Active Result Sets &#40;MARS&#41;](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)。<br /><br /> **背景**。 工作階段正在執行背景工作，例如死結偵測。<br /><br /> **復原**。 工作階段正在進行交易回復。<br /><br /> **暫**止。 工作階段正在等候工作者執行緒變成可用狀態。<br /><br /> 可**執行。** 在等候取得時間配量時，工作階段的工作位於排程器的可執行佇列中。<br /><br /> **spinloop**。 工作階段的工作正在等候單一執行緒存取鎖變成可用狀態。<br /><br /> 已**暫停**。 工作階段正在等候事件 (例如 I/O) 完成。|  
|**loginame**|**Nchar （128）**|特定處理序所關聯的登入名稱。|  
|**名稱**|**Nchar （128）**|每個處理序的主機或電腦名稱。|  
|**blk**|**char （5）**|封鎖處理序的工作階段識別碼 (如果有)。 否則，這個資料行就是零。<br /><br /> 當被遺棄的分散式交易封鎖了與指定工作階段識別碼相關的交易時，這個資料行會針對進行封鎖的被遺棄交易傳回 '-2'。|  
|**dbname**|**Nchar （128）**|處理序所用的資料庫。|  
|**cmd**|**Nchar （16）**|針對處理序來執行的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 命令 ([!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式、內部 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 處理序等等)。|  
|**request_id**|**int**|在特定工作階段中執行的要求識別碼。|  
  
 發生平行處理時，會針對特定的工作階段識別碼建立子執行緒。 主要執行緒會以 `spid = <xxx>` 和 `ecid =0` 的方式指出。 另一個子執行緒具有相同`spid = <xxx>`的，但**ecid** > 0。  
  
## <a name="remarks"></a>備註  
 進行封鎖的處理序 (可能擁有獨佔鎖定) 為持有另一處理序所需要之資源的處理序。  
  
 所有被遺棄的分散式交易都會有指派的工作階段識別碼值 '-2'。 被遺棄的分散式交易是不與任何工作階段識別碼相關聯的分散式交易。 如需詳細資訊，請參閱 [使用標示的異動以一致的方式復原相關資料庫 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)。  
  
 查詢 sys. dm_exec_sessions 的**is_user_process**資料行，以分隔系統進程與使用者進程。  
  
## <a name="permissions"></a>權限  
 需要有這部伺服器的 VIEW SERVER STATE 權限，才能在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上看到所有執行中的工作階段。 否則，使用者只會看到目前的工作階段。  
  
## <a name="examples"></a>範例  
  
### <a name="a-listing-all-current-processes"></a>A. 列出所有目前的處理序  
 下列範例使用不具參數的 `sp_who` 報告所有目前的使用者。  
  
```  
USE master;  
GO  
EXEC sp_who;  
GO  
```  
  
### <a name="b-listing-a-specific-users-process"></a>B. 列出特定使用者的處理序  
 下列範例會顯示如何依登入名稱來檢視有關單一目前使用者的資訊。  
  
```  
USE master;  
GO  
EXEC sp_who 'janetl';  
GO  
```  
  
### <a name="c-displaying-all-active-processes"></a>C. 顯示所有使用中的處理序  
  
```  
USE master;  
GO  
EXEC sp_who 'active';  
GO  
```  
  
### <a name="d-displaying-a-specific-process-identified-by-a-session-id"></a>D. 顯示工作階段識別碼所識別的特定處理序  
  
```  
USE master;  
GO  
EXEC sp_who '10' --specifies the process_id;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_lock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)   
 [sysprocesses &#40;Transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
