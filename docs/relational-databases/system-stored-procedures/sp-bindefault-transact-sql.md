---
title: sp_bindefault （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 11/25/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 918f545dd0ea0ca30524a307f1ae6d30c3fafb61
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68046051"
---
# <a name="sp_bindefault-transact-sql"></a>sp_bindefault (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  將預設值繫結到資料行或別名資料類型。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]我們建議您改為使用[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)或[CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)語句的 default 關鍵字來建立預設定義。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_bindefault [ @defname = ] 'default' ,   
    [ @objname = ] 'object_name'   
    [ , [ @futureonly = ] 'futureonly_flag' ]   
```  
  
## <a name="arguments"></a>引數  
`[ @defname = ] 'default'`這是 CREATE DEFAULT 所建立之預設值的名稱。 *預設值*為**Nvarchar （776）**，沒有預設值。  
  
`[ @objname = ] 'object_name'`這是要系結預設值的資料表和資料行名稱，或是別名資料類型。 *object_name*是**Nvarchar （776）** ，沒有預設值。 無法使用**Varchar （max）**、 **Nvarchar （max）**、 **Varbinary （MAX）**、 **xml**或 CLR 使用者定義型別來定義*object_name* 。  
  
 如果*object_name*是一個部分的名稱，它會解析為別名資料類型。 如果它是兩部份或三部份的名稱，就會先將它解析成資料表和資料行；如果這項解析失敗，就會將它解析成別名資料類型。 根據預設，除非已直接將預設值系結到資料行，否則，別名資料類型的現有資料行會繼承*default*。 Default 無法系結到**text**、 **Ntext**、 **image**、 **Varchar （max）**、 **Nvarchar （max）**、 **Varbinary （max）**、 **XML**、 **timestamp**或 CLR 使用者自訂類型資料行、具有識別屬性的資料行、計算資料行或已經有 default 條件約束的資料行。  
  
> [!NOTE]  
>  *object_name*可以包含方括弧 **[]** 做為分隔識別碼。 如需詳細資訊，請參閱＜ [Database Identifiers](../../relational-databases/databases/database-identifiers.md)＞。  
  
`[ @futureonly = ] 'futureonly_flag'`只有在將預設值系結到別名資料類型時，才會使用。 *futureonly_flag*是**Varchar （15）** ，預設值是 Null。 當這個參數設定為**futureonly**時，該資料類型的現有資料行就無法繼承新的預設值。 當預設值繫結到資料行時，永遠不會使用這個參數。 如果*futureonly_flag*是 Null，新的預設值會系結至目前沒有預設值或使用別名資料類型之現有預設值的別名資料類型的任何資料行。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 您可以使用**sp_bindefault** ，將新的預設條件約束系結至資料行，不過，使用預設條件約束是慣用的，或不會解除系結現有預設值的別名資料類型。 此時會覆寫舊的預設值。 您不能將預設值繫結到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料類型或 CLR 使用者自訂類型。 如果預設值與所繫結的資料行不相容，當它嘗試插入預設值時，而不是當您試圖繫結它時，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 會傳回一則錯誤訊息。  
  
 除非預設值直接系結至它們，或*futureonly_flag*指定為**futureonly**，否則，別名資料類型的現有資料行會繼承新的預設值。 別名資料類型的新資料行一律會繼承預設值。  
  
 當您將預設值系結至資料行時，會將相關資訊加入至**sys.databases**目錄檢視。 當您將預設值系結到別名資料類型時，會將相關資訊加入至**sys.databases**目錄檢視。  
  
## <a name="permissions"></a>權限  
 使用者必須擁有資料表，或是**系統管理員（sysadmin** ）固定伺服器角色的成員，或是**db_owner**和**db_ddladmin**固定資料庫角色。  
  
## <a name="examples"></a>範例  
  
### <a name="a-binding-a-default-to-a-column"></a>A. 將預設值繫結到資料行  
 已利用 CREATE RULE 陳述式，在目前資料庫中定義名稱為 `today` 的預設值，下列範例會將預設值繫結到 `HireDate` 資料表的 `Employee` 資料行。 每當將資料列加入 `Employee` 資料表，且未提供 `HireDate` 資料行的資料時，資料行都會取得 `today` 預設值的值。  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'today', 'HumanResources.Employee.HireDate';  
```  
  
### <a name="b-binding-a-default-to-an-alias-data-type"></a>B. 將預設值繫結到別名資料類型  
 名稱為 `def_ssn` 的預設值和名稱為 `ssn` 的別名資料類型已經存在。 下列範例會將 `def_ssn` 預設值繫結到 `ssn`。 當建立資料表時，所有指派了別名資料類型 `ssn` 的資料行都會繼承預設值。 除非已針對*futureonly_flag*值指定**futureonly** ，或除非資料行直接系結到它的預設值，**否則類型的**現有資料行也會繼承預設**def_ssn**。 繫結到資料行的預設值，一律優先於繫結到資料類型的預設值。  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'def_ssn', 'ssn';  
```  
  
### <a name="c-using-the-futureonly_flag"></a>C. 使用 futureonly_flag  
 下列範例將 `def_ssn` 預設值繫結到別名資料類型 `ssn`。 因為已指定**futureonly** ，所以不會影響任何`ssn`類型的現有資料行。  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'def_ssn', 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. 使用分隔識別碼  
 下列範例會示範如何在*object_name*中`[t.1]`使用分隔識別碼。  
  
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
 [資料庫引擎預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [DROP DEFAULT &#40;Transact-sql&#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [sp_unbindefault &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
