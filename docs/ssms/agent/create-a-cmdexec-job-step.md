---
title: 建立 CmdExec 作業步驟 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- CmdExec jobs
ms.assetid: b48da5b4-6fe7-4eb7-bade-dc7d697c6d5c
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: bdbe0bc11354088f4db181ccc4c21ab6b295a13b
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="create-a-cmdexec-job-step"></a>建立 CmdExec 作業步驟
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

此主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]、[!INCLUDE[tsql](../../includes/tsql_md.md)] 或 SQL Server 管理物件，在 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 中建立和定義 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 作業步驟，來使用可執行程式或作業系統命令。  
  
**本主題內容**  
  
-   **開始之前：**  
  
    [Security](#Security)  
  
-   **若要使用下列項目建立 CmdExec 作業步驟：**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server 管理物件](#SMO)  
  
## <a name="BeforeYouBegin"></a>開始之前  
  
### <a name="Security"></a>Security  
根據預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員可以建立 CmdExec 作業步驟。 這些作業步驟會以 SQL Server Agent 服務帳戶的身分執行，除非 **系統管理員 (sysadmin)** 使用者建立 Proxy 帳戶。 如果使用者不是 **系統管理員 (sysadmin)** 角色的成員，則必須能夠存取 CmdExec Proxy 帳戶，才能建立 CmdExec 作業步驟。  
  
#### <a name="Permissions"></a>Permissions  
如需詳細資訊，請參閱＜ [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)＞。  
  
## <a name="SSMS"></a>使用 SQL Server Management Studio  
  
#### <a name="to-create-a-cmdexec-job-step"></a>建立 CmdExec 作業步驟  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的執行個體，然後展開該執行個體。  
  
2.  展開 **SQL Server Agent**，建立新作業或以滑鼠右鍵按一下現有作業，然後按一下 [屬性]。  
  
3.  在 **[作業屬性]** 方塊中，按一下 **[步驟]** 頁面，然後按一下 **[新增]**。  
  
4.  在 **[新增作業步驟]** 對話方塊中，輸入一個作業 **步驟名稱**。  
  
5.  在 [類型] 清單中，選擇 [作業系統 (CmdExec)]。  
  
6.  在 **[執行身分]** 清單中，選取具有作業將會使用之認證的 Proxy 帳戶。 根據預設，CmdExec 作業步驟會以 SQL Server Agent 服務帳戶的身分執行。  
  
7.  在 **[成功命令的處理序結束碼]** 方塊中，輸入介於 0 到 999999 之間的值。  
  
8.   在 [命令]方塊中，輸入作業系統命令或可執行的程式。 如需範例，請參閱＜使用 Transact-SQL＞。  
  
9. 按一下 **[進階]** 頁面設定作業步驟選項，例如：作業步驟成功或失敗時要採取什麼動作、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 應該嘗試執行作業步驟多少次，以及可供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 寫入作業步驟輸出的檔案。 只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，可以將作業步驟輸出寫入作業系統檔案。  
  
## <a name="TSQL"></a>使用 Transact-SQL  
  
#### <a name="to-create-a-cmdexec-job-step"></a>建立 CmdExec 作業步驟  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    -- creates a job step that that uses CmdExec  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'CMDEXEC',  
        @command = C:\clickme_scripts\SQL11\PostBOLReorg GetHsX.exe',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    ```  
  
如需詳細資訊，請參閱 [sp_add_jobstep (Transact-SQL)](http://msdn.microsoft.com/en-us/97900032-523d-49d6-9865-2734fba1c755)  
  
## <a name="SMO"></a>使用 SQL Server 管理物件  
**建立 CmdExec 作業步驟**  
  
透過所選的程式語言，例如 Visual Basic、Visual C# 或 PowerShell，使用 **JobStep** 類別。  
  
