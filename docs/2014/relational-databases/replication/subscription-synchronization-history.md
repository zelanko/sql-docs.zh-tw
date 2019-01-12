---
title: 訂用帳戶，同步處理記錄 （合併訂閱，SQL Server 2005 和更新版本） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.subscription.synchhistory.f1
- sql12.rep.monitor.subscription.downlevelsynchhistory.f1
ms.assetid: 85f666f6-14ee-4f19-b385-e5cc508aabe4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 38bc4d44b988192be76ed613f52793dc2e8daefc
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54124418"
---
# <a name="subscription-synchronization-history-merge-subscription-sql-server-2005-and-later"></a>訂閱，同步處理記錄 (合併訂閱，SQL Server 2005 和更新的版本)
  **[同步處理記錄]** 索引標籤會顯示有關合併代理程式的詳細資訊，包括狀態、發行項統計資料、記錄、參考訊息和錯誤訊息等等。  
  
## <a name="options"></a>選項。  
 從 **[檢視]** 功能表中選取要檢視的合併代理程式工作階段，再於 **[合併代理程式工作階段]** 方格中選取特定的工作階段。 有關這個工作階段的詳細資訊，會顯示在標示為 **[在選取的工作階段中處理的發行項]** 的方格中。  
  
 **[檢視]**  
 選取要檢視的合併代理程式工作階段。  
  
 **狀態**  
 工作階段結束時的合併代理程式狀態。 下列清單顯示可能的狀態值：  
  
-   錯誤  
  
-   已完成  
  
-   正在重試  
  
-   執行中  
  
 **Start Time**  
 工作階段的開始時間。  
  
 **結束時間**  
 工作階段的結束時間。 如果代理程式未停止，則這個欄位是空的。  
  
 **有效期間**  
 合併代理程式在工作階段中執行的時間量。 如果代理程式目前正在執行，此時間代表經過時間；如果代理程式是先前有執行過，則此時間代表總共時間。  
  
 **已上傳的命令**  
 在合併代理程式工作階段期間，已上傳的資料列數。  
  
 **已下載命令**  
 在合併代理程式工作階段期間，已下載的資料列數。  
  
 **錯誤訊息**  
 如果工作階段結束時發生錯誤，這個欄位會顯示合併代理程式記錄的最後一個錯誤訊息。 如果工作階段結束時沒有錯誤，這個欄位會是空白。  
  
 **發行項**  
 發行集內每個發行項的名稱，以及整個發行集的下列處理階段：  
  
-   **初始化**。 這是指合併代理程式的啟動；而不是涉及套用快照集的訂閱之初始化。  
  
-   **結構描述變更及大量插入**。  
  
-   **將變更上傳至發行者**。  
  
-   **下載變更到訂閱者**。  
  
 方格中會包含這些階段，方格才能顯示所選取工作階段內、每個階段所花費時間量以及其時間量佔總時間量的百分比。  
  
 **總計的 %**  
 所選取工作階段內、每個階段所花費時間量佔總處理時間的百分比。  
  
 **有效期間**  
 每個處理階段所花費的時間量。 如果合併代理程式目前正在工作階段中執行，則時間代表經過時間，如果合併代理程式先前已執行過，則時間代表總共花費的時間。  
  
 **Inserts**  
 在所選取工作階段的此階段中插入之資料列數。  
  
 **Updates**  
 在所選取工作階段的此階段中更新之資料列數。  
  
 **Deletes**  
 在所選取工作階段的此階段中刪除之資料列數。  
  
 **衝突**  
 在所選取工作階段中的衝突數目。  
  
 **結構描述變更**  
 在所選取工作階段中的結構描述變更數目。 結構描述變更可能是因為：發行集資料庫複寫了結構描述變更；發行項的加入或卸除；以及發行項或發行集屬性的變更。  
  
 **所選取工作階段的最後訊息**  
 這個文字區域會顯示所選取工作階段的最後訊息。 如果發生錯誤，它會顯示錯誤的詳細資訊和發生錯誤時所嘗試的命令。 它也會包括與錯誤相關之其他內容的連結。  
  
## <a name="see-also"></a>另請參閱  
 [啟動複寫監視器](monitor/start-the-replication-monitor.md)   
 [檢視資訊並執行的工作，使用 「 複寫監視器](monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [監視複寫](monitoring-replication.md)   
 [複寫代理程式概觀](agents/replication-agents-overview.md)  
  
  
