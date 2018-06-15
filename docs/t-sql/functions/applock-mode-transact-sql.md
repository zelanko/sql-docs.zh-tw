---
title: APPLOCK_MODE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
manager: craigg
ms.openlocfilehash: 064a34cc6239a187d1f519d2dade38f555a5dcec
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33053465"
---
# <a name="applockmode-transact-sql"></a>APPLOCK_MODE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

此函數傳回特定應用程式資源的鎖定擁有者所持有的鎖定模式。 APPLOCK_MODE 是應用程式鎖定函數，會在目前的資料庫上運作。 資料庫是應用程式鎖定的範圍。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
APPLOCK_MODE( 'database_principal' , 'resource_name' , 'lock_owner' )  
```  
  
## <a name="arguments"></a>引數  
'*database_principal*'  
可被授與資料庫中物件權限的使用者、角色或應用程式角色。 函數的呼叫者必須是 *database_principal*、dbo 或 db_owner 固定資料庫角色的成員，才能成功呼叫函數。
  
'*resource_name*'  
用戶端應用程式指定的鎖定資源名稱。 應用程式必須確定資源名稱是唯一的。 指定的名稱會在內部雜湊成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 鎖定管理員可儲存在內部的值。 *resource_name* 是沒有預設值的 **nvarchar(255)**。 *resource_name* 是以二進位來比較，不論目前資料庫的定序設定為何，都會區分大小寫。
  
'*lock_owner*'  
為鎖定的擁有者，也就是要求鎖定時的 *lock_owner* 值。 *lock_owner* 是 **nvarchar(32)**，而且此值可以是**交易** (預設值) 或**工作階段**。
  
## <a name="return-types"></a>傳回型別
**nvarchar(32)**
  
## <a name="return-value"></a>傳回值
傳回特定應用程式資源的鎖定擁有者所保留的鎖定模式。 鎖定模式可以具有以下任一個值：
  
||||  
|-|-|-|  
|**NoLock**|**Update**|**\*SharedIntentExclusive**|  
|**IntentShared**|**IntentExclusive**|**\*UpdateIntentExclusive**|  
|**Shared**|**排除**||  
  
*這個鎖定模式是其他鎖定模式的組合，且 sp_getapplock 無法明確地取得它。
  
## <a name="function-properties"></a>函式屬性
**Nondeterministic**
  
**Nonindexable**
  
**Nonparallelizable**
  
## <a name="examples"></a>範例  
有個別工作階段的兩個使用者 (使用者 A 和使用者 B)，按照下列順序執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。
  
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
[APPLOCK_TEST &#40;Transact-SQL&#41;](../../t-sql/functions/applock-test-transact-sql.md)  
[sp_getapplock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getapplock-transact-sql.md)  
[sp_releaseapplock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-releaseapplock-transact-sql.md)
  
  
