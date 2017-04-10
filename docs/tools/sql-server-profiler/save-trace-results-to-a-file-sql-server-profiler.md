---
title: "將追蹤結果儲存至檔案 (SQL Server Profiler) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "儲存追蹤"
  - "追蹤 [SQL Server], 儲存"
ms.assetid: ac528747-0c19-4f3d-96f5-44c762a4abed
caps.latest.revision: 23
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 23
---
# 將追蹤結果儲存至檔案 (SQL Server Profiler)
  本主題描述如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，將追蹤結果儲存至檔案。  
  
### 若要將追蹤結果儲存至檔案  
  
1.  在 [檔案] 功能表上按一下 [新增追蹤]，然後連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。  
  
     會出現 [追蹤屬性] **[追蹤屬性]**對話方塊。  
  
    > [!NOTE]  
    >  如果選取 [進行連接後立即啟動追蹤]，將不會顯示 [追蹤屬性] 對話方塊，而是會開始追蹤。 在 [工具] 功能表上，按一下 [選項]，並清除 [進行連接後立即啟動追蹤] 核取方塊，以關閉這項設定。  
  
2.  在 **[追蹤名稱]** 方塊中，輸入追蹤的名稱。  
  
3.  選取 [儲存至檔案] 核取方塊。  
  
     [另存新檔] 對話方塊隨即出現。  
  
4.  在 [另存新檔] 對話方塊中指定路徑和檔名。 按一下 **[儲存].**  
  
    > [!NOTE]  
    >  請確定 SQL Server 服務具有足夠的權限，可將檔案寫入指定的目錄。  
  
5.  在 [追蹤屬性] 對話方塊的 [設定最大檔案大小 (MB)] 文字方塊中，輸入最大檔案大小。 預設值為 5 MB。  
  
6.  (選擇性) 指定下列選項：  
  
    -   選取 [啟用檔案換用] 核取方塊，讓 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 一旦達到最大檔案大小時，便會建立新的追蹤資料檔案。 預設會選取此選項。  
  
    -   選取 [伺服器處理追蹤資料] 核取方塊，以確定伺服器會記錄每一個追蹤事件。  
  
        > [!NOTE]  
        >  清除 [伺服器處理追蹤資料] 時，如果記錄事件會明顯降低效能，伺服器就不會記錄事件。  
  
## 另請參閱  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  