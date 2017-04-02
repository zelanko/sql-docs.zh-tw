---
title: "啟動複寫監視器 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "複寫監視器, 啟動"
ms.assetid: e037bd27-cc87-4ee9-9e5f-83f6d717cfa4
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# 啟動複寫監視器
  「複寫監視器」可以從任何 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 執行個體上的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 啟動，也可以從命令提示字元啟動。 啟動「複寫監視器」後，將一個或多個「發行者」新增至監視器。 如需詳細資訊，請參閱 [新增和移除 「 發行者 」 從 「 複寫監視器](../../../relational-databases/replication/monitor/add-and-remove-publishers-from-replication-monitor.md)。  
  
### 從 SQL Server Management Studio 啟動複寫監視器  
  
1.  連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 執行個體，然後展開伺服器節點。  
  
2.  以滑鼠右鍵按一下 **複寫** 資料夾或任何它的子資料夾，然後再按一下 **啟動複寫監視器**。  
  
### 從命令提示字元啟動複寫監視器  
  
1.  在命令提示字元中，瀏覽至工具安裝目錄， 預設路徑為 [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)] Tools\Binn\。  
  
2.  執行 sqlmonitor.exe。  
  
## 另請參閱  
 [監視複寫](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  