---
title: SQL Server Profiler-重新執行設定（Advanced Replay 選項） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.replay.generaloptions.advanced.f1
helpviewer_keywords:
- Replay Configuration dialog box
ms.assetid: b4eb34f7-3af6-4a44-ba7e-2b8430ec3cd7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0bf91032c1514037c754fd489ac266cf68063fa4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66089725"
---
# <a name="sql-server-profiler---replay-configuration-advanced-replay-options"></a>SQL Server Profiler - 重新執行組態 (進階重新執行選項)
  在 [重新執行組態]**** 對話方塊中，使用 [進階重新執行選項]**** 索引標籤來指定如何重新執行追蹤檔案。  
  
 若要檢視這個視窗，請使用 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 開啟包含用以重新執行的適當事件之追蹤檔案或資料表。 如需詳細資訊，請參閱 [Replay Requirements](../tools/sql-server-profiler/replay-requirements.md)。 在追蹤檔案或資料表開啟期間，請在 [重新執行]**** 功能表上按一下 [啟動]****，連接到想要重新執行追蹤之 SQL Server 的執行個體，然後按一下 [進階重新執行選項]**** 索引標籤。  
  
## <a name="options"></a>選項。  
 **重新執行系統 SPID**  
 指定 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 是否重新執行系統處理序識別碼 (SPID)。  
  
 **只重新執行一個 SPID**  
 只重新執行與選取之 SPID 相關的來源追蹤檔案中的活動。  
  
 **要重新執行的 SPID**  
 指定要重新執行的 SPID。  
  
 **依日期和時間限制重新執行**  
 核取以只重新執行來源追蹤檔案的一部份。  
  
 **開始時間**  
 來源追蹤檔案中應該啟動重新執行的日期和時間。  
  
 **結束時間**  
 來源追蹤檔案中應該停止重新執行的日期和時間。  
  
 **健全狀況監視器等候間隔（秒）**  
 指定重新執行的等候間隔秒數。 預設值為 3600 秒 (1 小時)。 此設定會影響健全狀況監視器結束處理序之前，處理序可以執行的時間量。  
  
 **健全狀況監視器輪詢間隔（秒）**  
 指定重新執行期間健全狀況監視器輪詢間隔秒數。 預設值為 60 秒。 此值可以讓使用者設定健全狀況監視器輪詢是否有應結束之候選者的頻率。  
  
 **啟用 SQL Server 封鎖處理序監視器**  
 啟用搜尋已封鎖或封鎖中處理序的處理序。  
  
 **封鎖的進程監視器等候間隔（秒）**  
 設定封鎖處理序監視器搜尋已封鎖或封鎖中處理序的頻率。  
  
## <a name="see-also"></a>另請參閱  
 [重新執行追蹤資料表 &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)   
 [重新執行追蹤檔案 &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)   
 [重新執行追蹤](../tools/sql-server-profiler/replay-traces.md)  
  
  
