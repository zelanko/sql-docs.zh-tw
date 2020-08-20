---
description: DBCC CHECKIDENT (Transact-SQL)
title: DBCC CHECKIDENT (Transact-SQL)
ms.custom: ''
ms.date: 03/07/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CHECKIDENT
- DBCC CHECKIDENT
- CHECKIDENT_TSQL
- DBCC_CHECKIDENT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- checking identity values
- reseeding identity values
- resetting identity values
- identity values [SQL Server]
- identity values [SQL Server], checking
- modifying identity values
- current identity values
- DBCC CHECKIDENT statement
- identity values [SQL Server], reseeding
- reporting current identity values
ms.assetid: 2c00ee51-2062-4e47-8b19-d90f524c6427
author: pmasl
ms.author: umajay
monikerRange: = azuresqldb-current || >= sql-server-2016 || >= sql-server-linux-2017 || = azure-sqldw-latest||= sqlallproducts-allversions
ms.openlocfilehash: b7fd8592ed2643d25736539c91b3e3bedfdd75ea
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88479857"
---
# <a name="dbcc-checkident-transact-sql"></a>DBCC CHECKIDENT (Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中檢查指定資料表目前的識別值，必要的話，請變更識別值。 您也可以使用 DBCC CHECKIDENT，手動設定識別欄位的新目前識別值。  
  
 ![文章連結圖示](../../database-engine/configure-windows/media/topic-link.gif "文章連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql

-- Syntax for SQL Server and Azure SQL Database  

DBCC CHECKIDENT
 (
    table_name  
        [, { NORESEED | { RESEED [, new_reseed_value ] } } ]  
)  
[ WITH NO_INFOMSGS ]  
```  

```console
-- Syntax for Azure SQL Data Warehouse
DBCC CHECKIDENT   
 (   
    table_name  
        [RESEED, new_reseed_value ]   
)  
[ WITH NO_INFOMSGS ]  

```
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數

 *table_name*  
 這是要檢查目前識別值之資料表的名稱。 指定的資料表必須包含識別欄位。 資料表名稱必須遵照[識別碼](../../relational-databases/databases/database-identifiers.md)的規則。 兩個或三個部分的名稱必須加以分隔，例如 'Person.AddressType' 或 [Person.AddressType]。
  
 NORESEED  
 指定不應變更目前的識別值。  
  
 RESEED  
 指定應變更目前的識別值。  
  
 *new_reseed_value*  
 這是要當做識別欄位之目前值使用的新值。  
  
 WITH NO_INFOMSGS  
 隱藏所有參考訊息。  
  
## <a name="remarks"></a>備註

 目前識別值的特定更正會隨著參數規格而不同。  
  
|DBCC CHECKIDENT 命令|進行的識別更正|  
|-----------------------------|---------------------------------------------|  
|DBCC CHECKIDENT ( *table_name*, NORESEED )|不重設目前的識別值。 DBCC CHECKIDENT 會傳回識別欄位目前的識別值和最大值。 如果這兩個值不同，則應該重設識別值以防止值序列中發生錯誤或間距。|  
|DBCC CHECKIDENT ( *table_name* )<br /><br /> 或<br /><br /> DBCC CHECKIDENT ( *table_name*, RESEED )|如果資料表目前的識別值小於識別欄位所儲存的最大識別值，就會利用識別欄位中的最大值來重設它。 請參閱稍後的＜例外＞一節。|  
|DBCC CHECKIDENT ( *table_name*, RESEED, *new_reseed_value* )|目前的識別值設為 *new_reseed_value*。 如果建立好資料表之後並未插入任何資料列，或者已經使用 TRUNCATE TABLE 陳述式來移除所有資料列，則執行 DBCC CHECKIDENT 之後所插入的第一個資料列就會使用 *new_reseed_value* 作為識別。 若資料表中有資料列，或已使用 DELETE 陳述式移除所有資料列，插入的下一列就會使用 *new_reseed_value* + [目前增量](../../t-sql/functions/ident-incr-transact-sql.md)值。 若交易插入一個資料行，並於稍後進行復原，則下一個插入的資料行會使用 *new_reseed_value* + [current increment](../../t-sql/functions/ident-incr-transact-sql.md) 值，如同資料列已遭到刪除。 如果資料表不是空的，則將識別值設定為小於識別欄位中最大值的數字，可能會導致下列其中一種狀況：<br /><br /> -如果識別欄位有 PRIMARY KEY 或 UNIQUE 條件約束，則之後對資料表進行插入作業時會產生錯誤訊息 2627，因為所產生的識別值會與現有值相衝突。<br /><br /> -如果沒有 PRIMARY KEY 或 UNIQUE 條件約束，則之後進行的插入作業會導致重複的識別值。|  
  
## <a name="exceptions"></a>例外狀況

 下表列出 DBCC CHECKIDENT 不會自動重設目前識別值的狀況，並提供重設值的方法。  
  
|條件|重設方法|  
|---------------|-------------------|  
|目前的識別值大於資料表中的最大值。|執行 DBCC CHECKIDENT (*table_name*, NORESEED) 來判斷資料行中的目前最大值。 接下來，在 DBCC CHECKIDENT (*table_name*, RESEED,*new_reseed_value*) 命令中將該值指定為 *new_reseed_value*。<br /><br /> -或-<br /><br /> 將 *new_reseed_value* 設定為非常低的值，並執行 DBCC CHECKIDENT (*table_name*, RESEED,*new_reseed_value*)，然後執行 DBCC CHECKIDENT (*table_name*, RESEED) 以更正此值。|  
|資料表中的所有資料列都遭到刪除。|執行 DBCC CHECKIDENT (*table_name*, RESEED,*new_reseed_value*)，並將 *new_reseed_value* 設定為所需的起始值。|  
  
## <a name="changing-the-seed-value"></a>變更初始值

 初始值就是針對載入資料表的第一個資料列插入到識別欄位中的值。 所有後續資料列都會包含目前的識別值加上遞增值，其中目前的識別值就是針對資料表或檢視表所產生的最後一個識別值。  
  
 您無法使用 DBCC CHECKIDENT 來執行下列工作：  
  
- 變更建立資料表或檢視時針對識別欄位所指定的原始初始值。  
  
- 重設資料表或檢視表中現有的資料列。  
  
 若要變更原始初始值並重設任何現有的資料列，請卸除識別欄位並指定新的初始值來重建此識別欄位。 當資料表包含資料時，識別數字就會加入至含有指定初始值和遞增值的現有資料列。 但是，無法保證資料列的更新順序。  
  
## <a name="result-sets"></a>結果集

 不論您是否針對包含識別欄位的資料表指定任何選項，DBCC CHECKIDENT 都會針對所有作業傳回下列訊息 (只有一個例外)。 該作業會指定新的初始值。  
  
`Checking identity information: current identity value '\<current identity value>', current column value '\<current column value>'. DBCC execution completed. If DBCC printed error messages, contact your system administrator.`
  
 當使用 DBCC CHECKIDENT 來透過 RESEED *new_reseed_value* 指定新的初始值時，將會傳回下列訊息。  
  
`Checking identity information: current identity value '\<current identity value>'. DBCC execution completed. If DBCC printed error messages, contact your system administrator.`
  
## <a name="permissions"></a>權限

 呼叫者必須擁有包含資料表的結構描述，或者必須是 **sysadmin** 固定伺服器角色、**db_owner** 固定資料庫角色，或 **db_ddladmin** 固定資料庫角色的成員。

Azure SQL 資料倉儲需要 **db_owner** 權限。
  
## <a name="examples"></a>範例  
  
### <a name="a-resetting-the-current-identity-value-if-its-needed"></a>A. 必要的話，重設目前的識別值  
 在必要時，下列範例會重設 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中指定資料表目前的識別值。  
  
```sql
USE AdventureWorks2012;  
GO  
DBCC CHECKIDENT ('Person.AddressType');  
GO  
```  
  
### <a name="b-reporting-the-current-identity-value"></a>B. 報告目前的識別值

 下列範例會報告 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中指定資料表目前的識別值，且如果識別值不正確則不會更正該值。  
  
```sql
USE AdventureWorks2012;
GO  
DBCC CHECKIDENT ('Person.AddressType', NORESEED);
GO  
```  
  
### <a name="c-forcing-the-current-identity-value-to-a-new-value"></a>C. 將目前識別值強制設為新的值  
 下列範例會強制將 `AddressTypeID` 資料表中 `AddressType` 資料行內的目前識別值設定為 10。 因為資料表目前有資料列，所以下一個插入的資料列會使用 11 為值，也就是為資料行定義的新目前識別值加 1 (這是資料行的增量值)。  

```sql
USE AdventureWorks2012;  
GO  
DBCC CHECKIDENT ('Person.AddressType', RESEED, 10);  
GO  
```

### <a name="d-resetting-the-identity-value-on-an-empty-table"></a>D. 在空白資料表上重設識別值

 下列範例會在刪除資料表中所有記錄後，強制將 `ErrorLog` 資料表中 `ErrorLogID` 資料行內的目前識別值設定為 1。 因為資料表沒有現有的資料列，所以下一個插入的資料列將會使用 1 作為值，也就是目前的識別值，而不新增針對資料行定義的遞增值。  
  
```sql
USE AdventureWorks2012;  
GO  
TRUNCATE TABLE dbo.ErrorLog
GO
DBCC CHECKIDENT ('dbo.ErrorLog', RESEED, 1);  
GO  
```  
  
## <a name="see-also"></a>另請參閱

[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[IDENTITY &#40;屬性&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)  
[複寫識別資料行](../../relational-databases/replication/publish/replicate-identity-columns.md)  
[USE &#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)  
[IDENT_SEED &#40;Transact-SQL&#41;](../../t-sql/functions/ident-seed-transact-sql.md)  
[IDENT_INCR &#40;Transact-SQL&#41;](../../t-sql/functions/ident-incr-transact-sql.md)  
