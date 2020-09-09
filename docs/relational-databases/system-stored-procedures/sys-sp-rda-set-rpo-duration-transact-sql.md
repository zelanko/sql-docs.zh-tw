---
title: sys. sp_rda_set_rpo_duration (Transact-sql) |Microsoft Docs
description: 瞭解 sys. sp_rda_set_rpo_duration。 您可以使用這個預存程式來設定 SQL Server 保留在臨時表中的已遷移資料時數。
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_set_rpo_duration
- sys.sp_rda_set_rpo_duration_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_set_rpo_duration stored procedure
ms.assetid: 95c80c5b-9252-4612-9ea7-544c48834fd2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d37717f2b2c8a3dad804538a9268e64023776422
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540439"
---
# <a name="syssp_rda_set_rpo_duration-transact-sql"></a>sys. sp_rda_set_rpo_duration (Transact-sql) 
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  設定 SQL Server 保留在臨時表中的已遷移資料時數，以協助確保遠端 Azure 資料庫的完整還原（如果需要還原時間點）。    
    
 如需詳細資訊，請參閱 [暫時保留遷移的資料列，Stretch Database 降低 Azure 資料的資料遺失風險](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md#stretchRPO)。  
   
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
     
## <a name="syntax"></a>語法    
    
```    
    
sp_rda_set_rpo_duration [ @duration_hrs = ] duration_hrs    
    
```    
    
## <a name="arguments"></a>引數    
 [ @duration_hrs =] *duration_hrs*    
 這是您想要 SQL Server 保留給目前已啟用 Stretch 之資料庫的 (非 null 整數值) 的小時數。 預設值和最小值為8小時。    
 
 > [!NOTE]
 > SQL Server 上的值愈高，需要的儲存空間越多。
    
## <a name="permissions"></a>權限    
 需要 db_owner 許可權。    
    
## <a name="remarks"></a>備註    
 藉由執行 [sys. sp_rda_get_rpo_duration &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md)來取得目前的值。    
    
## <a name="see-also"></a>另請參閱    
 [sys. sp_rda_get_rpo_duration &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md)     
 [ (Stretch Database) 還原已啟用 Stretch 的資料庫 ](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)     
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)    
    
  
