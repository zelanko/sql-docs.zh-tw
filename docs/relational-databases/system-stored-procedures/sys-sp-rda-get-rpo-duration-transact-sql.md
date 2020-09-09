---
title: sys. sp_rda_get_rpo_duration (Transact-sql) |Microsoft Docs
description: 使用 sys. sp_rda_get_rpo_duration 取得 SQL Server 保留在臨時表中的已遷移資料時數，以完整還原遠端 Azure 資料庫。
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_get_rpo_duration
- sys.sp_rda_get_rpo_duration_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_get_rpo_duration stored procedure
ms.assetid: 35882067-3072-47ff-9024-ca453c0f49a7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b3b52298861da031dc5eab6b3a32135eec9d26cb
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538457"
---
# <a name="syssp_rda_get_rpo_duration-transact-sql"></a>sys. sp_rda_get_rpo_duration (Transact-sql) 
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  取得 SQL Server 保留在臨時表中的已遷移資料時數，以協助確保遠端 Azure 資料庫的完整還原（如果需要還原時間點）。 
  
  如需詳細資訊，請參閱 [暫時保留遷移的資料列，Stretch Database 降低 Azure 資料的資料遺失風險](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md#stretchRPO)。  
    
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>語法    
    
```    
    
sp_rda_get_rpo_duration @durationinhours output    
    
```    
    
## <a name="output-parameter"></a>輸出參數    
 *\@durationinhours*    
  這是 (非 null 整數值的小時數，) SQL Server 針對目前已啟用 Stretch 的資料庫保留的已遷移資料。    
    
## <a name="permissions"></a>權限    
 需要 db_owner 許可權。    
    
## <a name="remarks"></a>備註    
 藉由執行 [sys. sp_rda_set_rpo_duration &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md)來變更值。    
    
## <a name="see-also"></a>另請參閱    
 [sys. sp_rda_set_rpo_duration &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md)     
 [ (Stretch Database) 還原已啟用 Stretch 的資料庫 ](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)    
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)    
    
  
