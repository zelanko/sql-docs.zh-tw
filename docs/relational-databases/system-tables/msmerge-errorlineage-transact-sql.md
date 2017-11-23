---
title: "M (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSmerge_errorlineage_TSQL
- MSmerge_errorlineage
dev_langs: TSQL
helpviewer_keywords: MSmerge_errorlineage system table
ms.assetid: 3bcbd328-c958-4cd4-a573-3c35539fa919
caps.latest.revision: "27"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 50e8b8e9745a29155d71cfd3ff1a027321ef878e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="msmergeerrorlineage-transact-sql"></a>MSmerge_errorlineage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_errorlineage**資料表包含已刪除 「 訂閱者 」，但刪除動作不會傳播到 「 發行者 」 的資料列。 這份資料表儲存在發行集和訂閱資料庫中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|指派給進行合併式複寫發行之資料表的整數值。 對應中的暱稱欄位**sysmergearticles**資料表。|  
|**rowguid**|**uniqueidentifier**|資料列識別碼。|  
|**歷程**|**varbinary(501)**|儲存訂閱者和發行者的資料列更新記錄清單。 它用來偵測和解決衝突狀況。|  
  
## <a name="see-also"></a>請參閱＜  
 [複寫資料表 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
