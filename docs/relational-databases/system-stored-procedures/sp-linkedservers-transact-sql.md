---
title: "sp_linkedservers (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_linkedservers
- sp_linkedservers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_linkedservers
ms.assetid: d8f82f78-8a1f-4831-bcee-7c36c6e7dfbb
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a8fd9f6a3c9f9acd4f1f956a827cab76dfa810af
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="splinkedservers-transact-sql"></a>sp_linkedservers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回本機伺服器中所定義的連結伺服器清單。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_linkedservers  
```  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或非零數字 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**SRV_NAME**|**sysname**|連結伺服器的名稱。|  
|**SRV_PROVIDERNAME**|**nvarchar (**128**)**|管理指定連結伺服器存取權之 OLE DB 提供者的易記名稱。|  
|**SRV_PRODUCT**|**nvarchar (**128**)**|連結伺服器的產品名稱。|  
|**SRV_DATASOURCE**|**nvarchar (**4000**)**|對應於指定連結伺服器的 OLE DB 資料來源屬性。|  
|**SRV_PROVIDERSTRING**|**nvarchar (**4000**)**|對應於連結伺服器的 OLE DB 提供者字串屬性。|  
|**SRV_LOCATION**|**nvarchar (**4000**)**|對應於指定連結伺服器的 OLE DB 位置屬性。|  
|**SRV_CAT**|**sysname**|對應於指定連結伺服器的 OLE DB 目錄屬性。|  
  
## <a name="permissions"></a>Permissions  
 需要結構描述的 SELECT 權限。  
  
## <a name="see-also"></a>請參閱  
 [sp_catalogs &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_column_privileges &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_columns_ex &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-columns-ex-transact-sql.md)   
 [sp_foreignkeys &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [< sp_indexes &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_primarykeys &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-primarykeys-transact-sql.md)   
 [sp_table_privileges &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [sp_tables_ex &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [分散式的查詢預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)  
  
  
