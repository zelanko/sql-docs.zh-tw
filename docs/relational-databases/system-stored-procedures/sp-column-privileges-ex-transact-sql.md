---
title: sp_column_privileges_ex (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_column_privileges_ex
- sp_column_privileges_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_column_privileges_ex
ms.assetid: 98cb6e58-4007-40fc-b048-449fb2e7e6be
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0c31ae66112acc5cf1831573e436995c68c5d7ff
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="spcolumnprivilegesex-transact-sql"></a>sp_column_privileges_ex (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回指定連結伺服器之指定資料表的資料行權限。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_column_privileges_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]   
     [ , [ @column_name = ] 'column_name' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@table_server =** ] **'***table_server***'**  
 這是傳回的資訊所屬的連結伺服器名稱。 *table_server*是**sysname**，沒有預設值。  
  
 [  **@table_name =** ] **'***table_name***'**  
 這是包含指定之資料行的資料表名稱。 *table_name*是**sysname**，預設值是 NULL。  
  
 [  **@table_schema =** ] **'***table_schema***'**  
 這是資料表結構描述。 *table_schema*是**sysname**，預設值是 NULL。  
  
 [  **@table_catalog =** ] **'***table_catalog 排列***'**  
 在其中的資料庫名稱指定*table_name*所在。 *table_catalog 排列*是**sysname**，預設值是 NULL。  
  
 [  **@column_name =** ] **'***column_name***'**  
 這是提供的權限資訊所屬的資料行名稱。 *column_name*是**sysname**，預設值是 NULL （所有資料行）。  
  
## <a name="result-sets"></a>結果集  
 下表會顯示結果集資料行。 傳回的結果會依照**TABLE_QUALIFIER**， **TABLE_OWNER**， **TABLE_NAME**， **COLUMN_NAME**，和**權限**。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|資料表限定詞名稱。 各種 DBMS 產品都支援三部分的資料表命名 (*限定詞***。***擁有者***。***名稱*)。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，這個資料行代表資料庫名稱。 在某些產品中，它代表資料表之資料庫環境的伺服器名稱。 這個欄位可以是 NULL。|  
|**再依據 TABLE_SCHEM 排列**|**sysname**|資料表擁有者名稱。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這個資料行代表建立資料表的資料庫使用者名稱。 這個欄位一律會傳回值。|  
|**TABLE_NAME**|**sysname**|資料表名稱。 這個欄位一律會傳回值。|  
|**COLUMN_NAME**|**sysname**|每個資料行的資料行名稱**TABLE_NAME**傳回。 這個欄位一律會傳回值。|  
|**授與者**|**sysname**|已授與此權限的資料庫使用者名稱**COLUMN_NAME**與列出**被授與者**。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，此資料行一律是相同**TABLE_OWNER**。 這個欄位一律會傳回值。<br /><br /> **授與者**資料行可以是資料庫擁有者 (**TABLE_OWNER**) 或其他人對資料庫擁有者授與權限的 GRANT 陳述式中使用 WITH GRANT OPTION 子句。|  
|**被授與者**|**sysname**|已授與此權限的資料庫使用者名稱**COLUMN_NAME**列出的**授與者**。 這個欄位一律會傳回值。|  
|**權限**|**varchar(**32**)**|可用的資料行權限之一。 資料行權限可以是下列值之一 (或定義實作時，資料來源所支援的其他值)：<br /><br /> 選取 =**被授與者**可以擷取資料行的資料。<br /><br /> INSERT =**被授與者**插入新資料列時，可以提供資料給這個資料行 (由**被授與者**) 到資料表。<br /><br /> UPDATE =**被授與者**可以修改資料行中的現有資料。<br /><br /> 參考 =**被授與者**可以參考外部資料表中主索引鍵/外部索引鍵關聯性中的資料行。 主索引鍵/外部索引鍵關聯性是利用資料表條件約束來定義的。|  
|**IS_GRANTABLE**|**varchar (**3**)**|指出是否**被授與者**允許權限授與其他使用者 （通常稱為"grant with grant"權限）。 它可以是 YES、NO 或 NULL。 未知 (或 NULL) 值是指不適用 "grant with grant" 的資料來源。|  
  
## <a name="permissions"></a>Permissions  
 需要結構描述的 SELECT 權限。  
  
## <a name="examples"></a>範例  
 下列範例會從 `HumanResources.Department` 連結伺服器的 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫之 `Seattle1` 資料表中，傳回資料行權限資訊。  
  
```  
EXEC sp_column_privileges_ex @table_server = 'Seattle1',   
   @table_name = 'Department',   
   @table_schema = 'HumanResources',  
   @table_catalog ='AdventureWorks2012';  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_table_privileges_ex &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-ex-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
