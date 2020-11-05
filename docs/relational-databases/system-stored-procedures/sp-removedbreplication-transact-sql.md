---
title: 'sp_removedbreplication (T-sql) '
description: 描述用來移除發行集資料庫上之所有複寫物件的 sp_removedbreplication 預存程式，以進行 SQL Server 複寫。
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_removedbreplication
- sp_removedbreplication_TSQL
helpviewer_keywords:
- sp_removedbreplication
ms.assetid: cb98d571-d1eb-467b-91f7-a6e091009672
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b8b8918bf659e6965fed1f9af0342f8295947509
ms.sourcegitcommit: b3a711a673baebb2ff10d7142b209982b46973ae
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/05/2020
ms.locfileid: "93364837"
---
# <a name="sp_removedbreplication-transact-sql"></a>sp_removedbreplication (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  這個預存程序會移除 SQL Server 發行者執行個體上的發行集資料庫的所有複寫物件，或移除 SQL Server 訂閱者執行個體上訂閱資料庫上的所有複寫物件。 在適當的資料庫中執行，或如果在相同的執行個體上的另一個資料庫的內容中執行時，指定要移除複寫物件所在的資料庫。 此程序中不會移除其他資料庫中的物件，例如散發資料庫。  
  
> [!NOTE]  
>  只有在其他移除複寫物件的方法都失敗時，才應使用此程序。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_removedbreplication [ [ @dbname = ] 'dbname' ]  
    [ , [ @type = ] type ]   
```  
  
## <a name="arguments"></a>引數  
`[ @dbname = ] 'dbname'` 這是資料庫的名稱。 *dbname* 是 **sysname** ，預設值為 NULL。 如果是 NULL，則會使用目前資料庫。  
  
`[ @type = ] type` 這是要移除資料庫物件的複寫類型。 *類型* 是 **Nvarchar (5)** 而且可以是下列其中一個值。  
  
|||  
|-|-|  
|**事務**|移除異動複寫發行物件。|  
|**合併**|移除合併式複寫發行物件。|  
|**(預設** 值) |移除所有的複寫發行物件。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_removedbreplication** 用於所有類型的複寫中。  
  
 在還原不需要還原之複寫物件的複寫資料庫時， **sp_removedbreplication** 會很有用。  
  
 **sp_removedbreplication** 不能用於標示為唯讀的資料庫。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色的成員，才可以執行 **sp_removedbreplication** 。  
  
## <a name="examples"></a>範例

### <a name="a-remove-replication-objects-adventureworks2012replica-subscription-database"></a>A. 移除複寫物件，AdventureWorks2012Replica 訂閱資料庫
 [!code-sql[HowTo#sp_removedbreplication](../../relational-databases/replication/codesnippet/tsql/sp-removedbreplication-t_1.sql)]  
  
### <a name="b-remove-replication-objects-adventureworksreplica-subscription-database"></a>B. 移除複寫物件，AdventureWorksReplica 訂閱資料庫
  
```sql
-- Remove replication objects from the subscription database on MYSUB.  
DECLARE @subscriptionDB AS sysname  
SET @subscriptionDB = N'AdventureWorksReplica'  
  
-- Remove replication objects from a subscription database (if necessary).  
USE master  
EXEC sp_removedbreplication @subscriptionDB  
GO  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [停用發行和散發](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
