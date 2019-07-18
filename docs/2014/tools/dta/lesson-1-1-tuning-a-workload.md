---
title: 微調工作負載 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- workloads [SQL Server], tuning
ms.assetid: 6229bf3f-1182-4bc6-8451-cedc37f4b62e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3dd87c1e2bd08ce5bb1d05e9d51d92e3f62bcc7a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66110190"
---
# <a name="tuning-a-workload"></a>微調工作負載
  您可以利用 Database Engine Tuning Advisor 來找出最好的實體資料庫設計，以改進您選擇要微調的資料庫和資料表的查詢效能。  
  
 此工作會使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 範例資料庫。 為了加強安全性，依預設，不會安裝範例資料庫。 若要安裝範例資料庫，請參閱＜ [安裝 SQL Server 範例和範例資料庫](http://sqlserversamples.codeplex.com)＞。  
  
### <a name="tune-a-workload-transact-sql-script-file"></a>微調工作負載 Transact-SQL 指令碼檔案  
  
1.  從下列步驟複製一個或多個範例 SELECT 陳述式：「A. 使用 SELECT 擷取資料列和資料行＞(在 [SELECT 範例 &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-examples-transact-sql) 中)，然後將陳述式貼入 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的查詢編輯器。 在您很容易找到的目錄中，將檔案儲存成 **MyScript.sql**。  
  
2.  啟動 Database Engine Tuning Advisor。 請參閱[啟動 Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md)。  
  
3.  在 Database Engine Tuning Advisor GUI 右窗格的 [工作階段名稱]  中，輸入 **MySession**。  
  
4.  選取 [工作負載]  的 [檔案]  ，然後按一下 [瀏覽工作負載檔案]  按鈕，來尋找您在步驟 1 儲存的 **MyScript.sql** 檔。  
  
5.  在 [工作負載分析的資料庫]  清單中選取 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]，在 [選取要微調的資料庫與資料表]  方格中選取 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]，並保留已選取的 [儲存微調記錄]  。 [工作負載分析的資料庫]  指定在微調工作負載時 Database Engine Tuning Advisor 所連接的第一個資料庫。 在微調開始之後，Database Engine Tuning Advisor 會連接到工作負載包含的 `USE DATABASE` 陳述式所指定的資料庫。  
  
6.  按一下 [微調選項]  索引標籤。您將不會設定這個練習的任何微調選項，但會花一些時間來檢閱預設的微調選項。 請按 F1 鍵來檢視這個索引標籤頁的說明。 請按一下 [進階選項]  來檢視其他微調選項。 如需這裡所顯示之微調選項的相關資訊，請按一下 [進階微調選項]  對話方塊中的 [說明]  。 請按一下 [取消]  來關閉 [進階微調選項]  對話方塊，保持選取預設的選項。  
  
7.  按一下工具列上的 **[開始分析]** 按鈕。 當 Database Engine Tuning Advisor 分析工作負載時，您可以在 [進度]  索引標籤中監視狀態。微調完成之後，會出現 [建議]  索引標籤。  
  
     如果您接收到關於微調停止日期和時間的錯誤，請檢查主要 [微調選項]  索引標籤上的 [停止時間]  。確定 [停止時間]  的日期和時間大於目前的日期和時間，必要時，請變更它們。  
  
8.  完成分析之後，在 [動作]  功能表上，按一下 [儲存建議]  ，將建議儲存成一份 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼。 在 [另存新檔]  對話方塊中，導覽到用來儲存建議指令碼的目錄，再輸入 **MyRecommendations** 檔案名稱。  
  
## <a name="summary"></a>總結  
 您已完成 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫之簡單 SELECT 陳述式工作負載的微調。 另外，Database Engine Tuning Advisor 也可以利用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 追蹤檔和資料表來作為微調工作負載。 下一項工作告訴您如何檢視和解譯練習微調結果所得出的微調建議。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [檢視微調建議](lesson-1-2-viewing-tuning-recommendations.md)  
  
  
