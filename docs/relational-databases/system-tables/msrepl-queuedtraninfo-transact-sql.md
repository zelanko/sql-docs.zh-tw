---
title: MSrepl_queuedtraninfo (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
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
- MSrepl_queuedtraninfo_TSQL
- MSrepl_queuedtraninfo
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_queuedtraninfo system table
ms.assetid: af7a5baf-32ea-475f-b6b9-68c557b4980c
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 8dfae0143bf2c9841166220ff32b898cec601d5f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33004925"
---
# <a name="msreplqueuedtraninfo-transact-sql"></a>MSrepl_queuedtraninfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **q**資料表由複寫處理程序來儲存所有佇列更新訂閱所使用 SQL 架構佇列更新所發出的佇列命令相關資訊。 這份資料表儲存在訂閱資料庫中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**發行者**|**sysname**|發行者的名稱。|  
|**publisher_db**|**sysname**|發行集資料庫的名稱。|  
|**發行集**|**sysname**|發行集的名稱。|  
|**Tranid**|**sysname**|執行佇列命令所用的交易識別碼。|  
|**maxorderkey**|**bigint**|僅供內部使用。|  
|**commandcount**|**bigint**|僅供內部使用。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
