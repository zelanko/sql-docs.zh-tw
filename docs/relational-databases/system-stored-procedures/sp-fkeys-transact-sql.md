---
title: sp_fkeys （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fkeys
- sp_fkeys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fkeys
ms.assetid: 18110444-d38d-4cff-90d2-d1fc6236668b
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2c280be43be2ef4f14e57321cb96420e6cf51eb6
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86012682"
---
# <a name="sp_fkeys-transact-sql"></a>sp_fkeys (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  傳回目前環境的邏輯外部索引鍵資訊。 這個程序會顯示包括已停用之外部索引鍵的外部索引鍵關聯性。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
sp_fkeys [ @pktable_name = ] 'pktable_name'   
     [ , [ @pktable_owner = ] 'pktable_owner' ]   
     [ , [ @pktable_qualifier = ] 'pktable_qualifier' ]   
     { , [ @fktable_name = ] 'fktable_name' }   
     [ , [ @fktable_owner = ] 'fktable_owner' ]   
     [ , [ @fktable_qualifier = ] 'fktable_qualifier' ]  
```  
  
## <a name="arguments"></a>引數  
 [ @pktable_name =] '*pktable_name*'  
 這是用來傳回目錄資訊的資料表名稱，含主索引鍵。 *pktable_name*是**sysname**，預設值是 Null。 不支援萬用字元的模式比對。 必須提供這個參數或*fktable_name*參數（或兩者）。  
  
 [ @pktable_owner =] '*pktable_owner*'  
 這是用來傳回目錄資訊之資料表（含主鍵）的擁有者名稱。 *pktable_owner*是**sysname**，預設值是 Null。 不支援萬用字元的模式比對。 如果未指定*pktable_owner* ，就會套用基礎 DBMS 的預設資料表可見度規則。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，如果目前使用者擁有一份含指定名稱的資料表，就會傳回這份資料表的資料行。 如果未指定*pktable_owner* ，而且目前的使用者並未擁有具有指定*pktable_name*的資料表，則程式會尋找資料庫擁有者所擁有之指定*pktable_name*的資料表。 如果資料表存在，就會傳回它的資料行。  
  
 [ @pktable_qualifier =] '*pktable_qualifier*'  
 這是資料表 (含主索引鍵) 限定詞的名稱。 *pktable_qualifier*是 sysname，預設值是 Null。 各種 DBMS 產品都支援三部分的資料表命名（*qualifier.owner.name*）。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這個限定詞代表資料庫名稱。 在某些產品中，它代表資料表之資料庫環境的伺服器名稱。  
  
 [ @fktable_name =] '*fktable_name*'  
 這是用來傳回目錄資訊之資料表 (含外部索引鍵) 的名稱。 *fktable_name*是 sysname，預設值是 Null。 不支援萬用字元的模式比對。 必須提供這個參數或*pktable_name*參數（或兩者）。  
  
 [ @fktable_owner =] '*fktable_owner*'  
 這是用來傳回目錄資訊之資料表 (含外部索引鍵) 的擁有者名稱。 *fktable_owner*是**sysname**，預設值是 Null。 不支援萬用字元的模式比對。 如果未指定*fktable_owner* ，就會套用基礎 DBMS 的預設資料表可見度規則。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，如果目前使用者擁有一份含指定名稱的資料表，就會傳回這份資料表的資料行。 如果未指定*fktable_owner* ，而且目前的使用者並未擁有具有指定*fktable_name*的資料表，則程式會尋找資料庫擁有者所擁有之指定*fktable_name*的資料表。 如果資料表存在，就會傳回它的資料行。  
  
 [ @fktable_qualifier =] '*fktable_qualifier*'  
 這是資料表 (含外部索引鍵) 限定詞的名稱。 *fktable_qualifier*是**sysname**，預設值是 Null。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這個限定詞代表資料庫名稱。 在某些產品中，它代表資料表之資料庫環境的伺服器名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 None  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|PKTABLE_QUALIFIER|**sysname**|資料表 (含主索引鍵) 限定詞的名稱。 這個欄位可以是 NULL。|  
|PKTABLE_OWNER|**sysname**|資料表 (含主索引鍵) 擁有者的名稱。 這個欄位一律會傳回值。|  
|PKTABLE_NAME|**sysname**|資料表 (含主索引鍵) 的名稱。 這個欄位一律會傳回值。|  
|PKCOLUMN_NAME|**sysname**|對於傳回之 TABLE_NAME 的每個資料行而言，這是主索引鍵資料行的名稱。 這個欄位一律會傳回值。|  
|FKTABLE_QUALIFIER|**sysname**|資料表 (含外部索引鍵) 限定詞的名稱。 這個欄位可以是 NULL。|  
|FKTABLE_OWNER|**sysname**|資料表 (含外部索引鍵) 擁有者的名稱。 這個欄位一律會傳回值。|  
|FKTABLE_NAME|**sysname**|資料表 (含外部索引鍵) 的名稱。 這個欄位一律會傳回值。|  
|FKCOLUMN_NAME|**sysname**|對於傳回之 TABLE_NAME 的每個資料行而言，這是外部索引鍵資料行的名稱。 這個欄位一律會傳回值。|  
|KEY_SEQ|**smallint**|資料行在多重資料行主索引鍵中的序號。 這個欄位一律會傳回值。|  
|UPDATE_RULE|**smallint**|當 SQL 作業是更新時，外部索引鍵所套用的動作。  可能的值：<br /> 0=外部索引鍵的 CASCADE 變更。<br /> 1=如果外部索引鍵存在，則是 NO ACTION 變更。<br />   2 = 設定 null <br /> 3 = 設定預設值 |  
|DELETE_RULE|**smallint**|當 SQL 作業是刪除時，外部索引鍵所套用的動作。 可能的值：<br /> 0=外部索引鍵的 CASCADE 變更。<br /> 1=如果外部索引鍵存在，則是 NO ACTION 變更。<br />   2 = 設定 null <br /> 3 = 設定預設值 |  
|FK_NAME|**sysname**|外部索引鍵識別碼。 如果不適用於資料來源的話，它便是 NULL。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回 FOREIGN KEY 條件約束名稱。|  
|PK_NAME|**sysname**|主索引鍵識別碼。 如果不適用於資料來源的話，它便是 NULL。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回 PRIMARY KEY 條件約束名稱。|  
  
 傳回的結果依  FKTABLE_QUALIFIER、FKTABLE_OWNER、FKTABLE_NAME 和 KEY_SEQ 來排序。  
  
## <a name="remarks"></a>備註  
 您可以遵照下列步驟來實作含已停用之外部索引鍵之資料表的應用程式編碼：  
  
-   在使用資料表時，暫時停用條件約束檢查 (ALTER TABLE NOCHECK 或 CREATE TABLE NOT FOR REPLICATION)，稍後再重新啟用它。  
  
-   利用觸發程序或應用程式碼來強制實施關聯性。  
  
如果提供了主索引鍵資料表名稱，且外部索引鍵資料表名稱是 NULL，sp_fkeys 會傳回所有含有指向給定資料表的外部索引鍵之資料表。 如果提供了外部索引鍵資料表名稱，且主索引鍵資料表名稱是 NULL，sp_fkeys 會傳回所有透過主索引鍵/外部索引鍵關聯性來與外部索引鍵資料表中之外部索引鍵產生關聯的資料表。  
  
sp_fkeys 預存程序相當於 ODBC 中的 SQLForeignKeys。  
  
## <a name="permissions"></a>權限  
 需要 `SELECT` 架構的許可權。  
  
## <a name="examples"></a>範例  
 下列範例會擷取 `HumanResources.Department` 資料庫之 `AdventureWorks2012` 資料表的外部索引鍵清單。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_fkeys @pktable_name = N'Department'  
    ,@pktable_owner = N'HumanResources';  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會擷取 `DimDate` 資料庫之 `AdventureWorksPDW2012` 資料表的外部索引鍵清單。 不會傳回任何資料列，因為 [!INCLUDE[ssDW](../../includes/ssdw-md.md)] 不支援外鍵。  
  
```sql  
EXEC sp_fkeys @pktable_name = N'DimDate;  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的目錄預存程式](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [&#40;Transact-sql&#41;的系統預存程式](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_pkeys &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-pkeys-transact-sql.md)  
  
  

