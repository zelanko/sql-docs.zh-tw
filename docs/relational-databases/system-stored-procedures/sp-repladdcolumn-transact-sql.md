---
title: "sp_repladdcolumn (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_repladdcolumn_TSQL
- sp_repladdcolumn
helpviewer_keywords: sp_repladdcolumn
ms.assetid: d6220f9f-c738-4f9c-bcf8-419994e86c81
caps.latest.revision: "37"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d638619d087d43b0820fdf21650a9b8db1f7cf63
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sprepladdcolumn-transact-sql"></a>sp_repladdcolumn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將資料行加入已發行的現有資料表發行項中。 它可讓您將新資料行加入發行這份資料表的所有發行者中，或只將資料行加入發行這份資料表的特定發行集。 這個預存程序執行於發行集資料庫的發行者端。  
  
> [!IMPORTANT]  
>  這個預存程序已被取代，支援它的目的是為了回溯相容性。 它應該只用於具有[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]發行者和[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]重新發行訂閱者。 這個程序不應該用於含有 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本中導入之資料類型的資料行。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_repladdcolumn [ @source_object = ] 'source_object', [ @column = ] 'column' ]  
    [ , [ @typetext = ] 'typetext' ]  
    [ , [ @publication_to_add = ] 'publication_to_add' ]  
    [ , [ @from_agent = ] from_agent ]  
    [ , [ @schema_change_script = ] 'schema_change_script' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>引數  
 [ @source_object =] '*source_object*'  
 這是包含要加入之新資料行的資料表發行項名稱。 *source_object*是**nvarchar (358**)，沒有預設值。  
  
 [ @column =] '*資料行*'  
 這是複寫要加入之資料表中的資料行名稱。 *資料行*是**sysname**，沒有預設值。  
  
 [ @typetext =] '*typetext*'  
 這是要加入之資料行的定義。 *typetext*是**nvarchar （3000)**，沒有預設值。 例如，如果要加入資料行，而且它是單一字元欄位時，不是 NULL，且預設值為**N**，order_filled 就是*資料行*參數，而的定義資料行， **char （1) NOT NULL CONSTRAINT constraint_name DEFAULT 'n'**會*typetext*參數值。  
  
 [ @publication_to_add =] '*publication_to_add*'  
 這是新資料行要加入其中的發行集名稱。 *publication_to_add*是**nvarchar （4000)**，預設值是**所有**。 如果**所有**，則所有發行集包含此資料表會受到影響。 如果*publication_to_add*指定，則此發行集已加入新的資料行。  
  
 [ @from_agent =] *from_agent*  
 預存程序是否由複寫代理程式執行。 *from_agent*是**int**，預設值是**0**，其中值為**1**複寫代理程式，並在正在執行此預存程序時，會使用每個其他情況下的預設值**0**應使用。  
  
 [ @schema_change_script =] '*schema_change_script*'  
 指定用來修改系統產生之自訂預存程序的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指令碼的名稱和路徑。 *schema_change_script*是**nvarchar （4000)**，預設值是 NULL。 複寫可讓使用者自訂的自訂預存程序，取代異動複寫所用的一個或多個預設程序。 *schema_change_script*執行後結構描述變更複寫的資料表發行項使用 sp_repladdcolumn 時，會進行，可用來執行下列其中一項：  
  
-   如果自動重新產生自訂的預存程序， *schema_change_script*可用來卸除這些自訂預存程序，並取代為使用者定義自訂預存程序可支援新的結構描述。  
  
-   如果無法自動重新產生自訂預存程序， *schema_change_script*可用來重新產生這些預存程序，或建立使用者定義的自訂預存程序。  
  
 [ @force_invalidate_snapshot =] *force_invalidate_snapshot*  
 啟用或停用使快照集失效的能力。 *force_invalidate_snapshot*是**元**，預設值是**1**。  
  
 **1**指定發行項的變更可能使快照集失效，如果這種情況下，值為和**1**提供將出現新的快照集的權限。  
  
 **0**指定發行項的變更不會使快照集失效。  
  
 [ @force_reinit_subscription =] *force_reinit_subscription*  
 啟用或停用重新初始化訂閱的能力。 *force_reinit_subscription*是**元**預設值是**0**。  
  
 **0**指定發行項的變更不會使訂閱重新初始化。  
  
 **1**指定發行項的變更可能使訂閱重新初始化，以及如果這種情況下，值為**1**提供發生訂閱重新初始化的權限。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="permissions"></a>Permissions  
 只有系統管理員 (sysadmin) 固定伺服器角色和 db_owner 固定資料庫角色的成員，才能夠執行 sp_repladdcolumn。  
  
## <a name="see-also"></a>請參閱＜  
 [SQL Server 複寫中已被取代的功能](../../relational-databases/replication/deprecated-features-in-sql-server-replication.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
