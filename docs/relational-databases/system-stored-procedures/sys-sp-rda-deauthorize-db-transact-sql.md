---
title: sys.sp_rda_deauthorize_db (TRANSACT-SQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 7ba94ff4f7093e0974e947c8f8ba2deccd2825ed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65979989"
---
# <a name="syssprdadeauthorizedb-transact-sql"></a>sys.sp_rda_deauthorize_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  移除本機已啟用 Stretch 的資料庫與遠端 Azure 資料庫之間已驗證的連接。 執行**sp_rda_deauthorize_db**當遠端資料庫處於無法連上或不一致的狀態，以及您想要變更資料庫中的所有已啟用 Stretch 之資料表的查詢行為。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
sp_rda_deauthorize_db   
```  
  
## <a name="return-code-values"></a>傳回碼值  
 0 （成功） 或 > 0 （失敗）  
  
## <a name="permissions"></a>Permissions  
 需要 db_owner 權限。  
  
## <a name="remarks"></a>備註  
 在執行後**sp_rda_deauthorize_db** ，針對已啟用 Stretch 的資料庫和資料表的所有查詢都失敗。 也就是查詢模式設為 停用。 若要結束此模式，請執行下列動作。  
  
-   執行[sys.sp_rda_reauthorize_db &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)重新連線到遠端的 Azure 資料庫。 這項作業會自動重設查詢模式 LOCAL_AND_REMOTE，這是 Stretch Database 的預設行為。 也就是說，查詢會傳回結果，從本機和遠端資料。  
  
-   執行[sys.sp_rda_set_query_mode &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) LOCAL_ONLY 引數，以便繼續執行，針對僅限本機資料的查詢。  
  
## <a name="see-also"></a>另請參閱  
 [sys.sp_rda_set_query_mode &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md)   
 [sys.sp_rda_reauthorize_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
