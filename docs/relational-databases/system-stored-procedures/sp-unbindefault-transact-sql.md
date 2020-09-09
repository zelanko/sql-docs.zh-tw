---
description: sp_unbindefault (Transact-SQL)
title: sp_unbindefault (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_unbindefault_TSQL
- sp_unbindefault
dev_langs:
- TSQL
helpviewer_keywords:
- sp_unbindefault
ms.assetid: c96a6c5e-f3ca-4c1e-b64b-0d8ef6986af8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b8a0ee77c73c6edcee17d6baad363c6c02eb52c3
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542979"
---
# <a name="sp_unbindefault-transact-sql"></a>sp_unbindefault (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  將預設值和資料行或目前資料庫中之別名資料類型解除繫結，或移除其預設值。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] 我們建議您改為使用 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) 或 [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) 語句中的 default 關鍵字來建立預設定義。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_unbindefault [ @objname = ] 'object_name'   
     [ , [ @futureonly = ] 'futureonly_flag' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @objname = ] 'object_name'` 這是要解除系結之預設值的資料表和資料行名稱，或是別名資料類型。 *object_name* 是 **Nvarchar (776) **，沒有預設值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會試圖先將兩部分識別碼解析成資料行名稱，再解析成別名資料類型。  
  
 當您將預設值和別名資料類型解除繫結時，也會解除繫結這個資料類型有相同預設值的任何資料行。 直接繫結預設值之資料類型的資料行不受影響。  
  
> [!NOTE]  
>  *object_name* 可以包含方括弧 **[]** 做為分隔的識別碼字元。 如需詳細資訊，請參閱＜ [Database Identifiers](../../relational-databases/databases/database-identifiers.md)＞。  
  
`[ @futureonly = ] 'futureonly_flag'` 只有解除系結別名資料類型的預設值時才會使用。 *futureonly_flag* 是 **Varchar (15) **，預設值是 Null。 當 *futureonly_flag* 為 **futureonly**時，資料類型的現有資料行就不會遺失指定的預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 若要顯示預設值的文字，請執行 **sp_helptext** ，並以預設名稱做為參數。  
  
## <a name="permissions"></a>權限  
 將預設值和資料表資料行解除繫結，需要資料表的 ALTER 權限。 將預設值和別名資料類型解除繫結，需要類型的 CONTROL 權限，或類型所屬結構描述的 ALTER 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-unbinding-a-default-from-a-column"></a>A. 將預設值和資料行解除繫結  
 下列範例會將預設值和 `hiredate` 資料表的 `employees` 資料行解除繫結。  
  
```  
EXEC sp_unbindefault 'employees.hiredate';  
```  
  
### <a name="b-unbinding-a-default-from-an-alias-data-type"></a>B. 將預設值和別名資料類型解除繫結  
 下列範例會將預設值和別名資料類型 `ssn` 解除繫結。 它會將這個類型的現有和未來資料行解除繫結。  
  
```  
EXEC sp_unbindefault 'ssn';  
```  
  
### <a name="c-using-the-futureonly_flag"></a>C. 使用 futureonly_flag  
 下列範例會為別名資料類型 `ssn` 未來的使用解除繫結，且不會影響現有的 `ssn` 資料行。  
  
```  
EXEC sp_unbindefault 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. 使用分隔識別碼  
 下列範例示範如何在 *object_name* 參數中使用分隔識別碼。  
  
```  
CREATE TABLE [t.3] (c1 int); -- Notice the period as part of the table   
-- name.  
CREATE DEFAULT default2 AS 0;  
GO  
EXEC sp_bindefault 'default2', '[t.3].c1' ;  
-- The object contains two periods;  
-- the first is part of the table name and the second   
-- distinguishes the table name from the column name.  
EXEC sp_unbindefault '[t.3].c1';  
```  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [&#40;Transact-sql&#41;的資料庫引擎預存程式 ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [DROP DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [sp_bindefault &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
