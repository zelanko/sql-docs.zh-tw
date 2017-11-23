---
title: "Y (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
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
- MSmerge_settingshistory
- MSmerge_settingshistory_TSQL
dev_langs: TSQL
helpviewer_keywords: MSmerge_settingshistory system table
ms.assetid: 0bdf2d5f-5502-44cd-aa9d-2d5006ad20ce
caps.latest.revision: "28"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ac25c834da1e4101d7a5ae9f58f479994fd0e1b1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="msmergesettingshistory-transact-sql"></a>MSmerge_settingshistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_settingshistory**資料表用來維護的一個合併式複寫拓撲的每項變更的資料列合併式複寫，發行項以及發行集屬性所做的變更記錄。 另外，這份資料表也儲存了何時設定初始屬性設定的相關資訊。 這份資料表儲存在發行集和訂閱資料庫中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**eventtime**|**datetime**|發生事件的日期時間。|  
|**pubid**|**uniqueidentifier**|給定發行集的唯一識別碼。|  
|**artid**|**uniqueidentifier**|給定發行項的唯一識別碼。|  
|**eventtype**|**tinyint**|指定所記錄之事件的類型，它可以是下列項目之一：<br /><br /> **1** – 初始發行集層級屬性設定。<br /><br /> **2** -發行集屬性中的變更。<br /><br /> **101** -初始發行項屬性設定。<br /><br /> **102** -發行項屬性中的變更。|  
|**屬性名稱**|**sysname**|設定或變更的屬性名稱|  
|**previousvalue**|**sysname**|如果變更了屬性，便是先前的屬性值。|  
|**newvalue**|**sysname**|屬性所改成的值，或建立時的值。|  
|**eventtext**|**nvarchar(2000)**|描述事件的字元字串。|  
  
## <a name="see-also"></a>請參閱＜  
 [複寫資料表 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
