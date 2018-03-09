---
title: "啟動複寫監視器 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Replication Monitor, starting
ms.assetid: e037bd27-cc87-4ee9-9e5f-83f6d717cfa4
caps.latest.revision: "36"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f5e9b5a38bbd6ef2468a21683b3279602edf8336
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="start-the-replication-monitor"></a>啟動複寫監視器
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 複寫監視器可以從任何 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體上的 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 啟動，也可以從命令提示字元啟動。 啟動「複寫監視器」後，將一個或多個「發行者」新增至監視器。 如需詳細資訊，請參閱 [從複寫監視器加入及移除發行者](../../../relational-databases/replication/monitor/add-and-remove-publishers-from-replication-monitor.md)。  
  
### <a name="to-start-replication-monitor-from-sql-server-management-studio"></a>從 SQL Server Management Studio 啟動複寫監視器  
  
1.  連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]執行個體，然後展開伺服器節點。  
  
2.  以滑鼠右鍵按一下 **[複寫]** 資料夾或其任何子資料夾，再按一下 **[啟動複寫監視器]**。  
  
### <a name="to-start-replication-monitor-from-the-command-prompt"></a>從命令提示字元啟動複寫監視器  
  
1.  在命令提示字元中，瀏覽至工具安裝目錄， 預設路徑為 [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]Tools\Binn\。  
  
2.  執行 sqlmonitor.exe。  
  
## <a name="see-also"></a>另請參閱  
 [監視複寫](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
