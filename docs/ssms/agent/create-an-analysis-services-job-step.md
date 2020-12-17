---
description: Create an Analysis Services Job Step
title: Create an Analysis Services Job Step
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.asquery.execgeneral.f1
helpviewer_keywords:
- job steps [Analysis Services]
ms.assetid: 03d4bb86-514b-4a55-97b9-c2c0fa08b428
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: e65aa07cff708a7112b7a0c4e0bbc0338cb40860
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477109"
---
# <a name="create-an-analysis-services-job-step"></a>Create an Analysis Services Job Step

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> [Azure SQL 受控執行個體](/azure/azure-sql/managed-instance/sql-managed-instance-paas-overview)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱[來自 SQL Server 的 Azure SQL 受控執行個體](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) \(部分機器翻譯\)。

此主題描述如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 SQL Server 管理物件，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中建立和定義執行 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]Analysis Services 命令與查詢的 [!INCLUDE[tsql](../../includes/tsql-md.md)] Agent 作業步驟。  
  
-   **開始之前：**  
  
    [限制事項](#Restrictions)  
  
    [安全性](#Security)  
  
-   **若要透過下列項目，建立使用 Analysis Services 命令和/或查詢的 SQL Server 作業步驟：**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server 管理物件](#SMO)  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>開始之前  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>限制事項  
  
-   如果作業步驟使用 Analysis Services 命令，命令陳述式必須是 XML for Analysis Services **Execute** 方法。 此陳述式可能不包含完整的簡易物件存取通訊協定 (SOAP) Envelope 或 XML for Analysis **Discover** 方法。 雖然 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 支援完整的 SOAP Envelope 與 **Discover** 方法，但是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業步驟則不支援。 如需有關 XML for Analysis Services 的詳細資訊，請參閱 [XML for Analysis 概觀 (XMLA)](/previous-versions/sql/)。  
  
-   如果作業步驟使用 Analysis Services 查詢，查詢陳述式必須是多維度運算式 (MDX) 查詢。 如需 MDX 的詳細資訊，請參閱 [MDX 陳述式基礎觀念 (MDX)](/analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services?viewFallbackFrom=sql-server-ver15)。  
  
### <a name="security"></a><a name="Security"></a>安全性  
  
#### <a name="permissions"></a><a name="Permissions"></a>Permissions  
  
-   若要執行使用 Analysis Services 子系統的作業步驟，使用者必須是 **系統管理員 (sysadmin)** 固定伺服器角色的成員，或具有已定義能使用此子系統之有效 Proxy 帳戶的存取權。 此外， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶或 Proxy 必須是 Analysis Services 管理員，且必須是有效的 Windows 網域帳戶。  
  
-   只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員可以將作業步驟輸出寫入檔案。 若作業步驟是由屬於 **msdb** 資料庫之 **SQLAgentUserRole** 資料庫角色 的使用者執行，則輸出只能寫入一個資料表。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會將作業步驟輸出寫入到 **msdb** 資料庫中的 **sysjobstepslog** 資料表。  
  
-   如需詳細資訊，請參閱＜ [實作 SQL Server Agent 安全性](../../ssms/agent/implement-sql-server-agent-security.md)＞。  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMS"></a>使用 SQL Server Management Studio  
  
#### <a name="to-create-an-analysis-services-command-job-step"></a>若要建立 Analysis Services 命令作業步驟  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的執行個體，然後展開該執行個體。  
  
2.  展開 **SQL Server Agent**，建立新作業或以滑鼠右鍵按一下現有作業，然後按一下 [屬性]  。 如需建立作業的詳細資訊，請參閱 [建立作業](../../ssms/agent/create-jobs.md)。  
  
3.  在 **[作業屬性]** 對話方塊中，按一下 **[步驟]** 頁面，然後按一下 **[新增]**。  
  
4.  在 **[新增作業步驟]** 對話方塊中，輸入作業 **步驟名稱**。  
  
5.  在 **[類型]** 清單中，按一下 **[SQL Server Analysis Services 命令]**。  
  
6.  在 **[執行身分]** 清單中，選取已定義為使用「Analysis Services 命令」子系統的 Proxy。 身為 **系統管理員 (sysadmin)** 固定伺服器角色成員的使用者，也可以選取 **[SQL 代理程式服務帳戶]** 來執行這個作業步驟。  
  
7.  選取將執行作業步驟的 **伺服器** ，或輸入伺服器名稱。  
  
8.  在 **[命令]** 方塊中，輸入要執行的陳述式，或按一下 **[開啟]** 選取陳述式。  
  
9. 按一下 **[進階]** 頁面以定義這個作業步驟的選項，例如在作業步驟成功或失敗時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 所該採取的行動、應該嘗試作業步驟多少次，以及應該在何處寫入作業步驟輸出。  
  
#### <a name="to-create-an-analysis-services-query-job-step"></a>若要建立 Analysis Services 查詢作業步驟  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的執行個體，然後展開該執行個體。  
  
2.  展開 **SQL Server Agent**，建立新作業或以滑鼠右鍵按一下現有作業，然後按一下 [屬性]  。 如需建立作業的詳細資訊，請參閱 [建立作業](../../ssms/agent/create-jobs.md)。  
  
3.  在 **[作業屬性]** 方塊中，按一下 **[步驟]** 頁面，然後按一下 **[新增]** 。  
  
4.  在 **[新增作業步驟]** 對話方塊中，輸入一個作業 **步驟名稱**。  
  
5.  在 **[類型]** 清單中，按一下 **[SQL Server Analysis Services 查詢]**。  
  
6.  在 **[執行身分]** 清單中，選取已定義為使用「Analysis Services 查詢」子系統的 Proxy。 身為 **系統管理員 (sysadmin)** 固定伺服器角色成員的使用者，也可以選取 **[SQL 代理程式服務帳戶]** 來執行這個作業步驟。  
  
7.  選取將執行作業步驟的 **伺服器** 與 **資料庫** ，或輸入伺服器或資料庫名稱。  
  
8.  在 **[命令]** 方塊中，輸入要執行的陳述式，或按一下 **[開啟]** 選取陳述式。  
  
9. 按一下 **[進階]** 頁面以定義這個作業步驟的選項，例如在作業步驟成功或失敗時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 所該採取的行動、應該嘗試作業步驟多少次，以及應該在何處寫入作業步驟輸出。  
  
## <a name="using-transact-sql"></a><a name="TSQL"></a>使用 Transact-SQL  
  
#### <a name="to-create-an-analysis-services-command-job-step"></a>若要建立 Analysis Services 命令作業步驟  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    -- Creates a job step that uses XMLA to create a relational data source that
    -- references the AdventureWorks2012 Microsoft SQL Server database.  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name =
            N'Create a relational data source that references the AdventureWorks2012 Microsoft SQL Server database',  
        @subsystem = N'ANALYSISCOMMAND',  
        @command =
            N' <Create xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
        <ParentObject>  
            <DatabaseID>AdventureWorks2012</DatabaseID>  
        </ParentObject>  
        <ObjectDefinition>  
            <DataSource xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                xsi:type="RelationalDataSource">  
                <ID>AdventureWorks2012</ID>  
                <Name>Adventure Works 2012</Name>  
                <ConnectionString>Data Source=localhost;Initial Catalog=AdventureWorks2012;Integrated Security=True</ConnectionString>  
                <ImpersonationInfo>  
                    <ImpersonationMode>ImpersonateServiceAccount</ImpersonationMode>  
                </ImpersonationInfo>  
                <ManagedProvider>System.Data.SqlClient</ManagedProvider>  
                <Timeout>PT0S</Timeout>  
            </DataSource>  
        </ObjectDefinition>  
    </Create>', ;  
    GO  
    ```  
  
如需詳細資訊，請參閱 [sp_add_jobstep (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)。  
  
#### <a name="to-create-an-analysis-services-query-job-step"></a>若要建立 Analysis Services 查詢作業步驟  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    -- Creates a job step that uses MDX to return data  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Returns the Internet sales amount by state',  
        @subsystem = N'ANALYSISQUERY',  
        @command = N' SELECT  
       [Measures].[Internet Sales Amount] ON COLUMNS,  
       [Customer].[State-Province].Members ON ROWS  
    FROM [AdventureWorks2012]',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    ```  
  
如需詳細資訊，請參閱 [sp_add_jobstep (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)。  
  
## <a name="using-sql-server-management-objects"></a><a name="SMO"></a>使用 SQL Server 管理物件  
**建立 PowerShell 指令碼作業步驟**  
  
透過所選的程式語言，例如 XMLA 或 MDX，使用 **JobStep** 類別。 如需詳細資訊，請參閱 [SQL Server 管理物件 (SMO)](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)。  
