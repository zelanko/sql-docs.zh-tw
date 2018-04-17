---
title: cdc.ddl_history (TRANSACT-SQL) |Microsoft 文件
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
- cdc.ddl_history_TSQL
- cdc.ddl_history
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.ddl_history
ms.assetid: cb97ea71-da2f-441a-bbd2-db1f5f48ab49
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 96232efb8041bceeff92f479a56b4b56483ab1fa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="cdcddlhistory-transact-sql"></a>cdc.ddl_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對在啟用異動資料擷取之資料表中所做的每個資料定義語言 (DDL) 變更，各傳回一個資料列。 您可以使用這個資料表來判斷來源資料表發生 DDL 變更的時間，以及變更的內容。 沒有 DDL 變更的來源資料表就不會在這份資料表中具有任何項目。  
  
 我們建議您不要直接查詢系統資料表。 請改為執行[sys.sp_cdc_get_ddl_history](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md)預存程序。  
   
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**source_object_id**|**int**|套用 DDL 變更之來源資料表的識別碼。|  
|**object_id**|**int**|與來源資料表擷取執行個體相關聯之變更資料表的識別碼。|  
|**required_column_update**|**bit**|指出擷取資料行的資料類型已在來源資料表中修改。 這項修改會更改變更資料表中的資料行。|  
|**ddl_command**|**nvarchar(max)**|套用至來源資料表的 DDL 陳述式。|  
|**ddl_lsn**|**binary(10)**|與 DDL 修改之認可相關聯的記錄序號 (LSN)。|  
|**ddl_time**|**datetime**|對來源資料表進行 DDL 變更的日期和時間。|  
  
## <a name="see-also"></a>另請參閱  
 [sys.sp_cdc_help_change_data_capture &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  
