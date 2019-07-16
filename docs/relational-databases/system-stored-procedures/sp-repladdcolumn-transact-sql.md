---
title: sp_repladdcolumn & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_repladdcolumn_TSQL
- sp_repladdcolumn
helpviewer_keywords:
- sp_repladdcolumn
ms.assetid: d6220f9f-c738-4f9c-bcf8-419994e86c81
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1b01a48e15c06f021b41b3bded35a0cd2739313c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006913"
---
# <a name="sprepladdcolumn-transact-sql"></a>sp_repladdcolumn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將資料行加入已發行的現有資料表發行項中。 它可讓您將新資料行加入發行這份資料表的所有發行者中，或只將資料行加入發行這份資料表的特定發行集。 這個預存程序執行於發行集資料庫的發行者端。  
  
> [!IMPORTANT]
>  這個預存程序已被取代，支援它的目的是為了回溯相容性。 它應該只搭配[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]發行者和[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]重新發行訂閱者。 這個程序不應該用於含有 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本中導入之資料類型的資料行。  
  
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
 這是複寫要加入之資料表中的資料行名稱。 *資料行*已**sysname**，沒有預設值。  
  
 [ @typetext =] '*typetext*'  
 這是要加入之資料行的定義。 *typetext*已**nvarchar(3000)** ，沒有預設值。 例如，如果資料行加入 order_filled，而且它是單一字元欄位時，不是 NULL，且具有預設值是**N**，order_filled 就是*資料行*參數，而的定義資料行**char(1) NOT NULL CONSTRAINT constraint_name DEFAULT 'n'** 會是*typetext*參數值。  
  
 [ @publication_to_add =] '*publication_to_add*'  
 這是新資料行要加入其中的發行集名稱。 *publication_to_add*已**nvarchar(4000)** ，預設值是**所有**。 如果**所有**，則所有的發行集包含此資料表會受到影響。 如果*publication_to_add*指定，則只有這個發行集會加入新的資料行。  
  
 [ @from_agent =] *from_agent*  
 預存程序是否由複寫代理程式執行。 *from_agent*已**int**，預設值是**0**的值**1**複寫代理程式，然後在執行這個預存程序時，會使用每個其他情況下的預設值**0**應該使用。  
  
 [ @schema_change_script =] '*schema_change_script&lt*'  
 指定用來修改系統產生之自訂預存程序的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指令碼的名稱和路徑。 *schema_change_script&lt*已**nvarchar(4000)** ，預設值是 NULL。 複寫可讓使用者自訂的自訂預存程序，取代異動複寫所用的一個或多個預設程序。 *schema_change_script&lt*執行後結構描述變更複寫的資料表發行項使用 sp_repladdcolumn 時，會進行，可用來執行下列其中一項：  
  
-   如果自動重新產生自訂的預存程序， *schema_change_script&lt*可用來卸除這些自訂預存程序和它們取代成使用者自訂預存程序來支援新的結構描述。  
  
-   如果未自動重新產生自訂預存程序， *schema_change_script&lt*可用來重新產生這些預存程序，或建立使用者定義的自訂預存程序。  
  
 [ @force_invalidate_snapshot =] *force_invalidate_snapshot*  
 啟用或停用使快照集失效的能力。 *force_invalidate_snapshot*已**位元**，預設值是**1**。  
  
 **1**指定發行項的變更可能使快照集失效，如果這種情況下，值為**1**提供將出現新的快照集的權限。  
  
 **0**指定發行項的變更不會使快照集失效。  
  
 [ @force_reinit_subscription =] *force_reinit_subscription*  
 啟用或停用重新初始化訂閱的能力。 *force_reinit_subscription*已**位元**預設值是**0**。  
  
 **0**指定發行項的變更不會使訂閱重新初始化。  
  
 **1**指定發行項的變更可能使訂閱重新初始化時，如果這種情況下，值為**1**提供發生之訂閱重新初始化的權限。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="permissions"></a>Permissions  
 只有系統管理員 (sysadmin) 固定伺服器角色和 db_owner 固定資料庫角色的成員，才能夠執行 sp_repladdcolumn。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 複寫中已被取代的功能](../../relational-databases/replication/deprecated-features-in-sql-server-replication.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
