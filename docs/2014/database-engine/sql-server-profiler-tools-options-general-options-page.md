---
title: SQL Server Profiler-工具-選項（一般選項頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.replay.tools.generaloptions.f1
helpviewer_keywords:
- General Options dialog box
ms.assetid: a888246d-ccfe-415f-bbdc-d6adafac250a
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 7845a84c45015ba3346538030725eb2973490d9b
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84928549"
---
# <a name="sql-server-profiler---tools-options-general-options-page"></a>SQL Server Profiler-工具-選項（一般選項頁面）
  使用 [一般選項]**** 對話方塊來檢視或指定下列選項。  
  
## <a name="options"></a>選項。  
  
### <a name="display-options"></a>顯示選項  
 **字型名稱**  
 顯示追蹤期間在追蹤結果方格中所使用的字型名稱。  
  
 **字型大小**  
 顯示追蹤期間在追蹤結果方格中所使用的字型大小。  
  
 **選擇字型**  
 開啟變更字型設定值的對話方塊。  
  
 **使用地區設定顯示日期和時間值**  
 顯示此電腦之地區設定中所設定的日期和時間值。 如果未選取此選項，就會以 Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]所用的固定格式來顯示日期和時間值，其中包含毫秒。  
  
> [!NOTE]  
>  切換此核取方塊可變更時間資料行的顯示格式，例如 **StartTime** 和 **EndTime**。 但是，此操作不會變更語言事件或遠端程序呼叫 (RPC) 中的 **DateTime** 值參數。  
  
 **顯示 [持續時間] 資料行中的值 (以百萬分之一秒為單位)。**  
 以百萬分之一秒顯示追蹤的 [持續時間]**** 資料行中的值。 依預設，[持續時間]**** 資料行會以毫秒為單位顯示值。  
  
### <a name="tracing-options"></a>追蹤選項  
 **進行連接後立即啟動追蹤**  
 建立連接後立即使用預設範本開始追蹤。  
  
 **提供者版本變更時，更新追蹤定義**  
 更新提供者時，將最新追蹤定義套用至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。 依預設，不會核取此項目。 這會強制 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 查詢伺服器的追蹤定義並在磁碟上重新建立 (如果已存在) 檔案。  
  
### <a name="file-rollover-options"></a>檔案換用選項  
 **依序載入所有換用檔案，不另外提示**  
 開啟追蹤檔案時自動載入換用檔案。 如果在追蹤時建立多個檔案，則選取此選項會自動載入所有的換用檔案。  
  
 **載入換用檔案之前先提示**  
 在開啟追蹤檔案時，讓 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 在加入換用檔案之前給您提示。  
  
 **永不載入後續的換用檔案**  
 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 開啟追蹤檔案時，永不載入後續的換用檔案。  
  
### <a name="replay-options"></a>重新執行選項  
 **預設重新執行執行緒數目**  
 指定要同時使用的重新執行執行緒的數目。 數字愈高會在重新執行時使用愈多資源，但是會增加重新執行並行。  
  
 **預設健全狀況監視器等候間隔 (秒)**  
 指定重新執行的等候間隔秒數。 預設值為 3600 秒 (1 小時)。 此設定會影響允許執行緒執行的時間量，超過之後會被健全狀況監視器結束。  
  
 **預設健全狀況監視器輪詢間隔 (秒)**  
 指定重新執行期間健全狀況監視器輪詢間隔秒數。 預設值為 60 秒。 此值可以讓使用者設定健全狀況監視器輪詢是否有應結束之候選者的頻率。  
  
## <a name="see-also"></a>另請參閱  
 [連接到伺服器 &#40;SQL Server Profiler 後，自動啟動追蹤&#41;](../tools/sql-server-profiler/start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)   
 [設定追蹤顯示預設值 &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)   
 [重新執行追蹤資料表 &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)   
 [重新執行追蹤檔案 &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)   
 [重新執行追蹤](../tools/sql-server-profiler/replay-traces.md)   
 [&#40;SQL Server Profiler 設定全域追蹤選項&#41;](../tools/sql-server-profiler/set-global-trace-options-sql-server-profiler.md)   
 [SQL Server Profiler 範本和權限](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
