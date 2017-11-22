---
title: "sys.sp_rda_get_rpo_duration (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-stretch
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_get_rpo_duration
- sys.sp_rda_get_rpo_duration_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.sp_rda_get_rpo_duration stored procedure
ms.assetid: 35882067-3072-47ff-9024-ca453c0f49a7
caps.latest.revision: "13"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4a36d1b1e04e53098710a1cacc8c463653f82710
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="syssprdagetrpoduration-transact-sql"></a>sys.sp_rda_get_rpo_duration (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  可確保完整還原遠端 Azure 資料庫中，如果需要還原時間點的臨時資料表中取得的 SQL Server 會保留已移轉資料的時數。 
  
  如需詳細資訊，請參閱[Stretch Database 可減少您的 Azure 資料的資料遺失的風險暫時保留已移轉的資料列](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md#stretchRPO)。  
    
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>語法    
    
```    
    
sp_rda_get_rpo_duration @durationinhours output    
    
```    
    
## <a name="output-parameter"></a>輸出參數    
 *@durationinhours*    
  是的小時數 （非 null 的整數值） 的移轉 SQL Server 會保留目前已啟用 Stretch 的資料庫的資料。    
    
## <a name="permissions"></a>Permissions    
 需要 db_owner 權限。    
    
## <a name="remarks"></a>備註    
 變更值，藉由執行[sys.sp_rda_set_rpo_duration &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md).    
    
## <a name="see-also"></a>請參閱＜    
 [sys.sp_rda_set_rpo_duration &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md)     
 [還原已啟用 Stretch 的資料庫 (Stretch Database)](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)    
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)    
    
  
