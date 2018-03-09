---
title: "sp_removedbreplication (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_removedbreplication
- sp_removedbreplication_TSQL
helpviewer_keywords:
- sp_removedbreplication
ms.assetid: cb98d571-d1eb-467b-91f7-a6e091009672
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e2c44063c4ab9019f191136ead3c890f50806885
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="spremovedbreplication-transact-sql"></a>sp_removedbreplication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [  **@dbname=**] **'***dbname***'**  
 這是資料庫的名稱。 *dbname* 是 **sysname**，預設值為 NULL。 如果是 NULL，則會使用目前資料庫。  
  
 [  **@type**  =]*類型*  
 這是要移除資料庫物件的複寫類型。 *型別*是**nvarchar （5)**而且可以是下列值之一。  
  
|||  
|-|-|  
|**tran**|移除異動複寫發行物件。|  
|**合併式**|移除合併式複寫發行物件。|  
|**同時**（預設值）|移除所有的複寫發行物件。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_removedbreplication**用於所有複寫類型。  
  
 **sp_removedbreplication**還原複寫的資料庫不必還原沒有複寫物件時很有用。  
  
 **sp_removedbreplication**不能針對已標示為唯讀的資料庫。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_removedbreplication](../../relational-databases/replication/codesnippet/tsql/sp-removedbreplication-t_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_removedbreplication**。  
  
## <a name="example"></a>範例  
  
```  
-- Remove replication objects from the subscription database on MYSUB.  
DECLARE @subscriptionDB AS sysname  
SET @subscriptionDB = N'AdventureWorksReplica'  
  
-- Remove replication objects from a subscription database (if necessary).  
USE master  
EXEC sp_removedbreplication @subscriptionDB  
GO  
  
```  
  
## <a name="see-also"></a>請參閱＜  
 [停用發行和散發](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
