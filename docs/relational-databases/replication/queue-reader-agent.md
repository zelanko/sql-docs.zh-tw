---
title: 佇列讀取器代理程式 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.queuereaderagent.f1
helpviewer_keywords:
- Queue Reader Agent dialog box
ms.assetid: f02d24b6-dcb5-4126-b56e-fab41cfe4337
caps.latest.revision: 18
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f5ec06133574580cdd2c0ee42a529bcb7f631b2a
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37360074"
---
# <a name="queue-reader-agent"></a>佇列讀取器代理程式
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **[佇列讀取器代理程式]** 對話方塊會顯示佇列讀取器代理程式的詳細資訊，其中包括狀態、記錄、參考訊息以及任何錯誤訊息。  
  
## <a name="options"></a>選項。  
 從 **[檢視]** 功能表中選取要檢視之佇列讀取器代理程式的工作階段，然後在標示為 **[佇列讀取器代理程式的工作階段]** 方格中，選取特定的工作階段。 有關這個工作階段的詳細資訊，會顯示在標示為 **[所選取工作階段中的動作]** 之方格中。 如果選取的工作階段結束時發生錯誤， **[所選取之工作階段的錯誤詳細資料或訊息]** 的文字區域也會顯示。  
  
 **[檢視]**  
 選取要檢視之佇列讀取器代理程式的工作階段。 佇列讀取器代理程式通常會連續執行，因此可能只會有一個可供檢視的工作階段。  
  
 **狀態**  
 佇列讀取器代理程式的狀態。 下列清單顯示可能的狀態值：  
  
-   錯誤  
  
-   正在重試失敗的命令  
  
-   未執行  
  
-   執行中  
  
 **Start Time**  
 工作階段的開始時間。  
  
 **結束時間**  
 工作階段的結束時間。 如果代理程式未停止，則這個欄位是空的。  
  
 **有效期間**  
 佇列讀取器代理程式在這個工作階段中已執行的時間。 如果代理程式目前正在執行，則時間代表經過時間，如果代理程式工作階段已結束，則時間代表工作階段總共花費的時間。  
  
 **錯誤訊息**  
 如果工作階段因發生錯誤而結束，這個欄位就會顯示佇列讀取器代理程式所記錄的最後一個錯誤訊息。 如果工作階段結束時沒有錯誤，這個欄位會是空白。  
  
 **動作訊息**  
 在選取的工作階段期間，佇列讀取器代理程式所記錄的所有參考訊息與錯誤訊息。  
  
 **動作時間**  
 執行 **[動作訊息]** 資料行所描述之動作的時間。  
  
 **[所選取之工作階段的錯誤詳細資料或訊息]**  
 唯有所選取工作階段在 **[狀態]** 資料行中顯示的值為 **[錯誤]** 時，才會顯示。 此文字區域會顯示詳細錯誤資訊和發生錯誤時所嘗試的命令。 它也會包括與錯誤相關之其他內容的連結。  
  
## <a name="see-also"></a>另請參閱  
 [啟動複寫監視器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [檢視與發行集建立關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md)   
 [監視複寫](../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [複寫代理程式概觀](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
