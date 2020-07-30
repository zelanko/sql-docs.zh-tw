---
title: 管理資料倉儲預存程式（Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- management data warehouse, data collector stored procedures
ms.assetid: bc492b18-6965-4bb5-8065-fe2641d29590
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b1dc4579216af9f47d120f19662de2908cf7f40f
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87394313"
---
# <a name="management-data-warehouse-stored-procedures-transact-sql"></a>管理資料倉儲預存程序 (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  資料收集器會將資料和資料收集器類型資訊儲存在管理資料倉儲中。 下列預存程序是用來更新資料和變更管理資料倉儲中的資料表。  

:::row:::
    :::column:::
        [core.sp_create_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-create-snapshot-transact-sql.md)

        [core.sp_add_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-add-collector-type-transact-sql.md)

        [core.sp_purge_data &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-purge-data-transact-sql.md)
    :::column-end:::
    :::column:::
        [core.sp_update_data_source &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-update-data-source-transact-sql.md)

        [core.sp_remove_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-remove-collector-type-transact-sql.md)
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [資料收集器預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)  
  
  
