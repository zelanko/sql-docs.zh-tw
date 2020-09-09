---
title: " (Transact-sql) 的擴充預存程式"
description: 瞭解當您使用已啟用 Stretch 的資料庫時，可以使用的擴充預存程式。 請參閱如何協調資料行和執行其他工作。
titleSuffix: SQL Server Stretch Database
ms.custom: seo-dt-2019
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Stretch Database, stored procedures
ms.assetid: bda29952-4b8b-4295-ab78-f24dcb0b03c6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 975255806d8a031d1998d85778d89ccbf97a806f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545819"
---
# <a name="stretch-database-extended-stored-procedures-transact-sql"></a>Stretch Database (Transact-sql 的擴充預存程式) 
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

 本章節描述與 Stretch Database 相關的擴充預存程式。  
  
## <a name="in-this-section"></a>本節內容  
[sys. sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md) 移除本機已啟用 Stretch 的資料庫與遠端 Azure 資料庫之間的已驗證連接。

[sys. sp_rda_get_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md) 取得 SQL Server 保留在臨時表中的已遷移資料時數，以協助確保遠端 Azure 資料庫的完整還原（如果需要還原）。
  
 [sys. sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) 還原已啟用 Stretch 和遠端資料庫之本機資料庫之間的已驗證連接。
  
 [sys.sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md)  
 使用儲存在遠端 Azure 資料表中的批次識別碼，來協調儲存在已啟用 Stretch 的 SQL Server 資料表中的批次識別碼，以取得最近遷移的資料。 
 
[sys. sp_rda_reconcile_columns](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-columns-transact-sql.md) 將遠端 Azure 資料表中的資料行協調成已啟用 Stretch 的 SQL Server 資料表中的資料行。
 
 [sys. sp_rda_reconcile_indexes](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-indexes-transact-sql.md) 將架構工作排入佇列，以協調遠端資料表上的索引。
 
 [sys. sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) 指定針對目前已啟用 Stretch 的資料庫和其資料表的查詢，是否會將本機和遠端資料同時 (預設) 或本機資料。
 
 [sys. sp_rda_set_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md) 設定 SQL Server 保留在臨時表中的已遷移資料時數，以協助確保遠端 Azure 資料庫的完整還原（如果需要還原）。
 
 [sys. sp_rda_test_connection](../../relational-databases/system-stored-procedures/sys-sp-rda-test-connection-transact-sql.md) 測試 SQL Server 與遠端 Azure 伺服器之間的連線，並報告可能導致資料移轉的問題。
 
## <a name="see-also"></a>另請參閱  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
