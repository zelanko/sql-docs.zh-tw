---
title: sys.databases sp_rda_deauthorize_db （Transact-sql） |Microsoft Docs
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6aeb27d4fb452a4ed5b7f45086f601eacb4f0339
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67905117"
---
# <a name="syssp_rda_deauthorize_db-transact-sql"></a>sys.databases sp_rda_deauthorize_db （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  移除本機已啟用 Stretch 的資料庫與遠端 Azure 資料庫之間的已驗證連接。 當遠端資料庫無法連線或處於不一致的狀態，而且您想要變更資料庫中所有已啟用 Stretch 之資料表的查詢行為時，請執行**sp_rda_deauthorize_db** 。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
sp_rda_deauthorize_db   
```  
  
## <a name="return-code-values"></a>傳回碼值  
 0（成功）或 >0 （失敗）  
  
## <a name="permissions"></a>權限  
 需要 db_owner 許可權。  
  
## <a name="remarks"></a>備註  
 執行**sp_rda_deauthorize_db**之後，針對已啟用 Stretch 的資料庫和資料表的所有查詢都會失敗。 也就是，查詢模式設定為 [停用]。 若要結束此模式，請執行下列其中一項動作。  
  
-   執行[sys.databases，sp_rda_reauthorize_db &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)重新連接到遠端 Azure 資料庫。 此操作會自動將查詢模式重設為 LOCAL_AND_REMOTE，這是 Stretch Database 的預設行為。 也就是說，查詢會傳回本機和遠端資料的結果。  
  
-   使用 LOCAL_ONLY 引數執行[sys.databases sp_rda_set_query_mode &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) ，讓查詢只會針對本機資料執行。  
  
## <a name="see-also"></a>另請參閱  
 [sp_rda_set_query_mode &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md)   
 [sp_rda_reauthorize_db &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
