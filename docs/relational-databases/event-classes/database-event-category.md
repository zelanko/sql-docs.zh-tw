---
title: "Database 事件類別目錄 | Microsoft Docs"
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
  - "事件類別 [SQL Server], 資料庫事件類別目錄"
  - "Database 事件類別目錄 [SQL Server]"
  - "SQL Server 事件類別, 資料庫事件類別目錄"
ms.assetid: b61af738-f144-4992-b0b2-d44cb7240991
caps.latest.revision: 30
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 30
---
# Database 事件類別目錄
  **Database** 事件類別目錄包含用來監視 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的事件類別。  
  
## 本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[Data File Auto Grow 事件類別](../../relational-databases/event-classes/data-file-auto-grow-event-class.md)|表示資料檔案自動成長。 如果以外顯方式透過 ALTER DATABASE 讓資料檔案成長，則不會觸發這個事件。|  
|[Data File Auto Shrink 事件類別](../../relational-databases/event-classes/data-file-auto-shrink-event-class.md)|指出資料檔案已壓縮。|  
|[資料庫鏡像連接事件類別](../../relational-databases/event-classes/database-mirroring-connection-event-class.md)|為報告資料庫鏡像的傳輸連接狀態而產生的事件。|  
|[Database Mirroring State Change 事件類別](../../relational-databases/event-classes/database-mirroring-state-change-event-class.md)|指出鏡像資料庫的狀態何時變更。|  
|[Database Suspect Data Page 事件類別](../../relational-databases/event-classes/database-suspect-data-page-event-class.md)|指出頁面何時加入至 **msdb** 資料庫中的 **suspect_pages** 資料表。|  
|[Log File Auto Grow 事件類別](../../relational-databases/event-classes/log-file-auto-grow-event-class.md)|表示記錄檔自動成長。 如果以外顯方式透過 ALTER DATABASE 讓記錄檔增長，則不會觸發這個事件。|  
|[Log File Auto Shrink 事件類別](../../relational-databases/event-classes/log-file-auto-shrink-event-class.md)|表示記錄檔自動成長。 如果透過 ALTER DATABASE 來明確壓縮記錄檔，則不會觸發此事件。|  
  
## 另請參閱  
 [擴充事件](../../relational-databases/extended-events/extended-events.md)  
  
  