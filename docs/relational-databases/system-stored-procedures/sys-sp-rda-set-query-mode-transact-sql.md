---
title: sys.databases sp_rda_set_query_mode （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_set_query_mode
- sys.sp_rda_set_query_mode_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_set_query_mode stored procedure
ms.assetid: 65a0b390-cf87-4db7-972a-1fdf13456c88
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 06690f79bf2cc708a83ec272906b3f4be09fe03d
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82807790"
---
# <a name="syssp_rda_set_query_mode-transact-sql"></a>sys.databases sp_rda_set_query_mode （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  指定是否針對目前已啟用 Stretch 的資料庫和其資料表的查詢同時傳回本機和遠端資料（預設值）或本機資料。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_rda_set_query_mode [ @mode = ] @mode   
    [ , [ @force = ]  @force ]  
```  
  
## <a name="arguments"></a>引數  
 [ @mode =] * \@ 模式*  
 是下列其中一個值。  
  
-   **已停用**針對已啟用 Stretch 之資料表的所有查詢都會失敗。  
  
-   **LOCAL_ONLY**對已啟用 Stretch 之資料表的查詢只會傳回本機資料。  
  
-   **LOCAL_AND_REMOTE**針對已啟用 Stretch 之資料表的查詢會同時傳回本機和遠端資料。 此為預設行為。  
  
 [ @force =] * \@ force*  
 是選擇性的位值，如果您想要在沒有驗證的情況下變更查詢模式，您可以將它設定為1。  
  
## <a name="return-code-values"></a>傳回碼值  
 0（成功）或 >0 （失敗）  
  
## <a name="permissions"></a>權限  
 需要 db_owner 許可權。  
  
## <a name="remarks"></a>備註  
 下列擴充預存程式也會針對已啟用延展功能的資料庫設定查詢模式。  
  
-   **sp_rda_deauthorize_db**  
  
     執行**sp_rda_deauthorize_db**之後，針對已啟用 Stretch 的資料庫和資料表的所有查詢都會失敗。 也就是，查詢模式設定為 [停用]。 若要結束此模式，請執行下列其中一項動作。  
  
    -   執行[sys.databases，sp_rda_reauthorize_db &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)重新連接到遠端 Azure 資料庫。 此操作會自動將查詢模式重設為 LOCAL_AND_REMOTE，這是 Stretch Database 的預設行為。 也就是說，查詢會傳回本機和遠端資料的結果。  
  
    -   使用 LOCAL_ONLY 引數執行[sys.databases sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) ，讓查詢只會針對本機資料執行。  
  
-   **sp_rda_reauthorize_db**  
  
     當您執行[sys.databases 時 sp_rda_reauthorize_db &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)重新連接到遠端 Azure 資料庫時，此作業會自動將查詢模式重設為 [LOCAL_AND_REMOTE]，這是 Stretch Database 的預設行為。 也就是說，查詢會傳回本機和遠端資料的結果。  
  
## <a name="see-also"></a>另請參閱  
 [sp_rda_deauthorize_db &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
