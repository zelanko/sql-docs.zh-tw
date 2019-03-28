---
title: sp_removedbreplication & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4b9f9c6c8c39355ec2c381c7fa4efa340da3addf
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58528660"
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
`[ @dbname = ] 'dbname'` 是資料庫的名稱。 *dbname* 是 **sysname**，預設值為 NULL。 如果是 NULL，則會使用目前資料庫。  
  
`[ @type = ] type` 是哪一個資料庫移除物件類型。 *型別*已**nvarchar(5)** 而且可以是下列值之一。  
  
|||  
|-|-|  
|**tran**|移除異動複寫發行物件。|  
|**merge**|移除合併式複寫發行物件。|  
|**兩者**（預設值）|移除所有的複寫發行物件。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_removedbreplication**用於所有類型的複寫。  
  
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
  
## <a name="see-also"></a>另請參閱  
 [停用發行和散發](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
