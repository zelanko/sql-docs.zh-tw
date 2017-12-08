---
title: "Security Audit 事件類別目錄 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: trace-events
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- Security Audit event category [SQL Server]
- event classes [Analysis Services], security audit
- security events [Analysis Services]
ms.assetid: 9686a495-68d7-4137-8e30-2655aa519f6c
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 74ae764326058f6ccedb8edf0b781b1f93dc0d87
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="security-audit-event-category"></a>安全性稽核事件類別目錄
  [安全性稽核] 事件類別目錄具有下表所描述的事件類別。  
  
|Event Class|事件識別碼|說明|  
|-----------------|--------------|-----------------|  
|稽核登入|1|記錄啟動追蹤之後的所有新連接事件，例如，當用戶端要求連接到執行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體的伺服器時。|  
|稽核登出|2|記錄啟動追蹤之後的所有新中斷連接事件，例如當用戶端發出中斷連接命令時。|  
|Audit Server Starts and Stops|4|記錄服務的關閉、啟動與暫停活動。|  
|稽核物件權限事件|18|記錄所有物件權限之變更。|  
|稽核管理作業事件|19|記錄備份、還原、同步處理、附加、卸離、影像載入和影像儲存的伺服器作業。|  
  
 如需每個安全性稽核事件類別之相關聯資料行的資訊，請參閱 [安全性稽核資料行](../../analysis-services/trace-events/security-audit-data-columns.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [Analysis Services 追蹤事件](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  
