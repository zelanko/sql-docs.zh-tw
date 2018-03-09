---
title: "Oracle CDC 執行個體 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: change-data-capture
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ed71e8c4-e013-4bf2-8b6c-1e833ff2a41d
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d06d4934318a045fff483e9866a72b929e69850d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="the-oracle-cdc-instance"></a>Oracle CDC 執行個體
  Oracle CDC 執行個體是由 Oracle CDC 服務建立的一種處理序，可處理從單一 Oracle 來源資料庫擷取的變更。 Oracle CDC 執行個體會從 **cdc.xdbcdc_config** 資料表擷取其組態，並在 **cdc.xdbcdc_state** 資料表中維護其狀態。 這些資料表是 CDC 資料庫的一部分 (此資料庫會定義 Oracle CDC 執行個體)。 如需有關 xdbcdc 資料庫和資料表的詳細資訊，請參閱＜ [The CDC Databases](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_CDCdatabase)＞。  
  
 以下描述 Oracle CDC 執行個體所執行的工作：  
  
-   **處理服務啟動驗證**：當啟動時，CDC 執行個體會從 **xdbcdc_config** 資料表載入其組態，並執行一系列的驗證來確保 CDC 執行個體保存的狀態一致而且可以開始處理變更。  
  
-   **準備變更擷取**：當順利通過驗證時，Oracle CDC 執行個體會掃描目前定義的所有擷取執行個體，並準備 Oracle LogMiner 查詢及變更擷取所需的其他支援結構。 此外，Oracle 執行個體會重新載入上次執行 Oracle CDC 執行個體時所儲存的內部擷取狀態。  
  
-   **從 Oracle 擷取變更**：Oracle CDC 執行個體會透過 Oracle LogMiner 功能來共用 Oracle 中的變更、根據交易認可加以排序，然後變更交易中的時間並將其寫入 CDC 資料庫中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 變更資料表。  
  
-   **處理服務關閉**：Oracle CDC 執行個體的生命週期由 Oracle CDC 服務所管理。 當系統要求 Oracle CDC 執行個體關閉時，它會執行以下工作：  
  
    -   停止讀取 Oracle 交易記錄。  
  
    -   停止將完成的 Oracle 交易寫入 CDC 資料庫。  
  
    -   必要時請等候 30 秒的時間，直到目前的交易完成寫入 CDC 資料庫為止。 如果過了 30 秒以上的時間，則會取消寫入並回復交易 (當重新啟動 CDC 執行個體時會重試)。  
  
    -   在個別執行緒中，最長可在 30 秒內盡量將許多記憶體快取的記錄寫入暫存交易資料表中 (從最舊的交易到最新的交易)，然後更新 **xdbcdc_state** 資料表並認可所有變更。  
  
-   **處理組態變更**：系統會通知 Oracle CDC 執行個體有關組態變更的消息 (從 CDC 服務或是藉由偵測 **cdc.xdbcdc_config** 資料表中的新版本)。 大多數的變更不需要重新啟動 Oracle CDC 執行個體 (例如，加入或移除擷取執行個體)。 但是，某些變更 (例如變更 Oracle 連接字串或存取認證) 確實需要重新啟動 CDC 執行個體。  
  
-   **處理復原**：當 Oracle CDC 執行個體啟動時，其內部狀態會從 **xdbcdc_state** 和 **xdbcdc_staged_transactions** 資料表中還原。 還原狀態之後，CDC 執行個體會如往常一樣繼續進行。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤處理](../../integration-services/change-data-capture/error-handling.md)  
  
  
