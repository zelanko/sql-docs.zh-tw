---
title: "sys.syscurconfigs (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.syscurconfigs
- sys.syscurconfigs_TSQL
- syscurconfigs
- syscurconfigs_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sys.syscurconfigs compatibility view
- syscurconfigs system table
ms.assetid: 454ab849-07a5-4b50-ba0a-6b1b14721f77
caps.latest.revision: "34"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e39a53fdfa7e377ea1b8cf04897f946e5b543ca8
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="syssyscurconfigs-transact-sql"></a>sys.syscurconfigs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含每個目前組態選項各一個項目。 同時，此檢視表含有描述組態結構的四個項目。 **syscurconfigs** ，會動態建立當使用者查詢。 如需詳細資訊，請參閱[sys.sysconfigures &#40;TRANSACT-SQL &#41;](../../relational-databases/system-compatibility-views/sys-sysconfigures-transact-sql.md).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
||  
|-|  
|**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。|  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**值**|**int**|使用者可以修改的變數值。 只有在執行 RECONFIGURE 時，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 才會使用這個項目。|  
|**組態**|**smallint**|組態變數號碼。|  
|**註解**|**nvarchar(255)**|組態選項的說明。|  
|**status**|**smallint**|指出選項狀態的點陣圖。 可能的值如下：<br /><br /> 0 = 靜態。 設定在伺服器重新啟動時生效。<br /><br /> 1 = 動態。 變數在執行 RECONFIGURE 陳述式時生效。<br /><br /> 2 = 進階。 會顯示變數時，才**顯示進階選項**設定。<br /><br /> 3 = 動態和進階。|  
  
## <a name="see-also"></a>請參閱＜  
 [將系統資料表對應至系統檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [相容性檢視 &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
