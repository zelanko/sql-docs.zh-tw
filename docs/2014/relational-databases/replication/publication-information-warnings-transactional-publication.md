---
title: 發行集資訊，警告（交易式發行集，SQL Server 2005 和更新版本） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publicationinfo.warningsandagents.tran.f1
ms.assetid: 4d4baf1d-d0a1-4d09-bec7-137811f43f09
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e2ab1c4be29b87e1051daa702ce40905a95e34ab
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63022003"
---
# <a name="publication-information-warnings-transactional-publication-sql-server-2005-and-later"></a>發行集資訊，警告 (交易式發行集，SQL Server 2005 和更新的版本)
  執行 **和更新版本的散發者可以使用** [警告] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 索引標籤。 **[警告]** 索引標籤可以讓您針對選取的發行集執行下列工作：  
  
-   啟用在複寫監視器中顯示警告。  
  
-   指定與警告相關聯的臨界值。  
  
-   定義與警告相關聯的警示。  
  
## <a name="warnings-thresholds-and-alerts"></a>警告、臨界值和警示  
 根據預設，複寫監視器會針對未初始化的訂閱顯示警告： **[未初始化的訂閱]** 狀態會在包含訂閱資訊之頁面的 **[狀態]** 資料行中顯示為警告。 針對交易式發行集，您可以指定下列其他狀況是否會造成警告：  
  
-   即將發生訂閱過期。  
  
     這會對應至 **[若訂閱將在臨界值內過期，就發出警告]** 選項。 如果達到或超出指定的臨界值，訂閱狀態會顯示為 **[即將過期/已過期]** (除非必須顯示具有更高優先權的問題)。  
  
-   超過指定的延遲。 這是正在發行者端認可的交易與正在訂閱者端認可的對應交易之間經過的時間量。  
  
     這會對應至 **[若延遲超過臨界值，就發出警告]** 選項。 如果達到或超出指定的臨界值，訂閱狀態會顯示為 **[效能嚴重不足]** (除非必須顯示更高優先權的問題)。 臨界值顯示在包含訂閱資訊之頁面的 **[效能]** 資料行中，也可以用來提供效能評比。 效能評比是下列其中一個值：  
  
    -   非常好  
  
    -   好  
  
    -   普通  
  
    -   差  
  
    -   重大  
  
 您啟用警告時，也會設定臨界值。 例如，若您啟用警告 **[若延遲超過臨界值，就發出警告]** ，請選取發行者端認可交易和訂閱者端認可交易之間允許的時間。  
  
 除了在複寫監視器顯示警告外，達到臨界值也會觸發警示。 定義警示的方式，是按一下 **[設定警示]** ，並在 **[設定複寫警示]** 對話方塊中提供資訊。  
  
## <a name="options"></a>選項。  
 **已啟用**  
 選取以啟用警告，並指定臨界值。  
  
 **警告**  
 與臨界值相關聯之警告的描述。  
  
 **閾值**  
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
 [啟動複寫監視器](monitor/start-the-replication-monitor.md)   
 [使用複寫監視器來檢視資訊及執行工作](monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [使用複寫監視器監視效能](monitor/monitor-performance-with-replication-monitor.md)   
 [監視複寫](monitoring-replication.md)   
 [Set Thresholds and Warnings in Replication Monitor](monitor/set-thresholds-and-warnings-in-replication-monitor.md)  
  
  
