---
title: sys.sp_rda_set_query_mode (Transact-SQL) | Microsoft Docs
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: aa168f3bbac37e34730d5ee0ab348f5fd7d1743d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65982887"
---
# <a name="syssprdasetquerymode-transact-sql"></a>sys.sp_rda_set_query_mode (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  指定是否針對目前的已啟用 Stretch 的資料庫與資料表的查詢會傳回本機和遠端資料 （預設值） 或僅限本機的資料。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_rda_set_query_mode [ @mode = ] @mode   
    [ , [ @force = ]  @force ]  
```  
  
## <a name="arguments"></a>引數  
 [ @mode = ] *@mode*  
 是下列值之一。  
  
-   **已停用**針對已啟用 Stretch 之資料表的所有查詢都失敗。  
  
-   **LOCAL_ONLY**針對已啟用 Stretch 之資料表的查詢會傳回僅限本機的資料。  
  
-   **以 LOCAL_AND_REMOTE**針對已啟用 Stretch 之資料表的查詢會傳回本機和遠端資料。 這是預設行為。  
  
 [ @force = ]  *@force*  
 是選擇性的位元值，如果您想要變更查詢模式，而不需驗證，您可以設定為 1。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 （成功） 或 > 0 （失敗）  
  
## <a name="permissions"></a>Permissions  
 需要 db_owner 權限。  
  
## <a name="remarks"></a>備註  
 下列的擴充預存程序也會設定已啟用 Stretch 的資料庫的查詢模式。  
  
-   **sp_rda_deauthorize_db**  
  
     在執行後**sp_rda_deauthorize_db** ，針對已啟用 Stretch 的資料庫和資料表的所有查詢都失敗。 也就是查詢模式設為 停用。 若要結束此模式，請執行下列動作。  
  
    -   執行[sys.sp_rda_reauthorize_db &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)重新連線到遠端的 Azure 資料庫。 這項作業會自動重設查詢模式 LOCAL_AND_REMOTE，這是 Stretch Database 的預設行為。 也就是說，查詢會傳回結果，從本機和遠端資料。  
  
    -   執行[sys.sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) LOCAL_ONLY 引數，以便繼續執行，針對僅限本機資料的查詢。  
  
-   **sp_rda_reauthorize_db**  
  
     當您執行[sys.sp_rda_reauthorize_db &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)重新連線到遠端的 Azure 資料庫，這項作業會自動重設查詢模式 LOCAL_AND_REMOTE，這是預設行為的Stretch Database。 也就是說，查詢會傳回結果，從本機和遠端資料。  
  
## <a name="see-also"></a>另請參閱  
 [sys.sp_rda_deauthorize_db &#40;SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
