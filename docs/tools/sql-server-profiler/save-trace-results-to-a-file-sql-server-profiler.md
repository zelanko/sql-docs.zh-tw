---
title: 將追蹤結果儲存至檔案 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: sql-server-profiler
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- saving traces
- traces [SQL Server], saving
ms.assetid: ac528747-0c19-4f3d-96f5-44c762a4abed
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e62a693466ac0de9a7ce67e9bbcbeec1c17b7af3
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/17/2018
---
# <a name="save-trace-results-to-a-file-sql-server-profiler"></a>將追蹤結果儲存至檔案 (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 本主題描述如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，將追蹤結果儲存至檔案。  
  
### <a name="to-save-trace-results-to-a-file"></a>若要將追蹤結果儲存至檔案  
  
1.  在 [檔案] 功能表上按一下 [新增追蹤]，然後連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。  
  
     會出現 [追蹤屬性] **[追蹤屬性]** 對話方塊。  
  
    > [!NOTE]  
    >  如果選取 [進行連接後立即啟動追蹤]，將不會顯示 [追蹤屬性] 對話方塊，而是開始追蹤。 於 [工具] 功能表，按一下 [選項]，並清除 [連接後立即啟動追蹤] 核取方塊，以關閉這項設定。  
  
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
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
