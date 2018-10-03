---
title: sp_table_privileges_ex (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_table_privileges_ex
- sp_table_privileges_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_table_privileges_ex
ms.assetid: b58d4a07-5c40-4f17-b66e-6d6b17188dda
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d800eed984c6371ed689e9d8ec2748cb6b9886c1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47752748"
---
# <a name="sptableprivilegesex-transact-sql"></a>sp_table_privileges_ex (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回指定連結伺服器中之指定資料表的權限相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_table_privileges_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]  
     [ , [@fUsePattern =] 'fUsePattern']  
```  
  
## <a name="arguments"></a>引數  
 [  **@table_server =** ] **'***table_server&lt***'**  
 這是傳回的資訊所屬的連結伺服器名稱。 *table_server&lt*已**sysname**，沒有預設值。  
  
 [  **@table_name =** ] **'***table_name***'**]  
 這是提供的資料表權限資訊所屬的資料表名稱。 *table_name*已**sysname**，預設值是 NULL。  
  
 [  **@table_schema =** ] **'***table_schema***'**  
 這是資料表結構描述。 在某些 DBMS 環境中，這是資料表擁有者。 *table_schema*已**sysname**，預設值是 NULL。  
  
 [  **@table_catalog =** ] **'***table_catalog 排列***'**  
 在其中的資料庫名稱指定*table_name*所在。 *table_catalog 排列*已**sysname**，預設值是 NULL。  
  
 [  **@fUsePattern =**] **'***fUsePattern***'**  
 判斷是否將 '_'、'%'、'[' 和 ']' 等字元解譯為萬用字元。 有效值是 0 (關閉模式比對) 和 1 (開啟模式比對)。 *fUsePattern*已**元**，預設值是 1。  
  
## <a name="return-code-values"></a>傳回碼值  
 None  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|資料表限定詞名稱。 各種 DBMS 產品都支援三部分的資料表命名 (*限定詞 ***。*** 擁有者 ***。*** 名稱*)。 在  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，這個資料行代表資料庫名稱。 在某些產品中，它代表資料表之資料庫環境的伺服器名稱。 這個欄位可以是 NULL。|  
|**再依據 TABLE_SCHEM 排列**|**sysname**|資料表擁有者名稱。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這個資料行代表建立資料表的資料庫使用者名稱。 這個欄位一律會傳回值。|  
|**TABLE_NAME**|**sysname**|資料表名稱。 這個欄位一律會傳回值。|  
|**同意授權者**|**sysname**|已授與此權限的資料庫使用者名稱**TABLE_NAME**與列出**被授與者**。 在  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，此資料行一律是相同**TABLE_OWNER**。 這個欄位一律會傳回值。 另外，GRANTOR 資料行可能是資料庫擁有者 (**TABLE_OWNER**) 或使用者對象的資料庫擁有者授與權限的 GRANT 陳述式中使用 WITH GRANT OPTION 子句。|  
|**被授與者**|**sysname**|已授與此權限的資料庫使用者名稱**TABLE_NAME**依列出**授與者**。 這個欄位一律會傳回值。|  
|**權限**|**varchar(** 32 **)**|可用的資料表權限之一。 資料表權限可以是下列值之一，或定義實作時，資料來源所支援的其他值：<br /><br /> 選取 =**被授與者**可以擷取一個或多個資料行的資料。<br /><br /> INSERT =**被授與者**可以提供資料的新資料列的一個或多個資料行。<br /><br /> UPDATE =**被授與者**可以修改現有資料的一個或多個資料行。<br /><br /> 刪除 =**被授與者**可以從資料表移除資料列。<br /><br /> 參考 =**被授與者**可以參考外部資料表中主索引鍵/外部索引鍵關聯性中的資料行。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，主索引鍵/外部索引鍵關聯性是利用資料表條件約束來定義的。<br /><br /> 提供給動作的範圍**被授與者**特定資料表權限是資料來源而定。 例如，UPDATE 權限可能會讓**被授與者**更新其中一個資料來源上的資料表中的所有資料行和這些資料行**授與者**另一個資料來源有 UPDATE 權限。|  
|**IS_GRANTABLE**|**varchar (** 3 **)**|指出是否**被授與者**允許其他使用者授與權限。 這通常稱為 "grant with grant" 權限。 它可以是 YES、NO 或 NULL。 未知 (或 NULL) 值是指不適用 "grant with grant" 的資料來源。|  
  
## <a name="remarks"></a>備註  
 傳回的結果都會按照**TABLE_QUALIFIER**， **TABLE_OWNER**， **TABLE_NAME**，以及**權限**。  
  
## <a name="permissions"></a>Permissions  
 需要結構描述的 SELECT 權限。  
  
## <a name="examples"></a>範例  
 下列範例會從指定連結伺服器 `Product` 中，傳回 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中名稱開頭為 `Seattle1` 的資料表之權限資訊  (假設 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是連結伺服器)。  
  
```  
EXEC sp_table_privileges_ex @table_server = 'Seattle1',   
   @table_name = 'Product%',   
   @table_schema = 'Production',  
   @table_catalog ='AdventureWorks2012';  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_column_privileges_ex &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-ex-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [分散式查詢預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)  
  
  
