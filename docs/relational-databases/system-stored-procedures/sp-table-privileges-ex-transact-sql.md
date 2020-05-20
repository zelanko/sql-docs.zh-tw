---
title: sp_table_privileges_ex （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ab1630f6dd172410d26f48d0485b23d257c6d408
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82825979"
---
# <a name="sp_table_privileges_ex-transact-sql"></a>sp_table_privileges_ex (Transact-SQL)
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
`[ @table_server = ] 'table_server'`這是要傳回信息的連結伺服器名稱。 *table_server*是**sysname**，沒有預設值。  
  
`[ @table_name = ] 'table_name']`這是要提供資料表許可權資訊的資料表名稱。 *table_name*是**sysname**，預設值是 Null。  
  
`[ @table_schema = ] 'table_schema'`這是資料表架構。 在某些 DBMS 環境中，這是資料表擁有者。 *table_schema*是**sysname**，預設值是 Null。  
  
`[ @table_catalog = ] 'table_catalog'`這是指定之*table_name*所在的資料庫名稱。 *table_catalog*是**sysname**，預設值是 Null。  
  
`[ @fUsePattern = ] 'fUsePattern'`判斷字元 ' _ '、'% '、' [' 和 '] ' 是否會解讀為萬用字元。 有效值是 0 (關閉模式比對) 和 1 (開啟模式比對)。 *fUsePattern*是**bit**，預設值是1。  
  
## <a name="return-code-values"></a>傳回碼值  
 無  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|資料表限定詞名稱。 各種 DBMS 產品都支援三部分的資料表命名（辨識_符號_**。**_擁有_者 **。**_名稱_）。 在中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，這個資料行代表資料庫名稱。 在某些產品中，它代表資料表之資料庫環境的伺服器名稱。 這個欄位可以是 NULL。|  
|**TABLE_SCHEM**|**sysname**|資料表擁有者名稱。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這個資料行代表建立資料表的資料庫使用者名稱。 這個欄位一律會傳回值。|  
|**TABLE_NAME**|**sysname**|資料表名稱。 這個欄位一律會傳回值。|  
|**授權**|**sysname**|已將此**TABLE_NAME**的許可權授**與列出之**被授與者的資料庫使用者名稱。 在中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，這個資料行一律與**TABLE_OWNER**相同。 這個欄位一律會傳回值。 此外，「授與者」資料行可能是資料庫擁有者（**TABLE_OWNER**），或資料庫擁有者在 GRANT 語句中使用 WITH GRANT OPTION 子句來授與許可權的使用者。|  
|**者**|**sysname**|已授與的資料庫使用者名稱，由列出的**授權**者在此**TABLE_NAME** 。 這個欄位一律會傳回值。|  
|**PRIVILEGE**|**Varchar （** 32 **）**|可用的資料表權限之一。 資料表權限可以是下列值之一，或定義實作時，資料來源所支援的其他值：<br /><br /> SELECT =**被**授與者可以抓取一或多個資料行的資料。<br /><br /> INSERT =**被**授與者可以針對一或多個資料行提供新資料列的資料。<br /><br /> UPDATE =**被**授與者可以修改一或多個資料行的現有資料。<br /><br /> DELETE =**被**授與者可以從資料表中移除資料列。<br /><br /> REFERENCES =**被**授與者可以在主鍵/外鍵關聯性中，參考外部資料表中的資料行。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，主索引鍵/外部索引鍵關聯性是利用資料表條件約束來定義的。<br /><br /> 特定資料表許可權提供**給被授與者**的動作範圍與資料來源相關。 例如，UPDATE 許可權可以讓被**授與者**更新一個資料來源上資料表中的所有資料行，而僅限於授與者對另一個資料**源具有 UPDATE 許可權的資料**行。|  
|**IS_GRANTABLE**|**Varchar （** 3 **）**|指出是否允許**被授與者**將許可權授與其他使用者。 這通常稱為 "grant with grant" 權限。 它可以是 YES、NO 或 NULL。 未知 (或 NULL) 值是指不適用 "grant with grant" 的資料來源。|  
  
## <a name="remarks"></a>備註  
 傳回的結果會依**TABLE_QUALIFIER**、 **TABLE_OWNER**、 **TABLE_NAME**和**許可權**來排序。  
  
## <a name="permissions"></a>權限  
 需要結構描述的 SELECT 權限。  
  
## <a name="examples"></a>範例  
 下列範例會從指定連結伺服器 `Product` 中，傳回 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中名稱開頭為 `Seattle1` 的資料表之權限資訊  （ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 假設為連結的伺服器）。  
  
```  
EXEC sp_table_privileges_ex @table_server = 'Seattle1',   
   @table_name = 'Product%',   
   @table_schema = 'Production',  
   @table_catalog ='AdventureWorks2012';  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_column_privileges_ex &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-ex-transact-sql.md)   
 [&#40;Transact-sql&#41;的系統預存程式](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [分散式查詢預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)  
  
  
