---
title: cdc. index_columns （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc.index_columns_TSQL
- cdc.index_columns
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.index_columns
ms.assetid: 256ec8a5-3031-40a8-9fdb-99db42ea453d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 69ed86e55cadf6c594ca764874bc1257c6d1a9a5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68035345"
---
# <a name="cdcindex_columns-transact-sql"></a>cdc.index_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對每一個與變更資料表相關聯的索引資料行，各傳回一個資料列。 異動資料擷取會使用索引資料行來唯一識別來源資料表中的資料列。 根據預設，來源資料表之主索引鍵的資料行包含在內。 不過，在來源資料表上啟用異動資料擷取時，如果指定了來源資料表上的唯一索引，就會改用該索引中的資料行。 如果啟用淨變更追蹤，就需要使用來源資料表的主索引鍵或唯一索引。 如需詳細資訊，請參閱[sp_cdc_enable_table &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)。  
  
 我們建議您不要直接查詢系統資料表。 請改為執行[sys.databases sp_cdc_help_change_data_capture](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)預存程式。  

  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|變更資料表的識別碼。|  
|**column_name**|**sysname**|索引資料行的名稱。|  
|**index_ordinal**|**tinyint**|索引中資料行的序數 (以 1 為基底)。|  
|**column_id**|**int**|來源資料表中資料行的識別碼。|  
  
## <a name="see-also"></a>另請參閱  
 [change_tables &#40;Transact-sql&#41;](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md)  
  
  
