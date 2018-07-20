---
title: sys.sp_rda_reconcile_batch (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: stored-procedures
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_reconcile_batch
- sys.sp_rda_reconcile_batch_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reconcile_batch stored procedure
ms.assetid: 6d21eac3-7b6c-4fe0-8bc4-bf503f3948a6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a55619d029df6946b68f9af3a3f7c4ad09e08c71
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39084450"
---
# <a name="syssprdareconcilebatch-transact-sql"></a>sys.sp_rda_reconcile_batch (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  協調儲存在遠端 Azure 資料表中的批次識別碼已啟用 Stretch 的 SQL Server 資料表中儲存的批次識別碼。  
  
 通常您只需要執行**sp_rda_reconcile_batch**如果您已經手動刪除遠端資料表中的最近移轉的資料。 當您以手動方式刪除遠端的資料，包括最新的批次時，批次識別碼未同步，移轉會停止。  
 
 若要刪除已移轉至 Azure 的資料，請參閱此頁面上的 < 備註 >。
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
   
## <a name="syntax"></a>語法  
  
```  
  
sp_rda_reconcile_batch @objname = '@objname'  
  
```  
  
## <a name="arguments"></a>引數  
 \@objname = '*\@objname*'  
 已啟用 Stretch 的 SQL Server 資料表的名稱。  
  
## <a name="permissions"></a>[權限]  
 需要 db_owner 權限。  
  
## <a name="remarks"></a>備註  
 如果您想要刪除已移轉至 Azure 的資料，請執行下列動作。  
  
1.  暫停資料移轉。 如需詳細資訊，請參閱[暫停和繼續資料移轉 &#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)。  
  
2.  使用 STAGE_ONLY 提示執行 DELETE 命令，從 SQL Server 暫存資料表刪除資料。 如需詳細資訊，請參閱 <<c0> [ 進行管理更新和刪除](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md#adminHints)。
  
3.  與 REMOTE_ONLY 提示執行 DELETE 命令，從遠端的 Azure 資料表刪除相同的資料。  
  
4.  執行**sp_rda_reconcile_batch**。  
  
5.  繼續資料移轉。 如需詳細資訊，請參閱[暫停和繼續資料移轉 &#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)。  
  
## <a name="example"></a>範例  
 若要先協調批次識別碼，執行下列陳述式。  
  
```sql  
EXEC sp_rda_reconcile_batch @objname = N'StretchEnabledTableName';  
```  
  
  
