---
title: sys.sp_rda_get_rpo_duration (TRANSACT-SQL) |Microsoft Docs
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0882344345c315f13d6cca11b7a1d1db88c9417b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47769696"
---
# <a name="syssprdagetrpoduration-transact-sql"></a>sys.sp_rda_get_rpo_duration (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  取得移轉之資料的 SQL Server 會保留時的數，以協助確保完整還原遠端的 Azure 資料庫中，如果需要還原時間點的臨時資料表中。 
  
  如需詳細資訊，請參閱 < [Stretch Database 透過暫時保留已移轉的資料列來減少您的 Azure 資料的資料遺失的風險](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md#stretchRPO)。  
    
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>語法    
    
```    
    
sp_rda_get_rpo_duration @durationinhours output    
    
```    
    
## <a name="output-parameter"></a>輸出參數    
 *@durationinhours*    
  是的小時數 （非 null 的整數值） 的 SQL Server 會保留目前已啟用 Stretch 的資料庫的移轉資料。    
    
## <a name="permissions"></a>Permissions    
 需要 db_owner 權限。    
    
## <a name="remarks"></a>備註    
 變更值，藉由執行[sys.sp_rda_set_rpo_duration &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md)。    
    
## <a name="see-also"></a>另請參閱    
 [sys.sp_rda_set_rpo_duration &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md)     
 [還原已啟用 Stretch 的資料庫 (Stretch Database)](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)    
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)    
    
  
