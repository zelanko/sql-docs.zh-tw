---
title: sp_repldropcolumn & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_repldropcolumn_TSQL
- sp_repldropcolumn
helpviewer_keywords:
- sp_repldropcolumn
ms.assetid: fdc1ec5f-f108-42b4-a2d8-f06a71913ab8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2c2a269abf3e7f465c71e09437c313196e1dcd30
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53205687"
---
# <a name="sprepldropcolumn-transact-sql"></a>sp_repldropcolumn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從已發行的現有資料表發行項中卸除資料行。 這個預存程序執行於發行集資料庫的發行者端。  
  
> [!IMPORTANT]
>  這個預存程序已被取代，支援它的目的，主要是為了與舊版相容。 它應該只搭配[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]發行者和[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]重新發行訂閱者。 這個程序不應該用於含有 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本中導入之資料類型的資料行。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_repldropcolumn [ @source_object = ] 'source_object', [ @column = ] 'column'   
    [ , [ @from_agent = ] from_agent]   
    [ , [ @schema_change_script = ] 'schema_change_script' ]   
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]   
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]   
```  
  
## <a name="arguments"></a>引數  
 [ @source_object =] '*source_object*'  
 這是包含要卸除之資料行的資料表發行項名稱。 *source_object*是 nvarchar(258)，沒有預設值。  
  
 [ @column =] '*資料行*'  
 這是資料表中要卸除的資料行名稱。 *資料行*是 sysname，沒有預設值。  
  
 [ @from_agent =] *from_agent*  
 預存程序是否由複寫代理程式執行。 *from_agent*是 int，預設值是 0，1 的值使用時是否由複寫代理程式執行這個預存程序和其他情況應該使用預設值為 0。  
  
 [ @schema_change_script =] '*schema_change_script&lt*'  
 指定用來修改系統產生之自訂預存程序的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指令碼的名稱和路徑。 *schema_change_script&lt*是 nvarchar(4000)，預設值是 NULL。 複寫可讓使用者自訂的自訂預存程序，取代異動複寫所用的一個或多個預設程序。 *schema_change_script&lt*執行後結構描述變更會對複寫的資料表發行項使用 sp_repldropcolumn，而且可用來執行下列其中一項：  
  
-   如果自動重新產生自訂的預存程序， *schema_change_script&lt*可用來卸除這些自訂預存程序和它們取代成使用者自訂預存程序來支援新的結構描述。  
  
-   如果未自動重新產生自訂預存程序， *schema_change_script&lt*可用來重新產生這些預存程序，或建立使用者定義的自訂預存程序。  
  
 [ @force_invalidate_snapshot =] *force_invalidate_snapshot*  
 啟用或停用使快照集失效的能力。 *force_invalidate_snapshot*是 bit，預設值是 1。  
  
 1 指定發行項的變更可能使快照集失效，若是如此，1 值會提供將出現之新快照集的權限。  
  
 0 指定發行項的變更不會使快照集失效。  
  
 [ @force_reinit_subscription =] *force_reinit_subscription*  
 啟用或停用重新初始化訂閱的能力。 *force_reinit_subscription*是 bit，預設值是 0。  
  
 0 指定發行項的變更不會使訂閱重新初始化。  
  
 1 指定發行項的變更可能使訂閱重新初始化，若是如此，1 值會提供將進行的訂閱重新初始化的權限。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="permissions"></a>Permissions  
 只有在發行者端的系統管理員 (sysadmin) 固定伺服器角色成員，或發行集資料庫中的 db_owner 或 db_ddladmin 固定資料庫角色成員，才能夠執行 sp_repldropcolumn。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 複寫中已被取代的功能](../../relational-databases/replication/deprecated-features-in-sql-server-replication.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
