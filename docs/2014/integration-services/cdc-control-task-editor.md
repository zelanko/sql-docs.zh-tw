---
title: CDC 控制工作編輯器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdccontroltask.config.f1
ms.assetid: 4f09d040-9ec8-4aaa-b684-f632d571f0a8
caps.latest.revision: 9
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f6ce35e58b34e44690de9992f5e0296edbe4589f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37256954"
---
# <a name="cdc-control-task-editor"></a>CDC 控制工作編輯器
  使用 **[CDC 控制工作編輯器]** 對話方塊，即可設定 CDC 控制工作。 CDC 控制工作組態包括定義 CDC 資料庫的連接、CDC 工作作業，以及狀態管理資訊。  
  
 若要了解有關 CDC 控制工作的詳細資訊，請參閱＜ [CDC Control Task](control-flow/cdc-control-task.md)＞。  
  
 **若要開啟 CDC 控制工作編輯器**  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，開啟具有 CDC 控制工作的 [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] 封裝。  
  
2.  在 [控制流程] 索引標籤中，按兩下 CDC 控制工作。  
  
## <a name="options"></a>選項。  
 **SQL Server CDC 資料庫 ADO.NET 連接管理員**  
 從清單中選取現有的連接管理員，或按一下 [新增] 建立新的連接。 此連接必須指向啟用 CDC 而且包含選取之變更資料表的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫。  
  
 **CDC 控制作業**  
 選取要針對此工作執行的作業。 所有作業都會使用儲存在 SSIS 封裝變數中的狀態變數，這個變數會儲存狀態並且在封裝中的不同元件之間傳遞狀態。  
  
-   **標記初始載入開始**：此作業是在從不含快照集的使用中資料庫執行初始載入時使用。 初始載入封裝開始讀取來源資料表之前，系統會在初始載入封裝的開頭叫用此作業，以便在來源資料庫中記錄目前的 LSN。 這需要來源資料庫的連接。  
  
     如果您在 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] CDC (亦即非 Oracle) 上工作時選取了 [標記初始載入開始]，連接管理員中指定的使用者就必須是 **db_owner** 或**系統管理員**。  
  
-   **標記初始載入結束**：此作業是在從不含快照集的使用中資料庫執行初始載入時使用。 初始載入封裝讀取來源資料表完成之後，系統會在初始載入封裝的結尾叫用此作業，以便在來源資料庫中記錄目前的 LSN。 這個 LSN 的決定方式如下：記錄進行此作業時的目前時間，然後在 CDC 資料庫中查詢 `cdc.lsn_time_`mapping 資料表，尋找該時間之後發生的變更。  
  
     如果您在 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] CDC (亦即非 Oracle) 上工作時選取了 [標記初始載入結束]，連接管理員中指定的使用者就必須是 **db_owner** 或**系統管理員**。  
  
-   **標記 CDC 開始**：此作業是在從快照集資料庫或靜止資料庫進行初始載入時使用。 系統會在初始載入封裝中的任何時間點叫用此作業。 此作業所接受的參數可以是快照集 LSN、快照集資料庫的名稱 (從中自動衍生快照集 LSN)，也可以保留空白 (在此情況中，目前資料庫 LSN 就會當做變更處理封裝的啟始 LSN 使用)。  
  
     此作業是用來取代「標記初始載入開始/結束」作業。  
  
     如果您在 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] CDC (亦即非 Oracle) 上工作時選取了 [標記 CDC 開始]，連接管理員中指定的使用者就必須是 **db_owner** 或**系統管理員**。  
  
-   **取得處理範圍**：此作業是在叫用使用 CDC 來源資料流程的資料流程之前用於變更處理封裝中。 叫用此作業時，它會建立 CDC 來源資料流程所讀取的 LSN 範圍。 此範圍會儲存在資料流程處理期間 CDC 來源所使用的 SSIS 封裝變數中。  
  
     如需儲存之可能 CDC 狀態的詳細資訊，請參閱 [定義狀態變數](data-flow/define-a-state-variable.md)。  
  
-   **標記處理的範圍**：此作業是在 CDC 回合結束時 (CDC 資料流程順利完成之後) 用於變更處理封裝中，以便記錄 CDC 回合中完整處理的最後一個 LSN。 下次執行 `GetProcessingRange` 時，這個位置就會決定下一個處理範圍的開頭。  
  
-   **重設 CDC 狀態**：此作業是用來重設與目前 CDC 內容相關聯的持續性 CDC 狀態。 執行此作業之後，LSN 時間戳記 `sys.fn_cdc_get_max_lsn` 資料表中的目前最大 LSN 就會變成下一個處理範圍的範圍開頭。 此作業需要來源資料庫的連接。  
  
     此作業使用時機的範例如下：當您只想要處理新建立的變更記錄，而忽略所有舊的變更記錄時。  
  
 **包含 CDC 狀態的變數**  
 選取儲存工作作業之狀態資訊的 SSIS 封裝變數。 您應該在開始之前定義變數。 如果您選取 **[自動狀態持續性]**，系統就會自動載入並儲存狀態變數。  
  
 如需定義狀態變數的詳細資訊，請參閱 [定義狀態變數](data-flow/define-a-state-variable.md)。  
  
 **要啟動 CDC 的 SQL Server LSN/快照集名稱:**  
 輸入目前的來源資料庫 LSN 或從中執行初始載入以決定 CDC 啟動位置之快照集資料庫的名稱。 只有當 **[CDC 控制作業]** 設定為 **[標記 CDC 開始]** 時，才能使用這個選項。  
  
 如需有關這些作業的詳細資訊，請參閱＜ [CDC Control Task](control-flow/cdc-control-task.md)＞。  
  
 **自動在資料庫資料表中儲存狀態**  
 選取此核取方塊，可讓 CDC 控制工作自動在指定資料庫所包含的狀態資料表中載入並儲存 CDC 狀態。 如果沒有選取此選項，開發人員就必須在封裝啟動時載入 CDC 狀態，而且每次 CDC 狀態變更時都必須儲存狀態。  
  
 **儲存狀態之資料庫的連接管理員**  
 從清單中選取現有的 ADO.NET 連接管理員，或按一下 [新增] 建立新的連接。 這個連接會指向包含狀態資料表的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫。 狀態資料表包含狀態資訊。  
  
 只有當您已選取 **[自動狀態持續性]** 時，才能使用這個選項，而且它是必要參數。  
  
 **要用於儲存狀態的資料表**  
 輸入要用於儲存 CDC 狀態之狀態資料表的名稱。 指定的資料表必須具有兩個名為 **name** 和 **state** 的資料行，而且這兩個資料行的資料類型都必須是 **varchar (256)**。  
  
 您可以選擇性地選取 **[新增]** 取得 SQL 指令碼，以便建置含有必要資料行的新狀態資料表。 選取 **[自動狀態持續性]** 時，開發人員必須根據上述需求建立狀態資料表。  
  
 只有當您已選取 **[自動狀態持續性]** 時，才能使用這個選項，而且它是必要參數。  
  
 **狀態名稱**  
 輸入要與持續性 CDC 狀態產生關聯的名稱。 使用相同 CDC 內容的完整載入和 CDC 封裝都將指定一般狀態名稱。 這個名稱是用於查閱狀態資料表中的狀態資料列。  
  
## <a name="see-also"></a>另請參閱  
 [CDC 控制工作自訂屬性](control-flow/cdc-control-task-custom-properties.md)  
  
  
