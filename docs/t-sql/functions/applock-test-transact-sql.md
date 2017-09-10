---
title: "APPLOCK_TEST (TRANSACT-SQL) |Microsoft 文件"
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
- APPLOCK_TEST_TSQL
- APPLOCK_TEST
dev_langs:
- TSQL
helpviewer_keywords:
- locking [SQL Server], applications
- APPLOCK_TEST function
- applications [SQL Server], locks
- sessions [SQL Server], application locks
- testing application locks
ms.assetid: 4ea33d04-f8e9-46ff-ae61-985bd3eaca2c
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a272abaccb41653c9b1b0569738b74905e93e5c9
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="applocktest-transact-sql"></a>APPLOCK_TEST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回是否可以針對未取得鎖定的指定鎖定擁有者，來授與特定應用程式資源之鎖定的相關資訊。 APPLOCK_TEST 是一個應用程式鎖定功能，它作用於目前資料庫。 應用程式鎖定的範圍是資料庫。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
APPLOCK_TEST ( 'database_principal' , 'resource_name' , 'lock_mode' , 'lock_owner' )  
```  
  
## <a name="arguments"></a>引數  
**'** *database_principal* **'**  
這是已獲授與資料庫中的物件權限之使用者、角色或應用程式角色。 函式的呼叫端必須是成員*database_principal*， **dbo**，或**db_owner**固定的資料庫角色，才能成功呼叫函數。
  
**'** *resource_name* **'**  
這是用戶端應用程式所指定的鎖定資源名稱。 應用程式必須確定資源是唯一的。 指定的名稱會在內部雜湊成可儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 鎖定管理員中的值。 *resource_name*是**nvarchar （255)**沒有預設值。 *resource_name*以二進位來比較和區分大小寫，不論目前資料庫的定序設定為何。
  
**'** *lock_mode* **'**  
這是要取得的特定資源鎖定模式。 *lock_mode*是**nvarchar （32)** ，沒有預設值。 值可以是下列任一項：**共用**，**更新**， **IntentShared**， **IntentExclusive**，**獨佔**.
  
**'** *lock_owner* **'**  
已鎖定，這是擁有者*lock_owner*要求鎖定時的值。 *lock_owner*是**nvarchar （32)**。 這個值可以是**交易**（預設值） 或**工作階段**。 如果預設或**交易**明確指定，必須在交易中從執行 APPLOCK_TEST。
  
## <a name="return-types"></a>傳回型別
**smallint**
  
## <a name="return-value"></a>傳回值
當無法將鎖定授與指定的擁有者時，傳回 0；如果可以授與鎖定，便傳回 1。
  
## <a name="function-properties"></a>函式屬性
**不具決定性**
  
**Nonindexable**
  
**Nonparallelizable**
  
## <a name="examples"></a>範例  
在下列範例中，兩位使用者 (**使用者 A**和**使用者 B**) 擁有個別工作階段，執行下列一系列[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式。
  
**使用者 A**執行：
  
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
  
**使用者 B**接著執行：
  
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
  
**使用者 A**接著執行：
  
```sql
EXEC sp_releaseapplock @Resource='Form1', @DbPrincipal='public';  
GO  
```  
  
**使用者 B**接著執行：
  
```sql
SELECT APPLOCK_TEST('public', 'Form1', 'Exclusive', 'Transaction');  
--Result set: '1' (The lock is grantable.)  
GO  
```  
  
**使用者 A**和**使用者 B**接著同時執行：
  
```sql
COMMIT TRAN;  
GO  
```  
  
## <a name="see-also"></a>另請參閱
[APPLOCK_MODE &#40;TRANSACT-SQL &#41;](../../t-sql/functions/applock-mode-transact-sql.md)  
[sp_getapplock &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-getapplock-transact-sql.md)  
[sp_releaseapplock &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-releaseapplock-transact-sql.md)
  
  

