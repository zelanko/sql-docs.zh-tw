---
title: MSreplication_queue & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c2370bfc06f9fd939f5778ad52e6cb09aeae2806
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52819051"
---
# <a name="msreplicationqueue-transact-sql"></a>MSreplication_queue (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSreplication_queue**資料表由複寫程序來儲存公布的所有使用 SQL 架構佇列更新訂閱已排入佇列的佇列的命令。 這份資料表儲存在訂閱資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**發行者**|**sysname**|發行者的名稱。|  
|**publisher_db**|**sysname**|發行集資料庫的名稱。|  
|**發行集**|**sysname**|發行集的名稱。|  
|**tranid**|**sysname**|執行佇列命令所用的交易識別碼。|  
|**data**|**varbinary(8000)**|儲存佇列命令相關資訊的壓縮位元組資料流。|  
|**datalen**|**int**|資料長度 (以位元組為單位)。|  
|**commandtype**|**int**|目前置於佇列中的命令類型：<br /><br /> 1 = 交易中的使用者命令。<br /><br /> 2 = 訂閱同步處理命令。|  
|**insertdate**|**datetime**|插入的日期。|  
|**orderkey**|**bigint**|單純遞增的識別欄位。|  
|**cmdstate**|**bit**|命令狀態：<br /><br /> 0 = 完成。<br /><br /> 1 = 部份。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
