---
title: "DBCC CHECKIDENT (TRANSACT-SQL) |Microsoft 文件"
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
caps.latest.revision: 63
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d81aa2c26cf693d8ed5613c2aceb970a54db5aca
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-checkident-transact-sql"></a>DBCC CHECKIDENT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中檢查指定之資料表目前的識別值，必要的話，會變更識別值。 您也可以使用 DBCC CHECKIDENT，手動設定識別欄位的新目前識別值。  
   
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
DBCC CHECKIDENT   
 (   
    table_name  
        [, { NORESEED | { RESEED [, new_reseed_value ] } } ]  
)  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>引數  
 *table_name*  
 這是要檢查目前識別值之資料表的名稱。 指定的資料表必須包含識別欄位。 資料表名稱必須遵守的規則[識別碼](../../relational-databases/databases/database-identifiers.md)。 兩個或三個部分的名稱必須加以分隔，例如 'Person.AddressType' 或 [Person.AddressType]。   
  
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
|DBCC CHECKIDENT ( *table_name*，NORESEED)|不重設目前的識別值。 DBCC CHECKIDENT 會傳回識別欄位目前的識別值和最大值。 如果這兩個值不同，則應該重設識別值以防止值序列中發生錯誤或間距。|  
|DBCC CHECKIDENT ( *table_name* )<br /><br /> 或<br /><br /> DBCC CHECKIDENT ( *table_name*，重設種子資料)|如果資料表目前的識別值小於識別欄位所儲存的最大識別值，就會利用識別欄位中的最大值來重設它。 請參閱稍後的＜例外＞一節。|  
|DBCC CHECKIDENT ( *table_name*，RESEED， *new_reseed_value* )|目前識別值設定為*new_reseed_value*。 如果任何資料列有被不插入至資料表，因為已建立資料表，或者如果已經使用 TRUNCATE TABLE 陳述式來移除所有資料列，插入執行 DBCC CHECKIDENT 之後的第一個資料列會使用*new_reseed_value*作為身分識別。<br /><br /> 如果資料列會存在資料表中下, 一個資料列會插入與*new_reseed_value*值。 在版本[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]和更早版本，會使用下一個資料列插入*new_reseed_value* +[目前增量](../../t-sql/functions/ident-incr-transact-sql.md)值。<br /><br /> 如果資料表不是空的，則將識別值設定為小於識別欄位中最大值的數字，可能會導致下列其中一種狀況：<br /><br /> -如果 PRIMARY KEY 或 UNIQUE 條件約束存在的識別欄位，錯誤訊息 2627年會產生更新插入資料表的插入作業，因為產生的識別值會與現有的值發生衝突。<br /><br /> -如果 PRIMARY KEY 或 UNIQUE 條件約束不存在，後續的插入作業會導致重複的識別值。|  
  
## <a name="exceptions"></a>例外狀況  
 下表列出 DBCC CHECKIDENT 不會自動重設目前識別值的條件，並提供重設值的方法。  
  
|條件|重設方法|  
|---------------|-------------------|  
|目前的識別值大於資料表中的最大值。|執行 DBCC CHECKIDENT (*table_name*，NORESEED) 來判斷資料行中的目前最大值，然後指定 該值為*new_reseed_value*在 DBCC checkident (*table_名稱*，RESEED，*new_reseed_value*) 命令。<br /><br /> -或-<br /><br /> 執行 DBCC CHECKIDENT (*table_name*，RESEED，*new_reseed_value*) 與*new_reseed_value*設為非常低的值，然後再執行 DBCC CHECKIDENT (*table_name*，RESEED) 來更正此值。|  
|資料表中的所有資料列都遭到刪除。|執行 DBCC CHECKIDENT (*table_name*，RESEED，*new_reseed_value*) 與*new_reseed_value*設定為所需的起始值。|  
  
## <a name="changing-the-seed-value"></a>變更初始值  
 初始值就是針對載入資料表中的第一個資料列插入識別欄位的值。 所有後續資料列都會包含目前的識別值加上遞增值，其中目前的識別值就是針對資料表或檢視表所產生的最後一個識別值。  
  
 您無法使用 DBCC CHECKIDENT 來執行下列工作：  
  
-   變更建立資料表或檢視表時針對識別欄位所指定的原始初始值。  
  
-   重設資料表或檢視表中現有的資料列。  
  
 若要變更原始的初始值並重設任何現有的資料列，您必須卸除識別欄位並指定新的初始值來重建此識別欄位。 當資料表包含資料時，識別數字就會加入至含有指定初始值和遞增值的現有資料列。 但是，無法保證資料列的更新順序。  
  
## <a name="result-sets"></a>結果集  
 不論是否針對包含識別欄位的資料表指定任何選項，DBCC CHECKIDENT 都會針對所有作業傳回下列訊息 (只指定新的初始值時例外)。  
  
`Checking identity information: current identity value '\<current identity value>', current column value '\<current column value>'. DBCC execution completed. If DBCC printed error messages, contact your system administrator.`
  
 當 DBCC CHECKIDENT 來透過 RESEED 指定新的初始值*new_reseed_value*，會傳回下列訊息。  
  
`Checking identity information: current identity value '\<current identity value>'. DBCC execution completed. If DBCC printed error messages, contact your system administrator.`
  
## <a name="permissions"></a>Permissions  
 呼叫端必須擁有包含資料表的結構描述，或必須屬於**sysadmin**固定伺服器角色、 **db_owner**固定資料庫角色或**db_ddladmin**固定資料庫角色。  
  
## <a name="examples"></a>範例  
  
### <a name="a-resetting-the-current-identity-value-if-it-is-needed"></a>A. 必要的話，重設目前的識別值  
 在必要時，下列範例會重設 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中指定之資料表目前的識別值。  
  
```  
USE AdventureWorks2012;  
GO  
DBCC CHECKIDENT ('Person.AddressType');  
GO  
```  
  
### <a name="b-reporting-the-current-identity-value"></a>B. 報告目前的識別值  
 下列範例會報告 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中指定之資料表目前的識別值，如果識別值不正確，並不會更正它。  
  
```  
USE AdventureWorks2012;   
GO  
DBCC CHECKIDENT ('Person.AddressType', NORESEED);   
GO  
  
```  
  
### <a name="c-forcing-the-current-identity-value-to-a-new-value"></a>C. 將目前識別值強制設為新的值  
 下列範例會強制將 `AddressTypeID` 資料表中 `AddressType` 資料行內的目前識別值設定為 10。 因為資料表目前有資料列，所以下一個插入的資料列將會使用 11 的值，也就是針對資料行值定義的目前增量值加 1。  
  
```  
USE AdventureWorks2012;  
GO  
DBCC CHECKIDENT ('Person.AddressType', RESEED, 10);  
GO  
  
```  
  
## <a name="see-also"></a>另請參閱  
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[IDENTITY &#40;屬性&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)  
[複寫識別欄位](../../relational-databases/replication/publish/replicate-identity-columns.md)  
[USE &#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)  
[IDENT_SEED &#40;TRANSACT-SQL &#41;](../../t-sql/functions/ident-seed-transact-sql.md)  
[IDENT_INCR &#40;TRANSACT-SQL &#41;](../../t-sql/functions/ident-incr-transact-sql.md)  
  
  

