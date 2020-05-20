---
title: MSreplication_queue （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSreplication_queue
- MSreplication_queue_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_queue system table
ms.assetid: 664bf817-8021-4417-96d6-2bb1e4baabff
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7763f7406f865194743c43a6d182466767799b41
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82829825"
---
# <a name="msreplication_queue-transact-sql"></a>MSreplication_queue (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  複寫程式會使用**MSreplication_queue**資料表來儲存所有使用 SQL 架構佇列的佇列更新訂閱所發出的佇列命令。 這份資料表儲存在訂閱資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|發行者的名稱。|  
|**publisher_db**|**sysname**|發行集資料庫的名稱。|  
|**發行集**|**sysname**|發行集的名稱。|  
|**tranid**|**sysname**|執行佇列命令所用的交易識別碼。|  
|**資料**|**varbinary(8000)**|儲存佇列命令相關資訊的壓縮位元組資料流。|  
|**datalen**|**int**|資料長度 (以位元組為單位)。|  
|**commandtype**|**int**|目前置於佇列中的命令類型：<br /><br /> 1 = 交易中的使用者命令。<br /><br /> 2 = 訂閱同步處理命令。|  
|**insertdate**|**datetime**|插入的日期。|  
|**orderkey**|**bigint**|單純遞增的識別欄位。|  
|**cmdstate**|**bit**|命令狀態：<br /><br /> 0 = 完成。<br /><br /> 1 = 部份。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
