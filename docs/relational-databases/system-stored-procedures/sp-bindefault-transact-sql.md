---
title: sp_bindefault (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 11/25/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_bindefault
- sp_bindefault_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_bindefault
ms.assetid: 3da70c10-68d0-4c16-94a5-9e84c4a520f6
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 69f008794756176c3046985e17d6263cf7979278
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43062829"
---
# <a name="spbindefault-transact-sql"></a>sp_bindefault (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  將預設值繫結到資料行或別名資料類型。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 我們建議您在使用 DEFAULT 關鍵字來建立 default 定義[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)或是[CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)陳述式改為。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_bindefault [ @defname = ] 'default' ,   
    [ @objname = ] 'object_name'   
    [ , [ @futureonly = ] 'futureonly_flag' ]   
```  
  
## <a name="arguments"></a>引數  
 [ **@defname=** ] **'***default***'**  
 這是 CREATE DEFAULT 所建立之預設值的名稱。 *預設值*已**nvarchar(776)**，沒有預設值。  
  
 [ **@objname=** ] **'***object_name***'**  
 這是預設值將要繫結之資料表和資料行的名稱，或是別名資料類型。 *object_name*已**nvarchar(776)** 沒有預設值。 *object_name*能以定義**varchar （max)**， **nvarchar （max)**， **varbinary （max)**， **xml**，或 CLR使用者定義型別。  
  
 如果*object_name*是單部分名稱，它會解析成別名資料類型。 如果它是兩部份或三部份的名稱，就會先將它解析成資料表和資料行；如果這項解析失敗，就會將它解析成別名資料類型。 根據預設，現有的資料行別名資料類型的繼承*預設*，除非您已繫結直接到資料行的預設值。 無法繫結至的預設值**文字**， **ntext**，**映像**， **varchar （max)**， **nvarchar （max)**，**varbinary （max)**， **xml**，**時間戳記**，或 CLR 使用者自訂類型資料行、 具有 IDENTITY 屬性的資料行、 計算資料行或資料行，已經有預設條件約束。  
  
> [!NOTE]  
>  *object_name*可以包含方括號 **[]** 作為分隔識別碼。 如需詳細資訊，請參閱＜ [Database Identifiers](../../relational-databases/databases/database-identifiers.md)＞。  
  
 [ **@futureonly=** ] **'***futureonly_flag***'**  
 只有將預設值繫結到別名資料類型時，才會使用這個項目。 *futureonly_flag*已**varchar(15)** 預設值是 NULL。 當此參數設定為**futureonly**，現有的資料行，該資料類型無法繼承新的預設值。 當預設值繫結到資料行時，永遠不會使用這個參數。 如果*futureonly_flag*是 NULL，新的預設值繫結至任何資料行的別名資料類型，目前有沒有預設值，或使用現有的別名資料類型的預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 您可以使用**sp_bindefault** ，繫結新的預設值的資料行中，雖然使用預設條件約束是慣用的或別名資料類型而不需要現有的預設值解除繫結。 此時會覆寫舊的預設值。 您不能將預設值繫結到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料類型或 CLR 使用者自訂類型。 如果預設值與所繫結的資料行不相容，當它嘗試插入預設值時，而不是當您試圖繫結它時，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 會傳回一則錯誤訊息。  
  
 別名資料類型的現有資料行會繼承新的預設值，除非預設值直接繫結或*futureonly_flag*指定為**futureonly**。 別名資料類型的新資料行一律會繼承預設值。  
  
 當您將預設值繫結至資料行時，相關的資訊會新增至**sys.columns**目錄檢視。 當您將預設值繫結到別名資料類型時，相關的資訊會新增至**sys.types**目錄檢視。  
  
## <a name="permissions"></a>Permissions  
 使用者必須擁有資料表，或隸屬**sysadmin**固定伺服器角色，或有**db_owner**並**db_ddladmin**固定資料庫角色。  
  
## <a name="examples"></a>範例  
  
### <a name="a-binding-a-default-to-a-column"></a>A. 將預設值繫結到資料行  
 已利用 CREATE RULE 陳述式，在目前資料庫中定義名稱為 `today` 的預設值，下列範例會將預設值繫結到 `HireDate` 資料表的 `Employee` 資料行。 每當將資料列加入 `Employee` 資料表，且未提供 `HireDate` 資料行的資料時，資料行都會取得 `today` 預設值的值。  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'today', 'HumanResources.Employee.HireDate';  
```  
  
### <a name="b-binding-a-default-to-an-alias-data-type"></a>B. 將預設值繫結到別名資料類型  
 名稱為 `def_ssn` 的預設值和名稱為 `ssn` 的別名資料類型已經存在。 下列範例會將 `def_ssn` 預設值繫結到 `ssn`。 當建立資料表時，所有指派了別名資料類型 `ssn` 的資料行都會繼承預設值。 類型的現有資料行**ssn**也會繼承預設值**futureonly_flag**，除非**futureonly**指定為*futureonly_flag*值，或者，除非資料行有直接繫結預設值。 繫結到資料行的預設值，一律優先於繫結到資料類型的預設值。  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'def_ssn', 'ssn';  
```  
  
### <a name="c-using-the-futureonlyflag"></a>C. 使用 futureonly_flag  
 下列範例將 `def_ssn` 預設值繫結到別名資料類型 `ssn`。 因為**futureonly**會指定類型的任何現有資料行`ssn`會受到影響。  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'def_ssn', 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. 使用分隔識別碼  
 下列範例示範使用分隔的識別碼`[t.1]`，請在*object_name*。  
  
```  
USE master;  
GO  
CREATE TABLE [t.1] (c1 int);   
-- Notice the period as part of the table name.  
EXEC sp_bindefault 'default1', '[t.1].c1' ;  
-- The object contains two periods;   
-- the first is part of the table name,   
-- and the second distinguishes the table name from the column name.  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [DROP DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [sp_unbindefault &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
