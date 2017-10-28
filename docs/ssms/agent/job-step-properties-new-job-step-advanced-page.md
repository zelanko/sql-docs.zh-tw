---
title: "作業步驟屬性 - 新增作業步驟 (進階頁面) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ag.job.stepadvanced.f1
ms.assetid: bdecfd4f-bcd8-4ba2-8ada-fbb636314f40
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ea8ecf39a23a0db715c95bb4041c802a382822fa
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="job-step-properties---new-job-step-advanced-page"></a>作業步驟屬性 - 新增作業步驟 (進階頁面)
使用此頁面來檢視和變更 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 作業步驟的屬性。  
  
## <a name="options"></a>選項。  
**成功時的動作**  
設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 在作業步驟成功時要執行的動作。  
  
**重試次數**  
設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 嘗試重試失敗之作業步驟的次數。  
  
**重試間隔 (分鐘)**  
設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 嘗試重試之間要等候的時間。  
  
**失敗時的動作**  
設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 在作業步驟失敗時要執行的動作。  
  
## <a name="options-for-transact-sql-job-steps"></a>Transact-SQL 作業步驟的選項  
**輸出檔案**  
設定作業步驟輸出所用的檔案。 只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能使用此選項。  
  
**...**  
瀏覽作業步驟輸出所用的檔案。  
  
**檢視**  
在 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)]中，會停用檢視輸出檔的這個按鈕。 而改用 [記事本] 來檢視作業步驟輸出檔。  
  
**將輸出附加至現有檔案**  
將輸出附加至現有的檔案內容。 否則，每次執行作業步驟時會覆寫先前的檔案內容。  
  
**記錄至資料表**  
將作業步驟輸出記錄至 **msdb** 資料庫中的 **sysjobstepslogs** 資料表。  
  
**[檢視]**  
至少執行一次作業步驟之後，按一下 [檢視] 即可在資料表中檢視其輸出。  
  
**將輸出附加至資料表的現有項目**  
將輸出附加至現有的資料表內容。 否則，每次執行作業步驟時會覆寫先前的資料表內容。  
  
**包含步驟輸出於記錄中**  
選取此選項即可將作業步驟的輸出包含於作業記錄中。  
  
**指定執行時的身分**  
如果您是 **系統管理員 (sysadmin)** 固定伺服器角色的成員，就可以選取另一個 SQL 登入來執行此作業步驟。  
  
## <a name="options-for-operating-system-cmdexec-job-steps"></a>作業系統 (CmdExec) 作業步驟的選項  
**輸出檔案**  
設定作業步驟輸出所用的檔案。  
  
**...**  
瀏覽作業步驟輸出所用的檔案。  
  
**檢視**  
在 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)]中，會停用檢視輸出檔的這個按鈕。 而改用 [記事本] 來檢視作業步驟輸出檔。  
  
**將輸出附加至現有檔案**  
每次執行作業步驟時，將作業步驟輸出附加至先前的檔案內容。  
  
**記錄至資料表**  
將作業步驟輸出記錄至 **msdb** 資料庫中的 **sysjobstepslogs** 資料表。  
  
**[檢視]**  
至少執行一次作業步驟之後，按一下 [檢視] 即可在資料表中檢視其輸出。  
  
**將輸出附加至資料表的現有項目**  
將輸出附加至現有的資料表內容。 否則，每次執行作業步驟時會覆寫先前的資料表內容。  
  
**包含步驟輸出於記錄中**  
選取此選項即可將作業步驟的輸出包含於作業記錄中。  
  
## <a name="options-for-powershell-job-steps"></a>PowerShell 作業步驟的選項  
**輸出檔案**  
設定作業步驟輸出所用的檔案。  
  
**...**  
瀏覽作業步驟輸出所用的檔案。  
  
**檢視**  
在 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)]中，會停用檢視輸出檔的這個按鈕。 而改用 [記事本] 來檢視作業步驟輸出檔。  
  
**將輸出附加至現有檔案**  
每次執行作業步驟時，將作業步驟輸出附加至先前的檔案內容。  
  
**記錄至資料表**  
將作業步驟輸出記錄至 **msdb** 資料庫中的 **sysjobstepslogs** 資料表。  
  
**[檢視]**  
至少執行一次作業步驟之後，按一下 [檢視] 即可在資料表中檢視其輸出。  
  
**將輸出附加至資料表的現有項目**  
將輸出附加至現有的資料表內容。 否則，每次執行作業步驟時會覆寫先前的資料表內容。  
  
**包含步驟輸出於記錄中**  
選取此選項即可將作業步驟的輸出包含於作業記錄中。  
  
## <a name="options-for-replication-queue-reader-job-steps"></a>複寫佇列讀取器作業步驟的選項  
**Server**  
設定複寫佇列讀取器作業步驟所用的伺服器。  
  
**資料庫**  
設定複寫佇列讀取器作業步驟所用的資料庫。  
  
## <a name="options-for-sql-server-analysis-services-job-steps"></a>SQL Server Analysis Services 作業步驟的選項  
**輸出檔案**  
設定作業步驟輸出所用的檔案。 只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能使用此選項。  
  
**...**  
瀏覽作業步驟輸出所用的檔案。  
  
**檢視**  
在 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)]中，會停用檢視輸出檔的這個按鈕。 而改用 [記事本] 來檢視作業步驟輸出檔。  
  
**將輸出附加至現有檔案**  
將輸出附加至現有的檔案內容。 否則，每次執行作業步驟時會覆寫先前的檔案內容。  
  
**記錄至資料表**  
將作業步驟輸出記錄至 **msdb** 資料庫中的 **sysjobstepslogs** 資料表。  
  
**[檢視]**  
至少執行一次作業步驟之後，按一下 [檢視] 即可在資料表中檢視其輸出。  
  
**將輸出附加至資料表的現有項目**  
將輸出附加至現有的資料表內容。 否則，每次執行作業步驟時會覆寫先前的資料表內容。  
  
**包含步驟輸出於記錄中**  
選取此選項即可將作業步驟的輸出包含於作業記錄中。  
  
## <a name="see-also"></a>另請參閱  
[管理作業步驟](../../ssms/agent/manage-job-steps.md)  
  

