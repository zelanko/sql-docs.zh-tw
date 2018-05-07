---
title: dbo.sysdownloadlist (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dbo.sysdownloadlist
- sysdownloadlist_TSQL
- dbo.sysdownloadlist_TSQL
- sysdownloadlist
dev_langs:
- TSQL
helpviewer_keywords:
- sysdownloadlist system table
ms.assetid: 71087a4c-e829-488e-aa7d-a9476e2b4779
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4390fe628a879b36b42ffd1a3c3209e910eb125c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="dbosysdownloadlist-transact-sql"></a>dbo.sysdownloadlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  存放所有目標伺服器的下載指示佇列。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|提供資料列自然插入順序的識別欄位。|  
|**source_server**|**sysname**|來源伺服器的名稱。|  
|**operation_code**|**tinyint**|作業的作業碼：<br /><br /> **1** = INS (INSERT)<br /><br /> **2** = UPD （更新）<br /><br /> **3** = DEL (DELETE)<br /><br /> **4** = 啟動<br /><br /> **5** = 停止|  
|**object_type**|**tinyint**|物件類型碼。|  
|**object_id** <sup>1</sup>|**uniqueidentifier**|物件識別碼。|  
|**target_server**|**sysname**|目標伺服器的名稱。|  
|**error_message**|**nvarchar(1024)**|當目標伺服器處理特定資料列而發現錯誤時，所出現的錯誤訊息。|  
|**date_posted**|**datetime**|作業公佈到目標伺服器的日期和時間。|  
|**date_downloaded**|**datetime**|前次下載作業的日期和時間。|  
|**status**|**tinyint**|作業的狀態：<br /><br /> **0** = 尚未下載<br /><br /> **1** = 下載成功|  
|**deleted_object_name**|**sysname**|已刪除的物件名稱。|  
  
 <sup>1</sup> **object_id**資料行可以是值為 **-1**，對應於值為所有如果**operation_code**資料行是 DELETE 值。  
  
  
