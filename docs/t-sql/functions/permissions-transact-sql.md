---
title: PERMISSIONS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PERMISSIONS_TSQL
- PERMISSIONS
dev_langs:
- TSQL
helpviewer_keywords:
- permissions [SQL Server], verifying
- current permission status
- users [SQL Server], permissions status
- checking permission status
- security [SQL Server], permissions
- verifying permission status
- testing permissions
- PERMISSIONS function
ms.assetid: 81625a56-b160-4424-91c5-1ce8b259a8e6
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: fc38de8bffc09461dc69a24acf15ce143276422b
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "73843634"
---
# <a name="permissions-transact-sql"></a>PERMISSIONS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回包含點陣圖的值，表示目前使用者的陳述式、物件或資料行權限。  
  
 **重要事項**：[!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 請改使用 [fn_my_permissions](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md) 和 [Has_Perms_By_Name](../../t-sql/functions/has-perms-by-name-transact-sql.md)。 繼續使用 PERMISSIONS 函數可能會降低效能。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
PERMISSIONS ( [ objectid [ , 'column' ] ] )  
```  
  
## <a name="arguments"></a>引數  
 *objectid*  
 這是安全性實體的識別碼。 如果未指定 *objectid*，則點陣圖值包含目前使用者的陳述式權限；否則，點陣圖包含目前使用者安全性實體的權限。 指定的安全性實體必須存在於目前資料庫中。 使用 [OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md) 函式來決定 *objectid* 值。  
  
 **'** *column* **'**  
 這是要傳回權限資訊之資料行的選擇性名稱。 資料行必須是 *objectid* 指定的資料表中有效的資料行名稱。  
  
## <a name="return-types"></a>傳回型別  
 **int**  
  
## <a name="remarks"></a>備註  
 PERMISSIONS 可用來決定目前使用者是否有必要的權限，來執行陳述式或將權限授與 (GRANT) 另一位使用者。  
  
 傳回的權限資訊是 32 位元點陣圖。  
  
 較低 16 位元反映出授與使用者的權限，以及套用至 Windows 群組的權限，和目前使用者是成員的固定伺服器角色。 例如，若未指定 *objectid*，傳回值 66 (十六進位值 0x42) 表示使用者有權限執行 CREATE TABLE (十進位值 2) 和 BACKUP DATABASE (十進位值 64) 陳述式。  
  
 較高 16 位元反映使用者可授與 (GRANT) 其他使用者的權限。 除了移位至左邊 16 位元 (乘以 65536) 之外，較高 16 位元與下表所描述之較低 16 位元的解譯方式完全一樣。 例如，指定 *objectid* 時，0x8 (十進位值 8) 就是表示 INSERT 權限的位元。 而 0x80000 (十進位值 524288) 表示 GRANT INSERT 權限的能力，因為 524288 = 8 x 65536。  
  
 因為角色的成員資格，沒有權限執行陳述式的使用者仍可授與該權限給另一位使用者。  
  
 下表顯示用於陳述式權限的位元 (未指定 *objectid*)。  
  
|位元 (dec)|位元 (hex)|陳述式權限|  
|-----------------|-----------------|--------------------------|  
|1|0x1|CREATE DATABASE (僅限 master 資料庫)|  
|2|0x2|CREATE TABLE|  
|4|0x4|CREATE PROCEDURE|  
|8|0x8|CREATE VIEW|  
|16|0x10|CREATE RULE|  
|32|0x20|CREATE DEFAULT|  
|64|0x40|BACKUP DATABASE|  
|128|0x80|BACKUP LOG|  
|256|0x100|Reserved|  
  
 下表顯示用於只有在指定 *objectid* 時才會傳回之物件權限的位元。  
  
|位元 (dec)|位元 (hex)|陳述式權限|  
|-----------------|-----------------|--------------------------|  
|1|0x1|SELECT ALL|  
|2|0x2|UPDATE ALL|  
|4|0x4|REFERENCES ALL|  
|8|0x8|Insert|  
|16|0x10|刪除|  
|32|0x20|EXECUTE (僅限程序)|  
|4096|0x1000|SELECT ANY (至少一個資料行)|  
|8192|0x2000|UPDATE ANY|  
|16384|0x4000|REFERENCES ANY|  
  
 下表顯示用於同時指定 *objectid* 和資料行時傳回之資料行層級物件權限的位元。  
  
|位元 (dec)|位元 (hex)|陳述式權限|  
|-----------------|-----------------|--------------------------|  
|1|0x1|SELECT|  
|2|0x2|UPDATE|  
|4|0x4|REFERENCES|  
  
 當指定的參數為 NULL 或無效時，會傳回 NULL (例如不存在的 *objectid* 或資料行)。 不套用權限的位元值 (例如，用於資料表的 EXECUTE 權限 bit 0x20) 尚未定義。  
  
 使用位元 AND (&) 運算子，來決定 PERMISSIONS 函式所傳回點陣圖中設定的每一個位元。  
  
 sp_helprotect 系統預存程序也用來傳回目前資料庫中使用者的權限清單。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-the-permissions-function-with-statement-permissions"></a>A. 搭配陳述式權限來使用 PERMISSIONS 函數  
 下列範例會決定目前使用者是否可執行 `CREATE TABLE` 陳述式。  
  
```  
IF PERMISSIONS()&2=2  
   CREATE TABLE test_table (col1 INT)  
ELSE  
   PRINT 'ERROR: The current user cannot create a table.';  
```  
  
### <a name="b-using-the-permissions-function-with-object-permissions"></a>B. 搭配物件權限來使用 PERMISSIONS 函數  
 下列範例會決定目前使用者是否可將資料列插入 `Address` 資料庫的 `AdventureWorks2012` 資料表中。  
  
```  
IF PERMISSIONS(OBJECT_ID('AdventureWorks2012.Person.Address','U'))&8=8   
   PRINT 'The current user can insert data into Person.Address.'  
ELSE  
   PRINT 'ERROR: The current user cannot insert data into Person.Address.';  
```  
  
### <a name="c-using-the-permissions-function-with-grantable-permissions"></a>C. 搭配可授與的權限來使用 PERMISSIONS 函數  
 下列範例會決定目前使用者是否可授與 `Address` 資料庫中 `AdventureWorks2012` 資料表的 INSERT 權限給另一位使用者。  
  
```  
IF PERMISSIONS(OBJECT_ID('AdventureWorks2012.Person.Address','U'))&0x80000=0x80000  
   PRINT 'INSERT on Person.Address is grantable.'  
ELSE  
   PRINT 'You may not GRANT INSERT permissions on Person.Address.';  
```  
  
## <a name="see-also"></a>另請參閱  
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [OBJECT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_helprotect &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [系統函數 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)  
  
  
