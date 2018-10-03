---
title: sp_unbindrule (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_unbindrule_TSQL
- sp_unbindrule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_unbindrule
ms.assetid: f54ee155-c3c9-4f1a-952e-632a8339f0cc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f35db2f08be985359de4723cdb9aa393ad608232
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47624158"
---
# <a name="spunbindrule-transact-sql"></a>sp_unbindrule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將規則和目前資料庫中的資料行或別名資料類型解除繫結。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] 我們建議您在使用中的 DEFAULT 關鍵字來建立 default 定義[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)或是[CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)陳述式改為。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_unbindrule [ @objname = ] 'object_name'   
     [ , [ @futureonly = ] 'futureonly_flag' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@objname=** ] **'***object_name***'**  
 這是規則將解除繫結的資料表和資料行或別名資料類型的名稱。 *object_name*已**nvarchar(776)**，沒有預設值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會試圖先將兩部分識別碼解析成資料行名稱，再解析成別名資料類型。 當您將規則和別名資料類型解除繫結時，也會解除繫結這個資料類型有相同規則的任何資料行。 直接繫結規則之資料類型的資料行不受影響。  
  
> [!NOTE]  
>  *object_name*可以包含方括號 **[]** 作為分隔識別碼字元。 如需詳細資訊，請參閱＜ [Database Identifiers](../../relational-databases/databases/database-identifiers.md)＞。  
  
 [ **@futureonly=** ] **'***futureonly_flag***'**  
 只有解除繫結別名資料類型的規則時，才使用這個項目。 *futureonly_flag*已**varchar(15)**，預設值是 NULL。 當*futureonly_flag*是**futureonly**，該資料類型的現有資料行不會失去指定的規則。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 若要顯示規則的文字，請將規則名稱設為參數來執行 **sp_helptext**。  
  
 規則解除繫結時，會從移除繫結的相關資訊**sys.columns**資料表，如果規則繫結至資料行，以及從**sys.types**資料表如果規則繫結到別名資料類型。  
  
 當您將規則和別名資料類型解除繫結時，也會解除繫結含這個別名資料類型的任何資料行。 規則也依然會繫結到資料行資料類型更新版本所變更的 ALTER TABLE 陳述式的 ALTER COLUMN 子句中，您必須明確解除繫結規則，這些資料行和使用**sp_unbindrule**並指定資料行名稱。  
  
## <a name="permissions"></a>Permissions  
 將規則和資料表資料行解除繫結，需要資料表的 ALTER 權限。 將規則和別名資料類型解除繫結，需要類型的 CONTROL 權限，或類型所屬之結構描述的 ALTER 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-unbinding-a-rule-from-a-column"></a>A. 將規則和資料行解除繫結  
 下列範例會將規則和 `startdate` 資料表的 `employees` 資料行解除繫結。  
  
```  
EXEC sp_unbindrule 'employees.startdate';  
```  
  
### <a name="b-unbinding-a-rule-from-an-alias-data-type"></a>B. 將規則和別名資料類型解除繫結  
 下列範例會將規則和別名資料類型 `ssn` 解除繫結。 它會將規則和這個類型的現有資料行及未來資料行解除繫結。  
  
```  
EXEC sp_unbindrule ssn;  
```  
  
### <a name="c-using-futureonlyflag"></a>C. 使用 futureonly_flag  
 下列範例會將規則和別名資料類型 `ssn` 解除繫結，且不會影響現有的 `ssn` 資料行。  
  
```  
EXEC sp_unbindrule 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. 使用分隔識別碼  
 下列範例示範中使用分隔的識別碼*object_name*參數。  
  
```  
CREATE TABLE [t.4] (c1 int); -- Notice the period as part of the table   
-- name.  
GO  
CREATE RULE rule2 AS @value > 100;  
GO  
EXEC sp_bindrule rule2, '[t.4].c1' -- The object contains two   
-- periods; the first is part of the table name and the second   
-- distinguishes the table name from the column name.  
GO  
EXEC sp_unbindrule '[t.4].c1';  
```  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Database Engine 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [DROP RULE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [sp_bindrule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
