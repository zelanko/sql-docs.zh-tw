---
title: "APPLOCK_MODE (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- APPLOCK_MODE_TSQL
- APPLOCK_MODE
dev_langs:
- TSQL
helpviewer_keywords:
- locking [SQL Server], applications
- applications [SQL Server], locks
- sessions [SQL Server], application locks
- APPLOCK_MODE function
ms.assetid: e43d4917-77f1-45cc-b231-68ba7fee3385
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ceec0a5465187e1b470bd9eb8b1039a5b3d60aae
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="applockmode-transact-sql"></a>APPLOCK_MODE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回特定應用程式資源的鎖定擁有者所保留的鎖定模式。 APPLOCK_MODE 是一個應用程式鎖定功能，它作用於目前資料庫。 應用程式鎖定的範圍是資料庫。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
APPLOCK_MODE( 'database_principal' , 'resource_name' , 'lock_owner' )  
```  
  
## <a name="arguments"></a>引數  
'*database_principal*'  
這是已獲授與資料庫中的物件權限之使用者、角色或應用程式角色。 函式的呼叫端必須是成員*database_principal*、 dbo 或 db_owner 固定資料庫角色，才能成功呼叫函數。
  
'*resource_name*'  
這是用戶端應用程式所指定的鎖定資源名稱。 應用程式必須確定資源名稱是唯一的。 指定的名稱會在內部雜湊成可儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 鎖定管理員中的值。 *resource_name*是**nvarchar （255)**沒有預設值。 *resource_name*是以二進位來比較，且區分大小寫，不論目前資料庫的定序設定為何。
  
'*lock_owner*'  
已鎖定，這是擁有者*lock_owner*要求鎖定時的值。 *lock_owner*是**nvarchar （32)**，而且此值可以是**交易**（預設值） 或**工作階段**。
  
## <a name="return-types"></a>傳回型別
**nvarchar （32)**
  
## <a name="return-value"></a>傳回值
傳回特定應用程式資源的鎖定擁有者所保留的鎖定模式。 鎖定模式可以是下列任何值之一：
  
||||  
|-|-|-|  
|**NoLock**|**Update**|**\*SharedIntentExclusive**|  
|**IntentShared**|**IntentExclusive**|**\*UpdateIntentExclusive**|  
|**共用**|**排除**||  
  
*這個鎖定模式是其他鎖定模式的組合，無法利用 sp_getapplock 來明確取得。
  
## <a name="function-properties"></a>函式屬性
**不具決定性**
  
**Nonindexable**
  
**Nonparallelizable**
  
## <a name="examples"></a>範例  
有個別工作階段的兩位使用者 (使用者 A 和使用者 B) 執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的順序。
  
使用者 A 執行：
  
```sql
USE AdventureWorks2012;  
GO  
BEGIN TRAN;  
DECLARE @result int;  
EXEC @result=sp_getapplock  
    @DbPrincipal='public',  
    @Resource='Form1',  
    @LockMode='Shared',  
    @LockOwner='Transaction';  
SELECT APPLOCK_MODE('public', 'Form1', 'Transaction');  
GO  
```  
  
之後，使用者 B 執行：
  
```sql
Use AdventureWorks2012;  
GO  
BEGIN TRAN;  
SELECT APPLOCK_MODE('public', 'Form1', 'Transaction');  
--Result set: NoLock  
  
SELECT APPLOCK_TEST('public', 'Form1', 'Shared', 'Transaction');  
--Result set: 1 (Lock is grantable.)  
  
SELECT APPLOCK_TEST('public', 'Form1', 'Exclusive', 'Transaction');  
--Result set: 0 (Lock is not grantable.)  
GO  
```  
  
之後，使用者 A 執行：
  
```sql
EXEC sp_releaseapplock @Resource='Form1', @DbPrincipal='public';  
GO  
```  
  
之後，使用者 B 執行：
  
```sql
SELECT APPLOCK_TEST('public', 'Form1', 'Exclusive', 'Transaction');  
--Result set: '1' (The lock is grantable.)  
GO  
```  
  
之後，使用者 A 和使用者 B 都執行：
  
```sql
COMMIT TRAN;  
GO  
```  
  
## <a name="see-also"></a>另請參閱
[APPLOCK_TEST &#40;TRANSACT-SQL &#41;](../../t-sql/functions/applock-test-transact-sql.md)  
[sp_getapplock &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-getapplock-transact-sql.md)  
[sp_releaseapplock &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-releaseapplock-transact-sql.md)
  
  

