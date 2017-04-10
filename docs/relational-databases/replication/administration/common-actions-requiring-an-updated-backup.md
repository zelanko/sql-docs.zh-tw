---
title: "需要更新之備份的常見動作 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "復原 [SQL Server 複寫], 需要備份的動作"
  - "還原 [SQL Server 複寫], 需要備份的動作"
  - "備份 [SQL Server 複寫], 需要備份的動作"
ms.assetid: a5975bf4-183e-42e3-b7d1-ad02f89d2e1d
caps.latest.revision: 32
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 32
---
# 需要更新之備份的常見動作
  如果您執行一般記錄備份，就必須在記錄備份中擷取任何複寫相關的變更。 如果您未執行記錄備份，備份發行集、 散發、 訂閱、 **msdb**, ，和 **主要** 在複寫結構描述或拓撲的修改後的資料庫。  
  
## 發行集資料庫  
 在下述動作之後備份發行集資料庫：  
  
-   建立新的發行集。  
  
-   變更包含篩選在內的任何發行集屬性。  
  
-   新增發行項 (Article) 至現有的發行集。  
  
-   執行訂閱的發行集全區重新初始化。  
  
-   在已發行的資料表上進行結構描述變更。  
  
-   執行隨指令碼執行與 [sp_addscriptexec & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql.md)。  
  
-   變更任何發行項的屬性。  
  
-   卸除發行集。  
  
-   卸除發行項。  
  
-   停用複寫。  
  
## 散發資料庫  
 在下述動作之後備份散發資料庫：  
  
-   建立或修改複寫代理程式設定檔。  
  
-   修改複寫代理程式設定檔參數。  
  
-   變更發送訂閱的複寫代理程式屬性 (包括排程)。  
  
-   由自動識別範圍管理功能指派新的識別範圍。  
  
## 訂閱資料庫  
 在下述動作之後備份訂閱資料庫：  
  
-   變更訂閱的屬性。  
  
-   變更「發行者」端合併訂閱的優先權。  
  
-   卸除訂閱。  
  
-   停用複寫。  
  
## msdb 資料庫  
 備份 **msdb** 於適當的節點之後的系統資料庫︰  
  
-   啟用或停用複寫。  
  
-   新增或卸除散發資料庫 (於「散發者」處)。  
  
-   啟用或停用發行所使用的資料庫 (於「發行者」處)。  
  
-   建立或修改複寫代理程式設定檔 (於「散發者」處)。  
  
-   修改複寫代理程式設定檔參數 (於「散發者」處)。  
  
-   變更發送訂閱的複寫代理程式屬性 (包括排程) (於「散發者」處)。  
  
-   變更提取訂閱的複寫代理程式屬性 (包括排程) (於「訂閱者」處)。  
  
-   建立與使用可轉換訂閱的交易式發行集相關聯的 DTS 封裝 (於「散發者」和「訂閱者」端)。  
  
-   新增或卸除可轉換訂閱 (於「散發者」和「訂閱者」端)。  
  
## master 資料庫  
 備份 **主要** 於適當的節點之後的系統資料庫︰  
  
-   啟用或停用複寫。  
  
-   新增或卸除散發資料庫 (於「散發者」處)。  
  
-   啟用或停用發行所使用的資料庫 (於「發行者」處)。  
  
-   在任何資料庫中新增第一個或卸除最後一個發行集 (於「發行者」處)。  
  
-   在任何資料庫中新增第一個或卸除最後一個訂閱 (於「訂閱者」處)。  
  
-   啟用或停用「散發發行者」的「發行者」(於「發行者」及「散發者」處)。  
  
## 另請參閱  
 [SQL Server 資料庫的備份與還原](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [備份及還原複寫的資料庫](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)  
  
  