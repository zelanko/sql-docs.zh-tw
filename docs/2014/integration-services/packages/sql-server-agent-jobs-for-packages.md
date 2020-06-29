---
title: 套件的 SQL Server Agent 作業 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- jobs [Integration Services]
- automatic package execution
- scheduling packages [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: ecf7a5f9-b8a7-47f1-9ac0-bac07cb89e31
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c834dcc5302244d4127aaf75ed9e16a53f3342aa
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85423725"
---
# <a name="sql-server-agent-jobs-for-packages"></a>封裝的 SQL Server Agent 作業
  您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 來自動化並排程 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 套件的執行。 您可以排程部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器，並且儲存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝存放區及檔案系統的封裝。  
  
## <a name="sections-in-this-topic"></a>本主題的章節  
 本主題包含下列幾節：  
  
-   [在 SQL Server Agent 中排程作業](#jobs)  
  
-   [排程 Integration Services 封裝](#packages)  
  
-   [疑難排解已排程封裝](#trouble)  
  
##  <a name="scheduling-jobs-in-sql-server-agent"></a><a name="jobs"></a>排程 SQL Server Agent 中的工作  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所安裝的服務，可讓您透過執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業，以自動化並排程工作。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務必須先執行，作業才能自動執行。 如需詳細資訊，請參閱 [Configure SQL Server Agent](../../ssms/agent/configure-sql-server-agent.md)。  
  
 當您連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體時，[SQL Server Agent]**** 節點會出現在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的物件總管中。  
  
 若要自動化週期性工作，請使用 [新增作業]**** 對話方塊建立作業。 如需詳細資訊，請參閱 [實作作業](../../ssms/agent/implement-jobs.md)。  
  
 建立作業後，您必須加入至少一個步驟。 作業可以包含多個步驟，且每個步驟都能執行不同的工作。 如需詳細資訊，請參閱 [Manage Job Steps](../../ssms/agent/manage-job-steps.md)。  
  
 在建立作業和步驟後，您就可以建立執行該作業的排程。 不過，您也可以建立以手動方式執行的未排程作業。 如需詳細資訊，請參閱 [建立及附加排程至作業](../../ssms/agent/create-and-attach-schedules-to-jobs.md)。  
  
 透過設定通知選項可以加強作業，例如，指定作業完成時要向其傳送電子郵件的操作員，或加入警示。 如需詳細資訊，請參閱 [警示](../../ssms/agent/alerts.md)。  
  
##  <a name="scheduling-integration-services-packages"></a><a name="packages"></a> Scheduling Integration Services Packages  
 當您建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業來排程 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝時，必須加入至少一個步驟，並將該步驟的類型設為 [SQL Server Integration Services 封裝]****。 作業可以包含多個步驟，且每個步驟都能執行不同的封裝。  
  
 從作業步驟執行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝，如同使用 **dtexec** (dtexec.exe) 和 **DTExecUI** (dtexecui.exe) 公用程式來執行封裝。 但不是透過使用命令列選項或 [執行封裝公用程式]**** 對話方塊來設定封裝的執行階段選項，而是在 [新增作業步驟]**** 對話方塊設定執行階段選項。 如需執行封裝之選項的詳細資訊，請參閱 [dtexec 公用程式](dtexec-utility.md)。  
  
 如需詳細資訊，請參閱 [使用 SQL Server Agent 排程封裝](../schedule-a-package-by-using-sql-server-agent.md)。  
  
 如需示範如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 來執行封裝的影片，請參閱 MSDN Library 中的影片首頁， [如何：使用 SQL Server Agent 讓 SSIS 封裝執行自動化 (SQL Server 影片)](https://go.microsoft.com/fwlink/?LinkId=141771)。  
  
##  <a name="troubleshooting"></a><a name="trouble"></a> 疑難排解  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業步驟可能無法啟動封裝，即使封裝在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中以及從命令列都順利執行。 此問題有一些常見的原因，以及數個建議的解決方案。 如需詳細資訊，請參閱下列資源。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 知識庫文件： [從 SQL Server Agent 作業步驟呼叫 SSIS 封裝時，SSIS 封裝未執行](https://support.microsoft.com/kb/918760)  
  
-   影片，[疑難排解：使用 SQL Server Agent 的封裝執行（SQL Server 影片）](https://go.microsoft.com/fwlink/?LinkId=141772)，位於 MSDN Library。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業步驟啟動封裝後，封裝執行可能失敗，也可能會成功，但產生非預期的結果。 您可以使用下列工具對這些問題進行疑難排解。  
  
-   對於儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] MSDB 資料庫、[!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝存放區，或是本機電腦上資料夾中的封裝，您可以使用 [記錄檔檢視器]****，以及在封裝執行期間所產生的任何記錄檔和偵錯傾印檔案。  
  
     **若要使用記錄檔檢視器，請執行下列操作。**  
  
    1.  在物件總管中以滑鼠右鍵按一下 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業]，然後按一下 [檢視記錄]****。  
  
    2.  利用 [訊息]**** 資料行中的 [作業失敗]**** 訊息，尋找 [記錄檔摘要]**** 方塊中的作業執行。  
  
    3.  展開作業節點，然後按一下作業步驟，檢視 [記錄檔摘要]**** 方塊下方區域中訊息的詳細資料。  
  
-   對於儲存在 SSISDB 資料庫中的封裝，您也可以使用 [記錄檔檢視器]****，以及在封裝執行期間所產生的任何記錄檔和偵錯傾印檔案。 此外，您可以使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器的報表。  
  
     **若要在報表中尋找與作業執行相關聯之封裝執行的資訊，請執行下列操作。**  
  
    1.  依照上述步驟檢視作業步驟之訊息的詳細資料。  
  
    2.  尋找訊息中列出的執行識別碼。  
  
    3.  在 [物件總管] 中展開 [Integration Services 目錄] 節點。  
  
    4.  以滑鼠右鍵按一下 [SSISDB]，然後依序指向 [報表]、[標準報表]，再按一下 [所有執行]。  
  
    5.  在 [所有執行]**** 報表中，於 [識別碼]**** 資料行中尋找執行識別碼。 按一下 [概觀]****、[所有訊息]**** 或 [執行效能]****，檢視此封裝執行的相關資訊。  
  
         如需 [概觀]、[所有訊息] 和 [執行效能] 報告的詳細資訊，請參閱 [Integration Services 伺服器的報表](../reports-for-the-integration-services-server.md)。  
  
## <a name="external-resources"></a>外部資源  
  
-   [網站上的知識庫文件：](https://support.microsoft.com/kb/918760)從 SQL Server Agent 作業步驟呼叫 SSIS 封裝時，SSIS 封裝未執行 [!INCLUDE[msCoName](../../includes/msconame-md.md)]  
  
-   位於 MSDN Library 的影片： [疑難排解：使用 SQL Server Agent 的封裝執行 (SQL Server 影片)](https://go.microsoft.com/fwlink/?LinkId=141772)  
  
-   位於 MSDN Library 的影片： [如何：使用 SQL Server Agent 讓 SSIS 封裝執行自動化 (SQL Server 影片)](https://go.microsoft.com/fwlink/?LinkId=141771)  
  
-   位於 mssqltips.com 的技術文件： [Checking SQL Server Agent jobs using Windows PowerShell](https://go.microsoft.com/fwlink/?LinkId=165675)(使用 Windows PowerShell 檢查 SQL Server Agent 作業)  
  
-   mssqltips.com 上的技術文件： [Auto alert for SQL Agent jobs when they are enabled or disabled](https://go.microsoft.com/fwlink/?LinkId=165676)(於 SQL Agent 作業已啟用或停用時自動警示)  
  
-   mssqltips.com 上的部落格文章： [Configuring SQL Agent Jobs to Write to Windows Event Log](https://go.microsoft.com/fwlink/?LinkId=220745)(將 SQL 代理程式工作設定成寫入 Windows 事件記錄檔)。  
  
  
