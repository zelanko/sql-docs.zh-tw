---
title: sys.foreign_keys (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- foreign_keys
- sys.foreign_keys
- sys.foreign_keys_TSQL
- foreign_keys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.foreign_keys catalog view
ms.assetid: e960df1a-13fc-43ee-ba91-34c1b719ac2c
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d1cceaf4c200f6fe9f2bf6c735548bc0f439dab7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62465569"
---
# <a name="sysforeignkeys-transact-sql"></a>sys.foreign_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  包含一個資料列，每個物件，與外部索引鍵條件約束**sys.object.type** = f。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**\<從 sys.objects 繼承的資料行 >**||如需這個檢視所繼承的資料行的清單，請參閱 < [j &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。|  
|**referenced_object_id**|**int**|被參考的物件識別碼。|  
|**key_index_id**|**int**|被參考的物件內之金鑰索引識別碼。|  
|**is_disabled**|**bit**|FOREIGN KEY 條件約束已停用。|  
|**is_not_for_replication**|**bit**|FOREIGN KEY 條件約束是利用 NOT FOR REPLICATION 選項來建立的。|  
|**is_not_trusted**|**bit**|FOREIGN KEY 條件約束尚未經過系統驗證。|  
|**delete_referential_action**|**tinyint**|在進行刪除時，針對這個 FOREIGN KEY 而宣告的參考動作。<br /><br /> 0 = 沒有動作<br /><br /> 1 = 串聯<br /><br /> 2 = 設為 NULL<br /><br /> 3 = 設為預設值|  
|**delete_referential_action_desc**|**nvarchar(60)**|在進行刪除時，針對這個 FOREIGN KEY 而宣告的參考動作之描述。<br /><br /> NO_ACTION<br /><br /> CASCADE<br /><br /> SET_NULL<br /><br /> SET_DEFAULT|  
|**update_referential_action**|**tinyint**|在進行更新時，針對這個 FOREIGN KEY 而宣告的參考動作。<br /><br /> 0 = 沒有動作<br /><br /> 1 = 串聯<br /><br /> 2 = 設為 NULL<br /><br /> 3 = 設為預設值|  
|**update_referential_action_desc**|**nvarchar(60)**|在進行更新時，針對這個 FOREIGN KEY 而宣告的參考動作之描述。<br /><br /> NO_ACTION<br /><br /> CASCADE<br /><br /> SET_NULL<br /><br /> SET_DEFAULT|  
|**is_system_named**|**bit**|1 = 名稱是系統所產生。<br /><br /> 0 = 名稱是使用者所提供。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [物件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [查詢 SQL Server 系統目錄常見問題集](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
