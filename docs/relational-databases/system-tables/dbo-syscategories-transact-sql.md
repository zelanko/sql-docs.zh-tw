---
title: "dbo.syscategories (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.syscategories_TSQL
- syscategories
- syscategories_TSQL
- dbo.syscategories
dev_langs: TSQL
helpviewer_keywords: syscategories system table
ms.assetid: eb2cb75c-dc58-4a5b-b329-664e9fe20ce0
caps.latest.revision: "27"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c61063d79e64cbd5350caad5eb374b12f028fa5c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="dbosyscategories-transact-sql"></a>dbo.syscategories (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 用來組織作業、警示和運算子的類別目錄。 這份資料表儲存在**msdb**資料庫。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|類別目錄識別碼|  
|**category_class**|**int**|類別目錄中的項目類型：<br /><br /> **1** = 作業<br /><br /> **2** = 警示<br /><br /> **3** = 運算子|  
|**category_type**|**tinyint**|類別目錄類型：<br /><br /> **1** = 本機<br /><br /> **2** = 多伺服器<br /><br /> **3** = 無|  
|**name**|**sysname**|類別目錄的名稱|  
  
  
