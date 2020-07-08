---
title: 設定 SQL Server 資料庫警示 (Windows) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server], creating
ms.assetid: 65d2c5c1-921f-4eff-9ef7-149170ab61e8
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 1a4cb551f72b408210064f88e0387c2fc4f3d638
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85716886"
---
# <a name="set-up-a-sql-server-database-alert-windows"></a>設定 SQL Server 資料庫警示 (Windows)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  您可以使用系統監視器來建立警示，讓它在系統監視器計數器達到閾值時引發。 為了回應此警示，「系統監視器」可啟動某個應用程式，諸如可處理此警示狀況的自訂應用程式。 例如，您可以建立在死結數目超出特定值時引發的警示。 
  
 也可以利用 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 定義警示。 如需詳細資訊，請參閱 [警示](../../ssms/agent/alerts.md)。  
  
## <a name="set-up-a-sql-server-database-alert"></a>設定 SQL Server 資料庫警示  
  
1. 在 [效能]  視窗的瀏覽樹狀目錄中，展開 [效能記錄檔及警示]  。  
  
2. 以滑鼠右鍵按一下 [警示]  ，然後選取 [New Alert Settings (新增警示設定)]  。
  
3. 在 [New Alert Settings (新增警示設定)]  對話方塊中，鍵入新警示的名稱，然後選取 [確定]  。  
  
4. 在新警示對話方塊的 [一般]  索引標籤上，新增 [註解]  。 選取 [新增]  將計數器新增警示。  
  
     所有警示必須至少要有一個計數器。  
  
5. 從 [新增計數器]  對話方塊的 [效能物件]  清單，選取一個 SQL Server 物件。 在 [從清單選取計數器]  中，選取一個計數器。  
  
6. 若要將計數器新增警示，請選取 [新增]  。 您可以繼續新增計數器，也可以選取 [關閉]  返回新的警示對話方塊。  
  
7. 在新警示對話方塊的 [達到這個值就發出警示]  清單中，選取 [超過]  或 [低於]  。 然後在 [限制]  中輸入閾值。  
  
     當計數器的值超過或低於閾值時，就會產生警示 (依據您之前選取 [超過]  或 [低於]  而定)。  
  
8. 在 [Sample data every (依下列週期進行資料取樣)]  方塊中，設定取樣頻率。  
  
9. 在 [動作]  索引標籤上，設定每次觸發警示時要採取的行動。  
  
10. 在 [排程]  索引標籤上，設定警示掃描的開始與停止排程。  
  
## <a name="see-also"></a>另請參閱  
 [建立 SQL Server 資料庫警示](../../relational-databases/performance-monitor/create-a-sql-server-database-alert.md)  
  
  
