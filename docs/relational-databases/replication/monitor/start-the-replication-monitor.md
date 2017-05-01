---
title: "啟動複寫監視器 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Replication Monitor, starting
ms.assetid: e037bd27-cc87-4ee9-9e5f-83f6d717cfa4
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 93a7c9657f3847f9c1bd345de8ed106be2454ef2
ms.lasthandoff: 04/11/2017

---
# <a name="start-the-replication-monitor"></a>啟動複寫監視器
  「複寫監視器」可以從任何 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 執行個體上的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]啟動，也可以從命令提示字元啟動。 啟動「複寫監視器」後，將一個或多個「發行者」新增至監視器。 如需詳細資訊，請參閱 [從複寫監視器加入及移除發行者](../../../relational-databases/replication/monitor/add-and-remove-publishers-from-replication-monitor.md)。  
  
### <a name="to-start-replication-monitor-from-sql-server-management-studio"></a>從 SQL Server Management Studio 啟動複寫監視器  
  
1.  連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]執行個體，然後展開伺服器節點。  
  
2.  以滑鼠右鍵按一下 **[複寫]** 資料夾或其任何子資料夾，再按一下 **[啟動複寫監視器]**。  
  
### <a name="to-start-replication-monitor-from-the-command-prompt"></a>從命令提示字元啟動複寫監視器  
  
1.  在命令提示字元中，瀏覽至工具安裝目錄， 預設路徑為 [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]Tools\Binn\。  
  
2.  執行 sqlmonitor.exe。  
  
## <a name="see-also"></a>另請參閱  
 [監視複寫](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
