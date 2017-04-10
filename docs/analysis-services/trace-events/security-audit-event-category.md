---
title: "安全性稽核事件類別目錄 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
helpviewer_keywords: 
  - "安全性稽核事件類別目錄 [SQL Server]"
  - "事件類別 [Analysis Services], 安全性稽核"
  - "安全性事件 [Analysis Services]"
ms.assetid: 9686a495-68d7-4137-8e30-2655aa519f6c
caps.latest.revision: 25
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 25
---
# 安全性稽核事件類別目錄
  [安全性稽核] 事件類別目錄具有下表所描述的事件類別。  
  
|Event Class|事件識別碼|說明|  
|-----------------|--------------|-----------------|  
|稽核登入|1|記錄啟動追蹤之後的所有新連接事件，例如，當用戶端要求連接到執行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的伺服器時。|  
|稽核登出|2|記錄啟動追蹤之後的所有新中斷連接事件，例如當用戶端發出中斷連接命令時。|  
|Audit Server Starts and Stops|4|記錄服務的關閉、啟動與暫停活動。|  
|稽核物件權限事件|18|記錄所有物件權限之變更。|  
|稽核管理作業事件|19|記錄備份、還原、同步處理、附加、卸離、影像載入和影像儲存的伺服器作業。|  
  
 如需每個安全性稽核事件類別之相關聯資料行的資訊，請參閱[安全性稽核資料行](../../analysis-services/trace-events/security-audit-data-columns.md)。  
  
## 請參閱＜  
 [Analysis Services 追蹤事件](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  