---
title: 發行者到散發者記錄 (交易式 - SSMS)
description: 描述 SQL Server Management Studio (SSMS) 中交易式發行集複寫監視器的 [發行者到散發者記錄] 索引標籤。
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.subscription.pubtodist.tran.f1
ms.assetid: d5a4c697-1342-49fd-8b7b-b059af32556a
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 350866a6a574469ef87586cd10f932bfcc201859
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2019
ms.locfileid: "75322179"
---
# <a name="subscription-publisher-to-distributor-history-transactional-subscription"></a>訂閱，發行者到散發者記錄 (交易式訂閱)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  **[發行者到散發者記錄]** 索引標籤會顯示關於記錄讀取器代理程式的詳細資訊，其中包括狀態、記錄、資訊性訊息，以及任何錯誤訊息。  
  
## <a name="options"></a>選項。  
 從 **[檢視]** 功能表選取要檢視的記錄讀取器代理程式工作階段，然後在標示為 **[記錄讀取器代理程式的工作階段]** 的方格中，選取一個特定的工作階段。 有關這個工作階段的詳細資訊，會顯示在標示為 **[所選取工作階段中的動作]** 之方格中。 如果選取的工作階段結束時發生錯誤， **[所選取之工作階段的錯誤詳細資料或訊息]** 的文字區域也會顯示。  
  
 **檢視**  
 選取要檢視的記錄讀取器代理程式工作階段。 記錄讀取器代理程式通常會連續執行，因此可能只會有一個工作階段可供檢視。  
  
 **狀態**  
 記錄讀取器代理程式的狀態。 下列清單顯示可能的狀態值：  
  
-   錯誤  
  
-   Completed  
  
-   正在重試  
  
-   執行中  
  
 **Start Time**  
 工作階段的開始時間。  
  
 **結束時間**  
 工作階段的結束時間。 如果代理程式未停止，則這個欄位是空的。  
  
 **有效期間**  
 記錄讀取器代理程式已在這個工作階段執行的時間量。 如果代理程式目前正在執行，則時間代表經過時間，如果代理程式工作階段已結束，則時間代表工作階段總共花費的時間。  
  
 **錯誤訊息**  
 如果工作階段因發生錯誤而結束，這個欄位會顯示記錄讀取器代理程式所記錄的最後錯誤訊息。 如果工作階段結束時沒有錯誤，這個欄位會是空白。  
  
 **動作訊息**  
 記錄讀取器代理程式在所選取工作階段過程中已記錄的所有參考訊息與錯誤訊息。  
  
 **動作時間**  
 執行 **[動作訊息]** 資料行所描述之動作的時間。  
  
 **[所選取之工作階段的錯誤詳細資料或訊息]**  
 唯有所選取工作階段在 **[狀態]** 資料行中顯示的值為 **[錯誤]** 時，才會顯示。 此文字區域會顯示詳細錯誤資訊和發生錯誤時所嘗試的命令。 它也會包括與錯誤相關之其他內容的連結。  
  
## <a name="see-also"></a>另請參閱  
 [啟動複寫監視器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [使用複寫監視器來檢視資訊及執行工作](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [監視複寫](../../relational-databases/replication/monitor/monitoring-replication.md)   
 [複寫代理程式概觀](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
