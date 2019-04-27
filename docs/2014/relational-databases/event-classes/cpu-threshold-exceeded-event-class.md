---
title: CPU Threshold Exceeded 事件類別 | Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- CPU Threshold Exceeded Event Class
ms.assetid: eb106f7d-baa3-4a2b-96b2-f9fe0844057d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cc8252d0049953f0958ea331015aae51fd737709
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62663481"
---
# <a name="cpu-threshold-exceeded-event-class"></a>CPU Threshold Exceeded 事件類別
  CPU Threshold Exceeded 事件類別會指出資源管理員偵測到某個查詢已經超過針對 REQUEST_MAX_CPU_TIME_SEC 所指定的 CPU 臨界值。  
  
> [!NOTE]  
>  這個事件的偵測間隔為五秒。 這樣會保證如果某個查詢超過指定的限制至少達五秒，就會產生事件。 不過，如果某個查詢超過指定的臨界值少於五秒，根據查詢的時間和上一次偵測清除的時間，可能會遺漏偵測。  
  
## <a name="cpu-threshold-exceeded-data-columns"></a>CPU Threshold Exceeded 資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|CPU|`int`|CPU 使用量 (以毫秒為單位)。|18|是|  
|EventClass|`int`|214|27|否|  
|EventSubClass|`int`|CPU 限制違規。|21|是|  
|GroupID|`int`|發生違規的群組識別碼。|66|是|  
|OwnerID|`int`|導致違規之處理序的 SPID。|58|是|  
|SPID|`int`|引發此事件之伺服器處理序的識別碼。<br /><br /> 注意:如果系統執行緒 CPU 使用量驗證為背景工作，這可能不同於實際的使用者 SPID。|12|是|  
|StartTime|`datetime`|引發此事件的時間。|14|是|  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
