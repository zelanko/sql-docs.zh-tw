---
title: sp_unbindefault (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_unbindefault_TSQL
- sp_unbindefault
dev_langs:
- TSQL
helpviewer_keywords:
- sp_unbindefault
ms.assetid: c96a6c5e-f3ca-4c1e-b64b-0d8ef6986af8
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 80453657de70133f269b35387813389ecb7cff0a
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33262316"
---
# <a name="spunbindefault-transact-sql"></a>sp_unbindefault (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將預設值和資料行或目前資料庫中之別名資料類型解除繫結，或移除其預設值。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] 我們建議您在使用中的 DEFAULT 關鍵字來建立預設定義[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)或[CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)陳述式改為。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_unbindefault [ @objname = ] 'object_name'   
     [ , [ @futureonly = ] 'futureonly_flag' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@objname=** ] **'***object_name***'**  
 這是預設值將解除繫結的資料表和資料行或別名資料類型的名稱。 *object_name*是**nvarchar(776)**，沒有預設值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會試圖先將兩部分識別碼解析成資料行名稱，再解析成別名資料類型。  
  
 當您將預設值和別名資料類型解除繫結時，也會解除繫結這個資料類型有相同預設值的任何資料行。 直接繫結預設值之資料類型的資料行不受影響。  
  
> [!NOTE]  
>  *object_name*可以包含方括號 **[]** 作為分隔識別碼字元。 如需詳細資訊，請參閱＜ [Database Identifiers](../../relational-databases/databases/database-identifiers.md)＞。  
  
 [ **@futureonly=** ] **'***futureonly_flag***'**  
 只有解除繫結別名資料類型的預設值時，才使用這個項目。 *futureonly_flag*是**varchar(15)**，預設值是 NULL。 當*futureonly_flag*是**futureonly**，現有的資料類型資料行不會失去指定的預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 若要顯示的預設值的文字，請執行**sp_helptext**做為參數的預設名稱。  
  
## <a name="permissions"></a>Permissions  
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
  
### <a name="c-using-the-futureonlyflag"></a>C. 使用 futureonly_flag  
 下列範例會為別名資料類型 `ssn` 未來的使用解除繫結，且不會影響現有的 `ssn` 資料行。  
  
```  
EXEC sp_unbindefault 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. 使用分隔識別碼  
 下列範例示範如何使用分隔的識別碼中*object_name*參數。  
  
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
 [Database Engine 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [DROP DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [sp_bindefault &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
