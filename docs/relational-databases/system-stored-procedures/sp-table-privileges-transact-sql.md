---
title: sp_table_privileges (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_table_privileges
- sp_table_privileges_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_table_privileges
ms.assetid: 0512e688-4fc0-4557-8dc8-016672c1e3fe
author: stevestein
ms.author: sstein
ms.openlocfilehash: 14e532d76f70f6a2d4fa623d80fa02e6c756348a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096138"
---
# <a name="sptableprivileges-transact-sql"></a>sp_table_privileges (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回一或多份指定資料表的資料表權限清單 (如 INSERT、DELETE、UPDATE、SELECT、REFERENCES)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_table_privileges [ @table_name = ] 'table_name'     
     [ , [ @table_owner = ] 'table_owner' ]   
     [ , [ @table_qualifier = ] 'table_qualifier' ]   
     [ , [ @fUsePattern = ] 'fUsePattern' ]  
```  
  
## <a name="arguments"></a>引數  
 [ @table_name= ] '*table_name*'  
 這是用來傳回目錄資訊的資料表。 *table_name*已**nvarchar (** 384 **)** ，沒有預設值。 支援萬用字元的模式比對。  
  
 [ @table_owner= ] '*table_owner*'  
 這是用來傳回目錄資訊之資料表的資料表擁有者。 *table_owner*已**nvarchar (** 384 **)** ，預設值是 NULL。 支援萬用字元的模式比對。 如果未指定擁有者，就會套用基礎 DBMS 的預設資料表可見性規則。  
  
 如果目前使用者擁有一份含指定名稱的資料表，就會傳回該資料表的資料行。 如果*擁有者*未指定且目前使用者並未擁有指定的資料表*名稱*，此程序會尋找具有指定的資料表*table_name*所擁有資料庫擁有者。 如果資料表存在，就會傳回這份資料表的資料行。  
  
 [ @table_qualifier=] '*table_qualifier*'  
 這是資料表限定詞的名稱。 *table_qualifier*已**sysname**，預設值是 NULL。 各種 DBMS 產品都支援三部分的資料表命名 (*qualifier.owner.name*)。 在  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，這個資料行代表資料庫名稱。 在某些產品中，它代表資料表之資料庫環境的伺服器名稱。  
  
 [ @fUsePattern= ] '*fUsePattern*'  
 判斷是否會將底線 (_)、 百分比 （%） 和括號 （[或]） 字元解譯成萬用字元。 有效值是 0 (關閉模式比對) 和 1 (開啟模式比對)。 *fUsePattern*已**元**，預設值是 1。  
  
## <a name="return-code-values"></a>傳回碼值  
 None  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|TABLE_QUALIFIER|**sysname**|資料表限定詞名稱。 在  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，這個資料行代表資料庫名稱。 這個欄位可以是 NULL。|  
|TABLE_OWNER|**sysname**|資料表擁有者名稱。 這個欄位一律會傳回值。|  
|TABLE_NAME|**sysname**|資料表名稱。 這個欄位一律會傳回值。|  
|GRANTOR|**sysname**|已將這份 TABLE_NAME 的權限授與列出之 GRANTEE 的資料庫使用者名稱。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這個資料行一律與 TABLE_OWNER 相同。 這個欄位一律會傳回值。 另外，GRANTOR 資料行也可能是資料庫擁有者 (TABLE_OWNER)，或資料庫擁有者利用 GRANT 陳述式中之 WITH GRANT OPTION 子句來授與權限的使用者。|  
|GRANTEE|**sysname**|列出的 GRANTOR 已授與這份 TABLE_NAME 的權限之資料庫使用者名稱。 在  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，這個資料行一律包括 sys.database_principalssystem 檢視的資料庫使用者。 這個欄位一律會傳回值。|  
|PRIVILEGE|**sysname**|可用的資料表權限之一。 資料表權限可以是下列值之一 (或定義實作時，資料來源所支援的其他值)：<br /><br /> SELECT = GRANTEE 可以擷取一個或多個資料行的資料。<br /><br /> INSERT = GRANTEE 可以提供一個或多個資料行的新資料列資料。<br /><br /> UPDATE = GRANTEE 可以修改一個或多個資料行的現有資料。<br /><br /> DELETE = GRANTEE 可以移除資料表中的資料列。<br /><br /> REFERENCES = GRANTEE 可以在主索引鍵/外部索引鍵關聯性中，參考外部資料表中的資料行。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，主索引鍵/外部索引鍵關聯性是利用資料表條件約束來定義的。<br /><br /> 特定資料表權限提供給 GRANTEE 的動作範圍會隨著資料來源而不同。 例如，UPDATE 權限可能會允許 GRANTEE 更新一項資料來源中某份資料表的所有資料行，但只更新另一項資料來源中 GRANTOR 有 UPDATE 權限的資料行。|  
|IS_GRANTABLE|**sysname**|指出是否允許 GRANTEE 將權限授與其他使用者 (通常稱為 "grant with grant" 權限)。 它可以是 YES、NO 或 NULL。 未知 (或 NULL) 值是指不適用 "grant with grant" 的資料來源。|  
  
## <a name="remarks"></a>備註  
 sp_table_privileges 預存程序相當於 ODBC 中的 SQLTablePrivileges。 傳回的結果依 TABLE_QUALIFIER、TABLE_OWNER、TABLE_NAME 和 PRIVILEGE 來排序。  
  
## <a name="permissions"></a>Permissions  
 需要結構描述的 SELECT 權限。  
  
## <a name="examples"></a>範例  
 下列範例會傳回名稱開頭為 `Contact` 一字的所有資料表之權限資訊。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_table_privileges   
   @table_name = 'Contact%';  
```  
  
## <a name="see-also"></a>另請參閱  
 [目錄預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
