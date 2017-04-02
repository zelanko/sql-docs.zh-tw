---
title: "PreConnect:Starting 事件類別 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "PreConnect:Starting 事件類別"
ms.assetid: d43ed0ad-3dbd-42e0-9cef-8320b8d87497
caps.latest.revision: 18
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 18
---
# PreConnect:Starting 事件類別
  PreConnect:Starting 事件類別會指出 LOGON 觸發程序或資源管理員分類函數開始執行。  
  
## PreConnect:Starting 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|EventClass|**int**|215|27|否|  
|SPID|**int**|引發此事件之伺服器處理序的識別碼。|12|是|  
|EventSubClass|**int**|1 代表使用者定義的分類函數。|21|是|  
|StartTime|**datetime**|使用者定義分類函數啟動的時間。|14|是|  
|ObjectID|**int**|使用者定義之分類物件的識別碼。|22|是|  
|ObjectName|**nvarchar(256)**|使用者定義之分類函數的兩段式名稱。 例如，dbo.classifier。|34|是|  
  
## 另請參閱  
 [擴充事件](../../relational-databases/extended-events/extended-events.md)   
 [PreConnect:Completed 事件類別](../../relational-databases/event-classes/preconnect-completed-event-class.md)   
 [資源管理員](../../relational-databases/resource-governor/resource-governor.md)  
  
  