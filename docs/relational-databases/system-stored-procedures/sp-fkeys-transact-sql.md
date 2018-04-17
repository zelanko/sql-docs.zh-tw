---
title: sp_fkeys (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_fkeys
- sp_fkeys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fkeys
ms.assetid: 18110444-d38d-4cff-90d2-d1fc6236668b
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b8d8e8616e919f3d457572aced700b65ea0a21ec
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="spfkeys-transact-sql"></a>sp_fkeys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

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
 [ @pktable_name=] '*b l e _*'  
 這是用來傳回目錄資訊的資料表名稱，含主索引鍵。 *b l e _*是**sysname**，預設值是 NULL。 不支援萬用字元的模式比對。 這個參數或*fktable_name*必須提供參數，或兩者。  
  
 [ @pktable_owner=] '*pktable_owner*'  
 是用來傳回目錄資訊之資料表 （含主索引鍵） 的擁有者名稱。 *pktable_owner*是**sysname**，預設值是 NULL。 不支援萬用字元的模式比對。 如果*pktable_owner*未指定，套用基礎 dbms 的預設資料表可見性規則。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，如果目前使用者擁有一份含指定名稱的資料表，就會傳回這份資料表的資料行。 如果*pktable_owner*未指定目前使用者並未擁有含有指定的資料表和*b l e _*，程序會尋找具有指定的資料表*ble_*資料庫擁有者所擁有。 如果資料表存在，就會傳回它的資料行。  
  
 [ @pktable_qualifier =] '*pktable_qualifier*'  
 這是資料表 (含主索引鍵) 限定詞的名稱。 *pktable_qualifier*是 sysname，預設值是 NULL。 各種 DBMS 產品都支援三部分的資料表命名 (*q*)。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這個限定詞代表資料庫名稱。 在某些產品中，它代表資料表之資料庫環境的伺服器名稱。  
  
 [ @fktable_name=] '*fktable_name*'  
 這是用來傳回目錄資訊之資料表 (含外部索引鍵) 的名稱。 *fktable_name*是 sysname，預設值是 NULL。 不支援萬用字元的模式比對。 這個參數或*b l e _*必須提供參數，或兩者。  
  
 [ @fktable_owner =] '*fktable_owner*'  
 這是用來傳回目錄資訊之資料表 (含外部索引鍵) 的擁有者名稱。 *fktable_owner*是**sysname**，預設值是 NULL。 不支援萬用字元的模式比對。 如果*fktable_owner*未指定，套用基礎 dbms 的預設資料表可見性規則。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，如果目前使用者擁有一份含指定名稱的資料表，就會傳回這份資料表的資料行。 如果*fktable_owner*未指定目前使用者並未擁有含有指定的資料表和*fktable_name*，程序會尋找具有指定的資料表*fktable_name*資料庫擁有者所擁有。 如果資料表存在，就會傳回它的資料行。  
  
 [ @fktable_qualifier=] '*fktable_qualifier*'  
 這是資料表 (含外部索引鍵) 限定詞的名稱。 *fktable_qualifier*是**sysname**，預設值是 NULL。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這個限定詞代表資料庫名稱。 在某些產品中，它代表資料表之資料庫環境的伺服器名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 無  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
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
|UPDATE_RULE|**smallint**|當 SQL 作業是更新時，外部索引鍵所套用的動作。  可能的值如下：<br /> 0=外部索引鍵的 CASCADE 變更。<br /> 1=如果外部索引鍵存在，則是 NO ACTION 變更。<br />   2 = 設為 null <br /> 3 = 設為預設值 |  
|DELETE_RULE|**smallint**|當 SQL 作業是刪除時，外部索引鍵所套用的動作。 可能的值如下：<br /> 0=外部索引鍵的 CASCADE 變更。<br /> 1=如果外部索引鍵存在，則是 NO ACTION 變更。<br />   2 = 設為 null <br /> 3 = 設為預設值 |  
|FK_NAME|**sysname**|外部索引鍵識別碼。 如果不適用於資料來源的話，它便是 NULL。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回 FOREIGN KEY 條件約束名稱。|  
|PK_NAME|**sysname**|主索引鍵識別碼。 如果不適用於資料來源的話，它便是 NULL。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回 PRIMARY KEY 條件約束名稱。|  
  
 傳回的結果會依 FKTABLE_QUALIFIER、 FKTABLE_OWNER、 FKTABLE_NAME 和 KEY_SEQ 來排序。  
  
## <a name="remarks"></a>備註  
 您可以遵照下列步驟來實作含已停用之外部索引鍵之資料表的應用程式編碼：  
  
-   在使用資料表時，暫時停用條件約束檢查 (ALTER TABLE NOCHECK 或 CREATE TABLE NOT FOR REPLICATION)，稍後再重新啟用它。  
  
-   利用觸發程序或應用程式碼來強制實施關聯性。  
  
如果提供了主索引鍵資料表名稱，且外部索引鍵資料表名稱是 NULL，sp_fkeys 會傳回所有含有指向給定資料表的外部索引鍵之資料表。 如果提供了外部索引鍵資料表名稱，且主索引鍵資料表名稱是 NULL，sp_fkeys 會傳回所有透過主索引鍵/外部索引鍵關聯性來與外部索引鍵資料表中之外部索引鍵產生關聯的資料表。  
  
Sp_fkeys 預存程序就相當於 ODBC 中的 SQLForeignKeys。  
  
## <a name="permissions"></a>Permissions  
 需要`SELECT`結構描述權限。  
  
## <a name="examples"></a>範例  
 下列範例會擷取 `HumanResources.Department` 資料庫之 `AdventureWorks2012` 資料表的外部索引鍵清單。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_fkeys @pktable_name = N'Department'  
    ,@pktable_owner = N'HumanResources';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會擷取 `DimDate` 資料庫之 `AdventureWorksPDW2012` 資料表的外部索引鍵清單。 會傳回任何資料列，因為[!INCLUDE[ssDW](../../includes/ssdw-md.md)]不支援的外部索引鍵。  
  
```sql  
EXEC sp_fkeys @pktable_name = N'DimDate;  
```  
  
## <a name="see-also"></a>另請參閱  
 [目錄預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_pkeys &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-pkeys-transact-sql.md)  
  
  

