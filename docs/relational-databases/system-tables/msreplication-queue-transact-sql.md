---
title: MSreplication_queue (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSreplication_queue
- MSreplication_queue_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_queue system table
ms.assetid: 664bf817-8021-4417-96d6-2bb1e4baabff
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7b09ee5ba3c1a2ad5caa827572ecc3cc881013be
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="msreplicationqueue-transact-sql"></a>MSreplication_queue (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSreplication_queue**資料表由複寫程序來儲存發行所有使用 SQL 架構佇列更新訂閱佇列的佇列的命令。 這份資料表儲存在訂閱資料庫中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**發行者**|**sysname**|發行者的名稱。|  
|**publisher_db**|**sysname**|發行集資料庫的名稱。|  
|**發行集**|**sysname**|發行集的名稱。|  
|**Tranid**|**sysname**|執行佇列命令所用的交易識別碼。|  
|**data**|**varbinary(8000)**|儲存佇列命令相關資訊的壓縮位元組資料流。|  
|**datalen**|**int**|資料長度 (以位元組為單位)。|  
|**commandtype**|**int**|目前置於佇列中的命令類型：<br /><br /> 1 = 交易中的使用者命令。<br /><br /> 2 = 訂閱同步處理命令。|  
|**insertdate**|**datetime**|插入的日期。|  
|**orderkey**|**bigint**|單純遞增的識別欄位。|  
|**cmdstate**|**bit**|命令狀態：<br /><br /> 0 = 完成。<br /><br /> 1 = 部份。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
