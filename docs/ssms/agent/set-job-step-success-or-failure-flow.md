---
title: 設定作業步驟成功或失敗的流程 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, action flow logic
- successful jobs [SQL Server]
- failed jobs [SQL Server]
- jobs [SQL Server Agent], action flow logic
ms.assetid: 23041ccf-8a07-41d3-85b9-c449a54b7e1e
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c14f10c9bba7dbdd40c1e2554fb590cd6f814043
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65105986"
---
# <a name="set-job-step-success-or-failure-flow"></a>設定作業步驟成功或失敗的流程
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

建立 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業時，您可以指定作業執行期間發生失敗時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 應採取什麼動作。 決定每個作業步驟成功或失敗時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 應採取的動作。 接著，依照下列程序使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 來設定作業步驟動作流程。  
  
-   **開始之前：**  
  
    [安全性](#Security)  
  
-   **若要使用下列項目，設定作業步驟成功或失敗的流程：**  
  
    [Transact-SQL](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server 管理物件](#SMO)  
  
## <a name="before-you-begin"></a>開始之前  
  
### <a name="Security"></a>Security  
如需詳細資訊，請參閱＜ [實作 SQL Server Agent 安全性](../../ssms/agent/implement-sql-server-agent-security.md)＞。  
  
## <a name="SSMS"></a>使用 SQL Server Management Studio  
  
#### <a name="to-set-job-step-success-or-failure-flow"></a>若要設定作業步驟成功或失敗的流程  
  
1.  在 **[物件總管]** 中，展開 **[SQL Server Agent]**，然後展開 **[作業]**。  
  
2.  以滑鼠右鍵按一下要刪除的作業，然後按一下 [屬性]。  
  
3.  按一下 **[步驟]** 頁面，再按一下步驟，然後按一下 **[編輯]**。  
  
4.  在 **[作業步驟屬性]** 對話方塊中，選取 **[進階]** 頁面。  
  
5.  在 [成功時的動作] 清單中，按一下作業步驟順利完成時要執行的動作。  
  
6.  在 **[重試次數]** 方塊中，輸入介於 0 到 9999 間的值，此值是當發生作業步驟失敗前應該重試的次數。 如果在 [重試次數] 方塊中指定大於 0 的值，請在 [重試間隔 (分鐘)] 方塊內輸入 1 至 9999 間的分鐘數，此值為作業步驟在重試前所應等待的時間。  
  
7.  在 **[當動作失敗時]** 清單中，按一下當作業步驟失敗時要執行的動作。  
  
8.  如果作業是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼，您可以從下列選項中選擇：  
  
    -   在 **[輸出檔]** 方塊中，輸入要寫入指令碼輸出的輸出檔名稱。 根據預設，每次執行作業步驟時都會覆寫此檔案。 如果您不想要覆寫輸出檔，請選取 **[將輸出附加至現有檔案]**。  
  
    -   若要將作業步驟記錄至資料庫資料表，請選取 **[記錄至資料表]** 。 根據預設，每次執行作業步驟時都會覆寫此資料表內容。 如果您不想要覆寫資料表內容，請選取 **[將輸出附加至資料表的現有項目]**。 作業步驟執行之後，您可以按一下 **[檢視]** 以檢視這個資料表的內容。  
  
    -   如果您希望步驟的記錄中包含輸出，請選取 **[包含步驟輸出於記錄中]** 。 只有無錯誤時，才會顯示輸出。 另外，輸出可能被截斷。  
  
9. 若 **[指定執行時的身分]** 清單可用，請選取具有作業將會使用之認證的 Proxy 帳戶。  
  
## <a name="TSQL"></a>使用 Transact-SQL  
  
#### <a name="to-set-job-step-success-or-failure-flow"></a>若要設定作業步驟成功或失敗的流程  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'TSQL',  
        @command = N'ALTER DATABASE SALES SET READ_ONLY',   
        @on_success_action = 1;  
    GO  
    ```  
  
如需詳細資訊，請參閱 [sp_add_jobstep (Transact-SQL)](https://msdn.microsoft.com/97900032-523d-49d6-9865-2734fba1c755)。  
  
## <a name="SMO"></a>使用 SQL Server 管理物件  
**若要設定作業步驟成功或失敗的流程**  
  
透過所選的程式語言，例如 Visual Basic、Visual C# 或 PowerShell，使用 **JobStep** 類別。 如需詳細資訊，請參閱 [SQL Server 管理物件 (SMO)](https://msdn.microsoft.com/library/ms162169.aspx)。  
  
