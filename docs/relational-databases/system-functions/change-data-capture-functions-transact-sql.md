---
title: 變更資料擷取函數 (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- change data capture [SQL Server], functions
ms.assetid: e5270557-aca3-44ab-8715-daccd498b88d
caps.latest.revision: 8
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: edd3f10d7f41d470ca0f831f81236387f6903b20
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33227984"
---
# <a name="change-data-capture-functions-transact-sql"></a>異動資料擷取函數 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  異動資料擷取會記錄套用至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表的插入、更新和刪除活動，並以方便取用的關聯式格式提供變更的詳細資料。 系統會針對修改的資料列擷取鏡像追蹤來源資料表之資料行結構的資料行資訊，以及將變更套用至目標環境所需的中繼資料。 下列函數是用來傳回變更的相關資訊。  
  
|||  
|-|-|  
|[cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)|[sys.fn_cdc_has_column_changed &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-has-column-changed-transact-sql.md)|  
|[cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)|[sys.fn_cdc_increment_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql.md)|  
|[sys.fn_cdc_decrement_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-decrement-lsn-transact-sql.md)|[sys.fn_cdc_is_bit_set &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-is-bit-set-transact-sql.md)|  
|[sys.fn_cdc_get_column_ordinal &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-get-column-ordinal-transact-sql.md)|[sys.fn_cdc_map_lsn_to_time &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md)|  
|[sys.fn_cdc_get_max_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql.md)|[sys.fn_cdc_map_time_to_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md)|  
|[sys.fn_cdc_get_min_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md)||  
  
## <a name="see-also"></a>另請參閱  
 [異動資料擷取資料表 &#40;Transact-SQL&#41;](../../relational-databases/system-tables/change-data-capture-tables-transact-sql.md)   
 [異動資料擷取預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/change-data-capture-stored-procedures-transact-sql.md)   
 [關於異動資料擷取 &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
