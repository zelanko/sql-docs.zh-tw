---
title: "設定 SQL Server 資料庫警示 (Windows) | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- alerts [SQL Server], creating
ms.assetid: 65d2c5c1-921f-4eff-9ef7-149170ab61e8
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8eabe827b89c3931523bda848e01471853cbde6b
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="set-up-a-sql-server-database-alert-windows"></a>設定 SQL Server 資料庫警示 (Windows)
  您可以使用「系統監視器」來建立警示，在達到「系統監視器」計數器的臨界值時引發警示。 為了回應此警示，「系統監視器」可啟動某個應用程式，諸如可處理此警示狀況的自訂應用程式。 例如，您可以建立在死結數目超出特定值時引發的警示。  
  
 也可以利用 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 定義警示。 如需詳細資訊，請參閱 [警示](http://msdn.microsoft.com/library/3f57d0f0-4781-46ec-82cd-b751dc5affef)。  
  
### <a name="to-set-up-a-sql-server-database-alert"></a>若要設定 SQL Server 資料庫警示  
  
1.  在 [效能] 視窗的巡覽樹狀目錄上，展開 [效能記錄檔及警示]。  
  
2.  以滑鼠右鍵按一下 [警示]，然後按一下 [New Alert Settings (新增警示設定)]。  
  
3.  在 [New Alert Settings (新增警示設定)] 對話方塊中，輸入新警示的名稱，然後按一下 [確定]。  
  
4.  在新警示對話方塊的 [一般] 索引標籤上，加入 [註解]，按一下 [新增] 將計數器加入警示中。  
  
     所有警示必須至少要有一個計數器。  
  
5.  在 [新增計數器] 對話方塊中，從 [效能物件] 清單選取 SQL Server 物件，然後在 [從清單選取計數器] 中選取計數器。  
  
6.  若要將計數器加入警示中，請按一下 [新增]。 您可以繼續加入計數器，也可以按一下 [關閉] 返回新的警示對話方塊。  
  
7.  在新的警示對話方塊中，與 [Alert when the value is (達到這個值就發出警示)] 清單中按一下 [超過] 或 [低於]，然後在 [限制] 中輸入臨界值。  
  
     當計數器的值超過或低於臨界值時，就會產生警示 (依據您之前按一下 [超過] 或 [低於] 而定)。  
  
8.  在 [Sample data every (依下列週期進行資料取樣)] 方塊中，設定取樣頻率。  
  
9. 在 [動作] 索引標籤上，設定每次觸發警示時要採取的行動。  
  
10. 在 [排程] 索引標籤上，設定警示掃描的開始與停止排程。  
  
## <a name="see-also"></a>另請參閱  
 [建立 SQL Server 資料庫警示](../../relational-databases/performance-monitor/create-a-sql-server-database-alert.md)  
  
  
