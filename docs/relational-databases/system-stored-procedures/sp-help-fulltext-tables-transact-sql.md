---
title: sp_help_fulltext_tables （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_tables
- sp_help_fulltext_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_tables
ms.assetid: 86e24a5f-a869-43f6-b83e-c52b7b01b5ff
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4ac8e09eff53c04377ccd48a47cc31d9d7ddc5e8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68055022"
---
# <a name="sp_help_fulltext_tables-transact-sql"></a>sp_help_fulltext_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回登錄了全文檢索索引的資料表清單。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]請改用**sys.databases fulltext_indexes**目錄檢視。 如需詳細資訊，請參閱[fulltext_indexes &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_fulltext_tables [ [ @fulltext_catalog_name = ] 'fulltext_catalog_name' ]   
     [ , [ @table_name = ] 'table_name' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @fulltext_catalog_name = ] 'fulltext_catalog_name'`這是全文檢索目錄的名稱。 *fulltext_catalog_name*是**sysname**，預設值是 Null。 如果省略*fulltext_catalog_name*或為 Null，則會傳回與資料庫相關聯的所有全文檢索索引資料表。 如果指定了*fulltext_catalog_name* ，但*table_name*省略或為 Null，則會針對與此目錄相關聯的每個全文檢索索引資料表來抓取全文檢索索引資訊。 如果同時指定*fulltext_catalog_name*和*table_name* ， *table_name*與*fulltext_catalog_name*相關聯，就會傳回一個資料列。否則，會引發錯誤。  
  
`[ @table_name = ] 'table_name'`這是所要求之全文檢索中繼資料的一或兩部分資料表名稱。 *table_name*是**Nvarchar （517）**，預設值是 Null。 如果只指定*table_name* ，則只會傳回與*table_name*相關的資料列。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**TABLE_OWNER**|**sysname**|資料表擁有者。 這是建立資料表之資料庫使用者的名稱。|  
|**TABLE_NAME**|**sysname**|資料表名稱。|  
|**FULLTEXT_KEY_INDEX_NAME**|**sysname**|在指定為唯一索引鍵資料行的資料行上賦予 UNIQUE 條件約束的索引。|  
|**FULLTEXT_KEY_COLID**|**int**|FULLTEXT_KEY_NAME 所識別之唯一索引的資料行識別碼。|  
|**FULLTEXT_INDEX_ACTIVE**|**int**|指定此資料表中標示為全文檢索索引的資料行是否適合查詢：<br /><br /> 0 = 非使用中<br /><br /> 1 = 使用中|  
|**FULLTEXT_CATALOG_NAME**|**sysname**|全文檢索索引資料所在的全文檢索目錄。|  
  
## <a name="permissions"></a>權限  
 執行許可權預設為**public**角色的成員。  
  
## <a name="examples"></a>範例  
 下列範例會傳回與 `Cat_Desc` 全文檢索目錄相關聯之全文檢索索引資料表的名稱。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_help_fulltext_tables 'Cat_Desc';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-sql&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [sp_fulltext_table &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-table-transact-sql.md)   
 [sp_help_fulltext_tables_cursor &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-cursor-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
