---
title: sys. sp_rda_deauthorize_db (Transact-sql) |Microsoft Docs
description: 瞭解如何使用 sys. sp_rda_deauthorize_db 移除本機已啟用 Stretch 的資料庫與遠端 Azure 資料庫之間的已驗證連接。
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_deauthorize_db
- sys.sp_rda_deauthorize_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_deauthorize_db stored procedure
ms.assetid: 2e362e15-2cd5-4856-9f0b-54df56b0866b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5c8413bf0a78ea1780d0babfc6fd88abb615d4ea
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538471"
---
# <a name="syssp_rda_deauthorize_db-transact-sql"></a>sys. sp_rda_deauthorize_db (Transact-sql) 
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  移除本機已啟用 Stretch 的資料庫與遠端 Azure 資料庫之間的已驗證連接。 當遠端資料庫無法連接或處於不一致的狀態，而且您想要變更資料庫中所有已啟用 Stretch 之資料表的查詢行為時，請執行 **sp_rda_deauthorize_db**  。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
sp_rda_deauthorize_db   
```  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 >0 (失敗)   
  
## <a name="permissions"></a>權限  
 需要 db_owner 許可權。  
  
## <a name="remarks"></a>備註  
 執行 **sp_rda_deauthorize_db** 之後，針對已啟用 Stretch 的資料庫和資料表的所有查詢都會失敗。 也就是說，查詢模式會設為 DISABLED。 若要結束此模式，請執行下列其中一項動作。  
  
-   執行 [sys. sp_rda_reauthorize_db &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) 以重新連接至遠端 Azure 資料庫。 這項作業會自動將查詢模式重設為 LOCAL_AND_REMOTE，這是 Stretch Database 的預設行為。 也就是說，查詢會傳回本機和遠端資料的結果。  
  
-   使用 LOCAL_ONLY 引數執行 [sys. sp_rda_set_query_mode &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) ，讓查詢繼續針對本機資料執行。  
  
## <a name="see-also"></a>另請參閱  
 [sys. sp_rda_set_query_mode &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md)   
 [sys. sp_rda_reauthorize_db &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
