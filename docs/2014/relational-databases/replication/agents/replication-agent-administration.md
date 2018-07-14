---
title: 複寫代理程式管理 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Snapshot Agent, administering
- Log Reader Agent, administering
- Queue Reader Agent, administering
- shared agents [SQL Server replication]
- Merge Agent, administering
- Distribution Agent, administering
- agents [SQL Server replication], administering
- replication cleanup jobs [SQL Server]
- administering replication, agents
- replication [SQL Server], administering
- independent agents [SQL Server replication]
ms.assetid: f27186b8-b1b2-4da0-8b2b-91f632c2ab7e
caps.latest.revision: 47
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: be31b82e3ce6d2ed319d0ef293332b65e9aa1e24
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37190228"
---
# <a name="replication-agent-administration"></a>複寫代理程式管理
  複寫代理程式可執行許多有關複寫的工作，包含建立結構描述和資料的副本、偵測「發行者」或「訂閱者」端的更新，以及在伺服器之間傳播變更。 依預設，複寫代理程式在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 作業步驟之下執行。 此代理程式只不過是可執行檔，所以也可以從命令列和批次指令碼直接呼叫。 每個複寫代理程式都支援一組用於控制其執行方式的執行時期參數；這些參數在代理程式設定檔或命令列中指定。  
  
> [!IMPORTANT]  
>  依預設，安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 時會停用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 服務，除非明確選擇在安裝期間自動啟動該服務。  
  
 複寫代理程式檔案位於 [!INCLUDE[ssInstallPathVar](../../../includes/ssinstallpathvar-md.md)]\COM 之下。 下表列出了複寫的可執行檔名稱和檔案名稱。 按一下代理程式的連結以檢視其參數參考。  
  
|代理程式可執行檔|檔案名稱|  
|----------------------|---------------|  
|[複寫快照集代理程式](replication-snapshot-agent.md)|snapshot.exe|  
|[Replication Distribution Agent](replication-distribution-agent.md)|distrib.exe|  
|[複寫記錄讀取器代理程式](replication-log-reader-agent.md)|logread.exe|  
|[複寫佇列讀取器代理程式](replication-queue-reader-agent.md)|qrdrsvc.exe|  
|[Replication Merge Agent](replication-merge-agent.md)|replmerg.exe|  
  
 除了複寫代理程式外，複寫還有許多依排程和依要求來執行維護的作業。  
  
 **若要執行代理程式和維護作業**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 和複寫監視器：[啟動和停止複寫代理程式&#40;SQL Server Management Studio&#41;](start-and-stop-a-replication-agent-sql-server-management-studio.md)。  
  
-   複寫程式設計：[複寫代理程式可執行檔概念](../concepts/replication-agent-executables-concepts.md)  
  
## <a name="agent-profiles"></a>代理程式設定檔  
 設定複寫時，會在散發者上安裝一組代理程式設定檔。 代理程式設定檔包含一組參數，代理程式每次執行時都會使用這組參數：每個代理程式在啟動過程中都會登入散發者，並查詢其設定檔內的參數。 複寫為每個代理程式提供預設的設定檔，並為記錄讀取代理程式、散發代理程式及合併代理程式提供其他預先定義的設定檔。 除了提供的設定檔之外，您也可以建立適合自己的應用程式需求的設定檔。 如需詳細資訊，請參閱 [Replication Agent Profiles](replication-agent-profiles.md)。  
  
 如需直接指定命令列參數的資訊，請參閱[複寫代理程式可執行檔概念](../concepts/replication-agent-executables-concepts.md)。  
  
## <a name="monitoring-replication-agents"></a>監視複寫代理程式  
 「複寫監視器」允許您檢視資訊並執行與每個複寫代理程式相關聯的工作。 下列清單包含每個代理程式、可以在複寫監視器上找到的索引標籤，以及到說明如何存取這些索引標籤之主題的連結：  
  
-   下列代理程式與複寫監視器中的發行集相關聯：  
  
    -   快照集代理程式  
  
    -   記錄讀取器代理程式  
  
    -   佇列讀取器代理程式  
  
     透過 **[代理程式]** 索引標籤，存取與這些代理程式相關聯的資訊和工作。如需詳細資訊，請參閱[檢視與發行集建立關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](../monitor/view-information-and-perform-tasks-for-publication-agents.md)。  
  
-   下列代理程式與複寫監視器中的訂閱相關聯：  
  
    -   散發代理程式  
  
    -   [合併代理程式]  
  
     透過下列索引標籤，存取與這些代理程式相關聯的資訊和工作： **[訂閱監看清單]** (每個發行者皆可用) 或者 **[所有訂閱]** 索引標籤 (每個發行者皆可用)。 如需詳細資訊，請參閱[檢視與訂閱建立關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](../monitor/view-information-and-perform-tasks-for-subscription-agents.md)。  
  
## <a name="independent-and-shared-agents"></a>獨立與共用的代理程式  
 獨立代理程式即服務一個訂閱的代理程式。 共用的代理程式會服務多個訂閱；如果使用相同共用代理程式的多個訂閱需要同步，依預設，它們會在佇列中等候，該共用代理程式會一次服務其中之一。 使用獨立代理程式會降低延遲，因為代理程式會在訂閱需要同步時就緒。 合併式複寫通常使用獨立代理程式，依預設，異動複寫會使用在「新增發行集精靈」中建立的發行集之獨立代理程式 (在舊版 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中，依預設，異動複寫則使用共用代理程式)。  
  
## <a name="replication-maintenance-jobs"></a>複寫維護作業  
 複寫使用下列作業執行依排程和視需要的維護。  
  
|清除作業|描述|預設排程|  
|------------------|-----------------|----------------------|  
|代理程式記錄清除：散發|從散發資料庫移除複寫代理程式的記錄。|每 10 分鐘執行|  
|散發清除：散發|從散發資料庫移除複寫的交易。 停用在最長散發保留期限內未同步的訂閱。|每 10 分鐘執行|  
|到期的訂閱清除|偵測並移除散發資料庫中到期的訂閱。|每天早上 1:00 執行|  
|重新初始化資料驗證失敗的訂閱|偵測使資料驗證失敗的所有訂閱，並將其標示為重新初始化。 下次「合併代理程式」或「散發代理程式」執行時，將在「訂閱者」端套用新的快照集。|沒有預設排程 (依預設值未啟動)|  
|複寫代理程式檢查|偵測並未動態記錄歷程的複寫代理程式。 如果作業步驟失敗，則其會寫入 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 事件記錄檔。|每十分鐘執行一次。|  
|散發的複寫監視重新整理器|重新整理「複寫監視器」使用的快取查詢。|連續執行。|  
  
## <a name="see-also"></a>另請參閱  
 [監視複寫](../monitoring-replication.md)  
  
  
