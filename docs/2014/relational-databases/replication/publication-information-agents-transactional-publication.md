---
title: 發行集資訊，代理程式 (交易式發行集) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publicationinfo.downlevelagents.tran.f1
ms.assetid: 38ef2f54-53bb-4053-876d-86f8f06a4519
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 68996f64bd61d96b4a2938a9711519207861fcd3
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52780360"
---
# <a name="publication-information-agents-transactional-publication"></a>發行集資訊，代理程式 (交易式發行集)
  **[代理程式]** 索引標籤會顯示所選取發行集之代理程式的摘要資訊。 所有的交易式發行集，都會顯示快照集代理程式與記錄讀取器代理程式的資訊。 已啟用佇列更新訂閱的交易式發行集，才會顯示佇列讀取器代理程式的資訊。  
  
## <a name="options"></a>選項。  
 如需代理程式的詳細資訊及其相關的工作，請以滑鼠右鍵按一下該代理程式的資料列，然後按一下捷徑功能表上的選項。 若要變更方格顯示資料的方式，請以滑鼠右鍵按一下方格，然後按一下下列其中一個選項：  
  
-   **排序**:中的一或多個資料行的排序**排序資料行** 對話方塊。  
  
-   **選擇要顯示的欄**:選取要顯示的順序來顯示它們在哪一個資料行 **[選擇資料行**] 對話方塊。  
  
-   **篩選**:篩選依據的資料行值的方格中的資料列**篩選設定** 對話方塊。  
  
-   **清除篩選**:清除方格的所有篩選設定。  
  
 篩選設定是每個方格特有的設定。 資料行選取和排序會套用至所有相同類型的方格，例如每個發行者的發行集方格。  
  
 **狀態**  
 與發行集相關聯之每個複寫代理程式的狀態。 下列清單顯示可能的狀態值：  
  
-   錯誤  
  
-   正在重試失敗的命令  
  
-   未執行  
  
-   執行中  
  
-   已完成  
  
 **代理程式**  
 與發行集相關聯之每個複寫代理程式的名稱。 散發代理程式與這個發行集的訂閱相關聯。 如需詳細資訊，請參閱[檢視與訂閱建立關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](monitor/view-information-and-perform-tasks-for-subscription-agents.md)。  
  
 **上次啟動時間**  
 代理程式上次啟動的時間。  
  
 **有效期間**  
 代理程式已執行的時間量。 如果代理程式目前正在執行，此時間代表經過時間；如果代理程式是先前有執行過，則此時間代表總共時間。  
  
 **最後一個動作**  
 最近一次代理程式執行期間執行的最後一個動作。  
  
## <a name="see-also"></a>另請參閱  
 [啟動複寫監視器](monitor/start-the-replication-monitor.md)   
 [檢視發行集的資訊並執行工作 &#40;複寫監視器&#41;](monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [檢視與發行集建立關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](monitor/view-information-and-perform-tasks-for-publication-agents.md)   
 [監視複寫](monitoring-replication.md)  
  
  
