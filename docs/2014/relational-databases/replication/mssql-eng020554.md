---
title: MSSQL_ENG020554 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG020554 error
ms.assetid: ef1a1b88-b2ab-43e8-99cd-163a973262d6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 744ab7a10db83cffa098bc97aa0ceb2c615481fd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63057118"
---
# <a name="mssqleng020554"></a>MSSQL_ENG020554
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|20554|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|複寫代理程式已有 %ld 分鐘未記錄進度訊息。 這可能表示代理程式沒有回應或系統活動量很高。 請確認記錄正在複寫至目的地，而且到訂閱者、發行者及散發者的連接仍在使用中。|  
  
## <a name="explanation"></a>說明  
 **檢查複寫代理程式** 作業將在指定間隔 (依預設為10 分鐘) 執行以檢查每個複寫代理程式的狀態。 如果代理程式自上次代理程式檢查作業執行以來未記錄任何進度訊息，則可能引發錯誤 MSSQL_ENG020554。 如果沒有發生其他複寫活動，則該代理程式必須至少記錄記錄訊息。 雖然複寫代理程式未按預期回應，但這不一定代表它已停止或失敗 (如果代理程式失敗，應引發錯誤 MSSQL_ENG020536)。  
  
 下列問題可能導致引發錯誤 MSSQL_ENG020554：  
  
-   代理程式忙碌中。  
  
     如果在受代理程式檢查作業輪詢期間，代理程式因太忙而無法作出回應，則代理程式檢查作業將無法報告複寫代理程式是否運作正常。 導致複寫代理程式忙碌的原因有很多：可能是正在複寫的資料太多，或者是應用程式設計或組態問題導致處理執行時間過長。  
  
-   代理程式無法登入拓撲中的某一台電腦。  
  
     所有代理程式均具有參數 **-LoginTimeOut** (預設設定為 15 秒)，該參數用於控制代理程式嘗試登入複寫節點所花費的時間，例如「合併代理程式」登入「發行者」。 如果設定的 **-LoginTimeOut** 值大於複寫代理程式檢查作業執行的時間間隔，則登入問題可能是導致錯誤的根本原因：錯誤 MSSQL_ENG020554 的引發會導致代理程式引發其他特定的錯誤。  
  
## <a name="user-action"></a>使用者動作  
 要求的動作視導致錯誤的原因而定：  
  
-   引發此錯誤的所有情況：  
  
     在「複寫監視器」中檢查錯誤詳細資料，然後重新啟動代理程式 (如果它已停止)。 錯誤詳細資料可能會提供有關代理程式無法正確執行之原因的額外資訊。 如果代理程式在執行，請勿停止並重新啟動代理程式，因為這樣可能會使問題惡化。 如需有關檢視代理程式狀態以及複寫監視器中的錯誤詳細資料，請參閱下列主題：  
  
    -   快照集代理程式、 記錄讀取器代理程式和佇列讀取器代理程式，請參閱[View Information and Perform Tasks 使用 「 複寫監視器](monitor/view-information-and-perform-tasks-replication-monitor.md)。  
  
    -   針對散發代理程式和合併代理程式，請參閱[View Information and Perform Tasks 使用 「 複寫監視器](monitor/view-information-and-perform-tasks-replication-monitor.md)。  
  
-   如果因代理程式正忙而頻繁出現此錯誤：  
  
     您可能需要重新設計應用程式，以縮短代理程式的處理時間。  
  
     您可以使用 **[作業屬性]** 對話方塊增加檢查代理程式狀態的間隔。 如需存取此對話方塊中，複寫作業的詳細資訊，請參閱[View Information and Perform Tasks 使用 「 複寫監視器](monitor/view-information-and-perform-tasks-replication-monitor.md)。  
  
-   如果代理程式無法登入拓撲中的某台電腦：  
  
     建議將 **-LoginTimeOut** 值設定為小於複寫代理程式檢查作業執行的時間間隔。 在某些情況下， **-LoginTimeOut** 的值之所以設定得高，是因為會導致登入逾時的網路問題。如果 **-LoginTimeOut** 設定得較低，則複寫會報告其他特定的問題，讓您可以對由權限、網路問題或其他問題導致的登入問題進行疑難排解。 可於代理程式設定檔和命令列中指定代理程式參數。 如需詳細資訊，請參閱：  
  
    -   [處理複寫代理程式設定檔](agents/replication-agent-profiles.md)  
  
    -   [檢視並修改複寫代理程式命令提示字元參數 &#40;SQL Server Management Studio&#41;](agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Replication Agent Executables Concepts](concepts/replication-agent-executables-concepts.md)的最小和最大記憶體數量。  
  
## <a name="see-also"></a>另請參閱  
 [複寫代理程式管理](agents/replication-agent-administration.md)   
 [錯誤和事件參考 &#40;複寫&#41;](errors-and-events-reference-replication.md)   
 [複寫散發代理程式](agents/replication-distribution-agent.md)   
 [複寫記錄讀取器代理程式](agents/replication-log-reader-agent.md)   
 [複寫合併代理程式](agents/replication-merge-agent.md)   
 [複寫佇列讀取器代理程式](agents/replication-queue-reader-agent.md)   
 [複寫快照集代理程式](agents/replication-snapshot-agent.md)  
  
  
