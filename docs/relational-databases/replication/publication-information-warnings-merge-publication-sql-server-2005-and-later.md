---
title: "發行集資訊-警告-合併式發行集-SQL Server 2005+ | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.monitor.publicationinfo.warningsandagents.merge.f1
ms.assetid: 9bef3565-5f13-42ac-8723-ebe55b0c11e6
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 943f84af82aca8829571243927adf6dc4799ad96
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="publication-information-warnings-merge-publication-sql-server-2005-and-later"></a>發行集資訊，警告 (合併式發行集，SQL Server 2005 和更新的版本)
  執行 **和更新版本的散發者可以使用** [警告] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 索引標籤。 **[警告]** 索引標籤可以讓您針對選取的發行集執行下列工作：  
  
-   啟用警告。  
  
-   指定與警告相關聯的臨界值。  
  
-   定義與警告相關聯的警示。  
  
## <a name="warnings-thresholds-and-alerts"></a>警告、臨界值和警示  
 根據預設，複寫監視器會針對未初始化的訂閱顯示警告： **[未初始化的訂閱]** 狀態會在包含訂閱資訊之頁面的 **[狀態]** 資料行中顯示為警告。 針對合併式發行集，您可以指定這些其他的條件是否會導致警告：  
  
-   即將發生訂閱過期。  
  
     這會對應至 **[若訂閱將在臨界值內過期，就發出警告]**選項。 如果達到或超出指定的臨界值，訂閱狀態會顯示為 **[即將過期/已過期]** (除非必須顯示具有更高優先權的問題)。  
  
-   超過指定的同步處理時間。  
  
     這會對應至 **[若撥號連接的合併長度超過臨界值，就發出警告]** 和 **[若 LAN 連接的合併長度超過臨界值，就發出警告]**選項。 可以設定這兩個臨界值，但是進行同步處理期間只會使用一個。 合併代理程式會根據連接類型套用適當的臨界值。  
  
     如果指定的臨界值符合或超過，則訂閱狀態會顯示為 **[長期執行合併]** (除非需要顯示擁有更高優先權的問題)。  
  
-   在給定時間內處理的資料列數達不到指定數目。  
  
     這會對應至 **[若撥號連接的每秒的合併資料列少於臨界值，就發出警告]** 和 **[若 LAN 連接的合併長度超過臨界值，就發出警告]**選項。 可以設定這兩個臨界值，但是進行同步處理期間只會使用一個。 合併代理程式會根據連接類型套用適當的臨界值。  
  
     如果達到或超出指定的臨界值，訂閱狀態會顯示為 **[效能嚴重不足]** (除非必須顯示更高優先權的問題)。  
  
 您啟用警告時，也會設定臨界值。 例如，若您啟用警告 **[若 LAN 連接的合併長度超過臨界值，就發出警告]**，請設定合併同步允許的時間長度上限。  
  
 除了在複寫監視器顯示警告外，達到臨界值也會觸發警示。 定義警示的方式，是按一下 **[設定警示]** ，並在 **[設定複寫警示]** 對話方塊中提供資訊。  
  
## <a name="options"></a>選項  
 **已啟用**  
 選取以啟用警告，並指定臨界值。  
  
 **警示**  
 選取以啟用所指複寫警告的警示設定。  
  
 **警告**  
 與臨界值相關聯之警告的描述。  
  
 **臨界值**  
 指定臨界值的值。  
  
 **[設定警示]**  
 在 **[警告]** 方格中選取一個資料列，然後按一下 **[設定警示]** 以啟動 **[設定複寫警示]** 對話方塊。 此對話方塊可以讓您定義與選取的臨界值和警告相關聯的警示。  
  
 **捨棄變更**  
 按一下即可捨棄對警告與臨界值所做的任何變更。  
  
> [!NOTE]  
>  按一下 **[捨棄變更]** 不會影響在 **[設定複寫警示]** 對話方塊中定義的警示。  
  
 **儲存變更**  
 按一下即可儲存對警告與臨界值所做的任何變更。  
  
## <a name="see-also"></a>另請參閱  
 [啟動複寫監視器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [檢視發行集的資訊並執行工作 &#40;複寫監視器&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [使用複寫監視器監視效能](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)   
 [監視複寫](../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [在複寫監視器中設定閾值和警告](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)  
  
  
