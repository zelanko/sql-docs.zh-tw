---
title: cdc.lsn_time_mapping (TRANSACT-SQL) |Microsoft 文件
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
- cdc.lsn_time_mapping
- cdc.lsn_time_mapping_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.lsn_time_mapping
ms.assetid: 1cb7aedc-48a4-486e-9b91-d30c4bd4084e
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 559dc5dfa4fe3fba6309ac307388d02b962c206c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="cdclsntimemapping-transact-sql"></a>cdc.lsn_time_mapping (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對在變更資料表中具有資料列的每筆交易，各傳回一個資料列。 這個資料表是用來在記錄序號 (LSN) 認可值與交易認可的時間之間進行對應。 此外，系統也會針對沒有變更資料表項目的位置，記錄項目。 在變更活動很少或沒有變更活動的期間，這可讓資料表記錄 LSN 處理的完成狀態。  
  
 我們建議您不要直接查詢系統資料表。 請改為執行[sys.fn_cdc_map_lsn_to_time &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md)和[sys.fn_cdc_map_time_to_lsn &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md)系統函數。  
    
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**start_lsn**|**binary(10)**|認可交易的 LSN。|  
|**tran_begin_time**|**datetime**|與 LSN 相關聯之交易開始的時間。|  
|**tran_end_time**|**datetime**|交易結束的時間。|  
|**tran_id**|**varbinary(10)**|交易的識別碼。|  
  
## <a name="see-also"></a>另請參閱  
 [交易記錄 &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [cdc。&#60;capture_instance&#62;_CT &#40;Transact SQL&#41;](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)  
  
  
