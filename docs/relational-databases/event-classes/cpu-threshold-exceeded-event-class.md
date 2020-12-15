---
description: CPU Threshold Exceeded 事件類別
title: CPU Threshold Exceeded 事件類別 | Microsoft 文件
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- CPU Threshold Exceeded Event Class
ms.assetid: eb106f7d-baa3-4a2b-96b2-f9fe0844057d
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e2051df175d07ea98dcccb4b3aa7b6f385fde4c0
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97420476"
---
# <a name="cpu-threshold-exceeded-event-class"></a>CPU Threshold Exceeded 事件類別
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  CPU Threshold Exceeded 事件類別會指出資源管理員偵測到某個查詢已經超過針對 REQUEST_MAX_CPU_TIME_SEC 所指定的 CPU 臨界值。  
  
> [!NOTE]  
>  這個事件的偵測間隔為五秒。 這樣會保證如果某個查詢超過指定的限制至少達五秒，就會產生事件。 不過，如果某個查詢超過指定的臨界值少於五秒，根據查詢的時間和上一次偵測清除的時間，可能會遺漏偵測。  
  
## <a name="cpu-threshold-exceeded-data-columns"></a>CPU Threshold Exceeded 資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|CPU|**int**|CPU 使用量 (以毫秒為單位)。|18|是|  
|EventClass|**int**|214|27|否|  
|EventSubClass|**int**|CPU 限制違規。|21|是|  
|GroupID|**int**|發生違規的群組識別碼。|66|是|  
|OwnerID|**int**|導致違規之處理序的 SPID。|58|是|  
|SPID|**int**|引發此事件之伺服器處理序的識別碼。<br /><br /> 注意：如果系統執行緒將 CPU 使用量驗證為背景工作，這個識別碼可能會與實際的使用者 SPID 不同。|12|是|  
|StartTime|**datetime**|引發此事件的時間。|14|是|  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
