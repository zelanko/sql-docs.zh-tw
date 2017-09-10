---
title: "DBCC OPENTRAN (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC_OPENTRAN_TSQL
- DBCC OPENTRAN
- OPENTRAN_TSQL
- OPENTRAN
dev_langs:
- TSQL
helpviewer_keywords:
- status information [SQL Server], transactions
- transactions [SQL Server], status information
- DBCC OPENTRAN statement
- open transactions
- displaying transaction information
- checking open transactions
- oldest transactions [SQL Server]
ms.assetid: 63163843-226f-42d3-9e2c-b634fbf06943
caps.latest.revision: 40
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f3d3b47d9bc553edd49f6f401d1a1c7a857d0a7d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-opentran-transact-sql"></a>DBCC OPENTRAN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

DBCC OPENTRAN 有助於識別可能阻礙記錄截斷的使用中交易。 DBCC OPENTRAN 顯示在指定之資料庫的交易記錄內，最舊的使用中交易以及最舊的分散式和非分散式複寫交易 (如果有的話) 的相關資訊。 只有在記錄內有使用中的交易或資料庫包含複寫資訊時，才會顯示結果。 如果記錄內沒有使用中的交易，就會顯示參考用訊息。
  
> [!NOTE]  
>  非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者不支援 DBCC OPENTRAN。  
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DBCC OPENTRAN   
[   
    ( [ database_name | database_id | 0 ] ) ]  
    { [ WITH TABLERESULTS ]  
      [ , [ NO_INFOMSGS ] ]  
    }  
]   
```  
  
## <a name="arguments"></a>引數  
 *database_name* | *database_id*| 0  
 這是要顯示最舊交易資訊之資料庫的名稱或識別碼。 若未指定，或指定 0，就會使用目前的資料庫。 資料庫名稱必須符合的規則[識別碼](../../relational-databases/databases/database-identifiers.md)。  
  
 TABLERESULTS  
 指定可載入資料表的表格式格式結果。 請利用這個選項來建立結果資料表，這些結果可插入資料表以進行比較。 當未指定這個選項時，會將結果格式化，以便閱讀。  
  
 NO_INFOMSGS  
 隱藏所有參考訊息。  
  
## <a name="remarks"></a>備註  
請利用 DBCC OPENTRAN 來判斷開啟的交易是否在交易記錄內。 當您使用 BACKUP LOG 陳述式時，只能截斷記錄非使用中的部分。開啟的交易可以防止記錄徹底截斷。 若要識別開啟的交易，請利用 sp_who 來取得系統處理序識別碼。
  
## <a name="result-sets"></a>結果集  
當沒有開啟的交易時，DBCC OPENTRAN 會傳回下列結果集：
  
```sql
No active open transactions.  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissions  
需要 **系統管理員** 固定伺服器角色或 **db_owner** 固定資料庫角色中的成員資格。
  
## <a name="examples"></a>範例  
### <a name="a-returning-the-oldest-active-transaction"></a>A. 傳回最舊的使用中交易  
下列範例會取得目前資料庫的交易資訊。 結果可能各不相同。
  
```sql  
CREATE TABLE T1(Col1 int, Col2 char(3));  
GO  
BEGIN TRAN  
INSERT INTO T1 VALUES (101, 'abc');  
GO  
DBCC OPENTRAN;  
ROLLBACK TRAN;  
GO  
DROP TABLE T1;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`Transaction information for database 'master'.`
  
`Oldest active transaction:`
  
`SPID (server process ID) : 52`
  
`UID (user ID) : -1`
  
`Name          : user_transaction`
  
`LSN           : (518:1576:1)`
  
`Start time    : Jun  1 2004  3:30:07:197PM`
  
`SID           : 0x010500000000000515000000a065cf7e784b9b5fe77c87709e611500`
  
`DBCC execution completed. If DBCC printed error messages, contact your system administrator.`
  
> [!NOTE]  
>  「UID (使用者識別碼)」結果無意義而且將會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的未來版本中移除。  
  
### <a name="b-specifying-the-with-tableresults-option"></a>B. 指定 WITH TABLERESULTS 選項  
下列範例會將 DBCC OPENTRAN 命令的結果載入暫存資料表中。
  
```sql  
-- Create the temporary table to accept the results.  
CREATE TABLE #OpenTranStatus (  
   ActiveTransaction varchar(25),  
   Details sql_variant   
   );  
-- Execute the command, putting the results in the table.  
INSERT INTO #OpenTranStatus   
   EXEC ('DBCC OPENTRAN WITH TABLERESULTS, NO_INFOMSGS');  
  
-- Display the results.  
SELECT * FROM #OpenTranStatus;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
[BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)  
[認可交易 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DB_ID &#40;TRANSACT-SQL &#41;](../../t-sql/functions/db-id-transact-sql.md)  
[ROLLBACK TRANSACTION &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)
  
  

