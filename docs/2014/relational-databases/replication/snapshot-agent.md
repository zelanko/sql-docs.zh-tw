---
title: 快照集代理程式 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rep.monitor.snapshotagent.f1
helpviewer_keywords:
- Snapshot Agent dialog box
ms.assetid: b715e621-2cd5-4a15-8f58-a341aa8ef5e4
caps.latest.revision: 19
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 75d39a1152138a39a676612df45e76fa0e74dbb9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023290"
---
# <a name="snapshot-agent"></a>快照集代理程式
  **[快照集代理程式]** 對話方塊會顯示快照集代理程式的詳細資訊，包括狀態、記錄、參考用訊息以及任何錯誤訊息。  
  
## <a name="options"></a>選項。  
 從 **[檢視]** 功能表選取要檢視的快照集代理程式工作階段，然後在標示為 **[快照集代理程式的工作階段]** 的方格中選取特定工作階段。 有關這個工作階段的詳細資訊，會顯示在標示為 **[所選取工作階段中的動作]** 之方格中。 如果選取的工作階段結束時發生錯誤， **[所選取之工作階段的錯誤詳細資料或訊息]** 的文字區域也會顯示。  
  
 **[檢視]**  
 選取要檢視的快照集代理程式工作階段。  
  
 **狀態**  
 快照集代理程式的狀態。 下列清單顯示可能的狀態值：  
  
-   錯誤  
  
-   正在重試失敗的命令  
  
-   未執行  
  
-   已完成  
  
 **Start Time**  
 工作階段的開始時間。  
  
 **結束時間**  
 工作階段的結束時間。 如果代理程式未停止，則這個欄位是空的。  
  
 **有效期間**  
 已經在此工作階段中執行快照集代理程式的時間量。 如果代理程式目前正在執行，則時間代表經過時間，如果代理程式工作階段已結束，則時間代表工作階段總共花費的時間。  
  
 **錯誤訊息**  
 如果工作階段以錯誤結束，則此欄位會顯示快照集代理程式記錄的最後一個錯誤訊息。 如果工作階段結束時沒有錯誤，這個欄位會是空白。  
  
 **動作訊息**  
 在選取的工作階段期間，快照集代理程式已經記錄的所有參考用訊息與錯誤訊息。  
  
 **動作時間**  
 執行 **[動作訊息]** 資料行所描述之動作的時間。  
  
 **[所選取之工作階段的錯誤詳細資料或訊息]**  
 只有當所選取工作階段在 **[狀態]** 資料行中顯示的值為 **[錯誤]** 時，才會顯示這個選項。 此文字區域會顯示詳細錯誤資訊和發生錯誤時所嘗試的命令。 它也會包括與錯誤相關之其他內容的連結。  
  
## <a name="see-also"></a>另請參閱  
 [啟動複寫監視器](monitor/start-the-replication-monitor.md)   
 [檢視與發行集建立關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](monitor/view-information-and-perform-tasks-for-publication-agents.md)   
 [監視複寫](monitoring-replication.md)   
 [複寫代理程式概觀](agents/replication-agents-overview.md)  
  
  