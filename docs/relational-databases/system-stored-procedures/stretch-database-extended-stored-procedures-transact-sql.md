---
title: Stretch Database 擴充預存程序 (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7f96a07b6106667a06c492a368799994849cae10
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47704798"
---
# <a name="stretch-database-extended-stored-procedures-transact-sql"></a>Stretch Database 的擴充預存程序 & Amp;#40;transact-SQL&AMP;#41
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

 本章節描述相關 Stretch Database 的擴充預存程序。  
  
## <a name="in-this-section"></a>本節內容  
[sys.sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)移除本機已啟用 Stretch 的資料庫與遠端 Azure 資料庫之間已驗證的連接。

[sys.sp_rda_get_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md)取得暫存資料表以協助確保完整還原遠端的 Azure 資料庫中，如果有必要進行還原的 SQL Server 會保留已移轉資料的時數。
  
 [sys.sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)還原遠端資料庫啟用 Stretch 的本機資料庫之間已驗證的連接。
  
 [sys.sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md)  
 協調儲存在遠端 Azure 資料表中的批次識別碼儲存在最近移轉的資料已啟用 Stretch 的 SQL Server 資料表中的批次識別碼。 
 
[sys.sp_rda_reconcile_columns](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-columns-transact-sql.md)調解遠端 Azure 資料表中的資料行中的資料行已啟用 Stretch 的 SQL Server 資料表。
 
 [sys.sp_rda_reconcile_indexes](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-indexes-transact-sql.md)協調遠端資料表上的索引的結構描述工作排入佇列。
 
 [sys.sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md)指定是否針對目前的已啟用 Stretch 的資料庫與資料表的查詢會傳回本機和遠端資料 （預設值） 或僅限本機的資料。
 
 [sys.sp_rda_set_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md)以協助確保完整還原遠端的 Azure 資料庫中，如果有必要進行還原的暫存資料表中設定的 SQL Server 會保留已移轉資料的時數。
 
 [sys.sp_rda_test_connection](../../relational-databases/system-stored-procedures/sys-sp-rda-test-connection-transact-sql.md)測試從 SQL Server 連接到遠端 Azure 伺服器和報告可能會導致資料移轉的問題。
 
## <a name="see-also"></a>另請參閱  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
