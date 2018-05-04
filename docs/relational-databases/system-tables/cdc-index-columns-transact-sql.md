---
title: cdc.index_columns (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- cdc.index_columns_TSQL
- cdc.index_columns
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.index_columns
ms.assetid: 256ec8a5-3031-40a8-9fdb-99db42ea453d
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 23ebf53a0d65f283e45546327ac55ef5c8207e9e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="cdcindexcolumns-transact-sql"></a>cdc.index_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對每一個與變更資料表相關聯的索引資料行，各傳回一個資料列。 異動資料擷取會使用索引資料行來唯一識別來源資料表中的資料列。 根據預設，來源資料表之主索引鍵的資料行包含在內。 不過，在來源資料表上啟用異動資料擷取時，如果指定了來源資料表上的唯一索引，就會改用該索引中的資料行。 如果啟用淨變更追蹤，就需要使用來源資料表的主索引鍵或唯一索引。 如需詳細資訊，請參閱[sys.sp_cdc_enable_table &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)。  
  
 我們建議您不要直接查詢系統資料表。 請改為執行[sys.sp_cdc_help_change_data_capture](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)預存程序。  

  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|變更資料表的識別碼。|  
|**column_name**|**sysname**|索引資料行的名稱。|  
|**index_ordinal**|**tinyint**|索引中資料行的序數 (以 1 為基底)。|  
|**column_id**|**int**|來源資料表中資料行的識別碼。|  
  
## <a name="see-also"></a>另請參閱  
 [cdc.change_tables &#40;Transact SQL&#41;](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md)  
  
  
