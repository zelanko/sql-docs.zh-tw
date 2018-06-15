---
title: 新增發行者 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.addpublisher.f1
helpviewer_keywords:
- Add Publisher dialog box
ms.assetid: 4b57e298-655f-42c2-82bc-25cdad94a194
caps.latest.revision: 23
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e00f644fd6b9088a4d454e47a3a30ae7d31345e5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32957400"
---
# <a name="add-publisher"></a>加入發行者
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **[加入發行者]** 對話方塊，可讓您將一或多個發行者加入至複寫監視器的左窗格。 加入發行者之後，選取左窗格中的發行者會在右窗格中顯示該發行者的資訊。  
  
## <a name="options"></a>選項。  
 **[加入]**  
 按一下即可選取要加入的發行者類型，可用來啟動 **[連接到伺服器]** 對話方塊。 選項包括：  
  
-   **加入 SQL Server 發行者...**  
  
     使用 **[連接到伺服器]** 對話方塊連接到發行者。  
  
-   **加入 Oracle 發行者...**  
  
     使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributor associated with the Oracle Publisher using the **Connect to Server** dialog box.  
  
-   **指定散發者，並加入其發行者...**  
  
     使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [連接到伺服器] **對話方塊，連接到與一或多個發行者相關聯的** 散發者。  
  
 順利連接到發行者或散發者之後，每個發行者及其散發者的名稱會在對話方塊頂端的方格中顯示。  
  
> [!NOTE]  
>  散發者和發行者經常在相同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上執行，但散發者也可在另一個執行個體上執行 (此組態稱為遠端散發者)。  
  
 **移除**  
 在對話方塊頂端的方格中選取發行者，然後按一下 **[移除]** 從要加入的發行者清單中移除發行者。  
  
> [!NOTE]  
>  此按鈕無法用來移除已顯示在複寫監視器中的發行者。 若要移除已顯示的發行者，請以滑鼠右鍵按一下複寫監視器之左窗格中的發行者，然後按一下 **[移除]**。  
  
 **啟動複寫監視器時自動連接**  
 選取即可讓複寫監視器自動連接到散發者，並擷取在對話方塊頂端方格中選取之發行者的狀態資訊。 如果清除此核取方塊，您必須在啟動複寫監視器後手動連接：以滑鼠右鍵按一下複寫監視器之左窗格中的發行者，然後按一下 **[連接]**。  
  
 **自動重新整理此發行者和其發行集的狀態**  
 選取即可讓複寫監視器自動重新整理在對話方塊頂端方格中選取之發行者的狀態。 如果選取此選項，複寫監視器就會輪詢散發者，以取得發行者和其發行集的狀態資訊。 輪詢間隔會由 **[重新整理的頻率]** 選項設定。 如需複寫監視器中之重新整理的詳細資訊，請參閱[快取、重新整理和複寫監視器效能](../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md)。  
  
 **[重新整理的頻率]**  
 輸入一個值 (以秒為單位)，來指定複寫監視器應輪詢散發者以取得狀態的頻率。 較低的值會產生較頻繁的輪詢，如果您監視大量的發行者，這會影響散發者端的效能。 建議您測試自己的系統，以決定適當的值。 如果您在複寫監視器的任何一個詳細資料視窗中選取 **[自動重新整理]** ，也會使用 **[重新整理的頻率]** 設定。  
  
 **在下列群組中顯示此發行者**  
 從清單中選取一個發行者群組。 發行者會在左窗格中的這個群組之下顯示。 群組提供組織發行者的一種方式，對於複寫的運作方式沒有影響。 如果沒有定義任何群組或想要建立新的群組，請按一下 **[新增群組]**。  
  
 **[新增群組]**  
 按一下即可建立新的發行者群組。 發行者群組提供在複寫監視器內組織發行者的一種便利方式。 群組不會影響資料的複寫，也不會影響複寫拓撲中各伺服器間的關聯性。  
  
## <a name="see-also"></a>另請參閱  
 [啟動複寫監視器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [監視複寫](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
