---
title: cdc.change_tables (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- cdc.change_tables
- cdc.change_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.change_tables
ms.assetid: 3525a5f5-8d8b-46a8-b334-4b7cd9fb7c21
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e2f10909d7660e7dd6e65c38182a8332068a801f
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39103870"
---
# <a name="cdcchangetables-transact-sql"></a>cdc.change_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對資料庫中的每個變更資料表，各傳回一個資料列。 當來源資料表啟用變更資料擷取時，就會建立變更資料表。 我們建議您不要直接查詢系統資料表。 請改為執行[sys.sp_cdc_help_change_data_capture](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)預存程序。  
  |資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|變更資料表的識別碼。 在資料庫中，這是唯一的。|  
|**version**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> 若為 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，這個資料行一律會傳回 0。|  
|**source_object_id**|**int**|啟用變更資料擷取之來源資料表的識別碼。|  
|**擷取執行個體**|**sysname**|用來命名執行個體專用追蹤物件之擷取執行個體的名稱。 根據預設，名稱衍生自來源結構描述名稱加上來源資料表名稱的格式*schemaname_sourcename*。|  
|**start_lsn**|**binary(10)**|在變更資料表中查詢變更資料時，代表低端點的記錄序號 (LSN)。<br /><br /> NULL = 尚未建立低端點。|  
|**end_lsn**|**binary(10)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> 若為 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]，這個資料行一律會傳回 NULL。|  
|**supports_net_changes**|**bit**|針對變更資料表啟用查詢淨變更的支援。|  
|**has_drop_pending**|**bit**|擷取處理序收到了來源資料表已經卸除的通知。|  
|**role_name**|**sysname**|用來限制變更資料之存取權的資料庫角色名稱。<br /><br /> NULL = 不使用角色。|  
|**index_name**|**sysname**|在來源資料表中，用來唯一識別資料列的索引名稱。 **index_name**是來源資料表的主索引鍵索引名稱或唯一索引名稱指定來源資料表上啟用異動資料擷取時。<br /><br /> NULL = 啟用異動資料擷取時，來源資料表沒有主索引鍵，而且啟用異動資料擷取時，沒有指定唯一的索引。<br /><br /> 注意： 如果主索引鍵所在的資料表上啟用異動資料擷取時，異動資料擷取功能使用的索引，而不論是否啟用淨變更。 在啟用異動資料擷取之後，就不允許在主索引鍵上進行修改。 如果資料表上沒有主索引鍵，您仍然可以啟用異動資料擷取，但是只有當淨變更設定為 False 時才能啟用。 在啟用異動資料擷取之後，您可以建立主索引鍵。 您也可以修改主索引鍵，因為異動資料擷取不會使用此主索引鍵。|  
|**filegroup_name**|**sysname**|變更資料表所在的檔案群組名稱。<br /><br /> NULL = 變更資料表位於資料庫的預設檔案群組中。|  
|**create_date**|**datetime**|啟用來源資料表的日期。|  
|**partition_switch**|**bit**|指出是否**SWITCH PARTITION**命令**ALTER TABLE**可以針對啟用異動資料擷取的資料表來執行。 0 表示已封鎖資料分割切換。 非資料分割的資料表一律傳回 1。|  
  
## <a name="see-also"></a>另請參閱  
 [sys.sp_cdc_help_change_data_capture &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)  
  
  
