---
title: 管理作業步驟 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- job steps [SQL Server replication]
- job steps [SQL Server Agent]
- jobs [SQL Server Agent], Integration Services package step
- executable programs as job steps
- operating systems [SQL Server], job steps
- Transact-SQL job step
- job steps [Transact-SQL]
- Integration Services packages, job steps
- replication job steps [SQL Server]
- logs [SQL Server], jobs
- SQL Server Agent jobs, job steps
- ActiveX scripting jobs [SQL Server]
- job steps [Analysis Services]
ms.assetid: 51352afc-a0a4-428b-8985-f9e58bb57c31
caps.latest.revision: 49
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 19d8635c9836277f915896c17dbd4719d5d1da71
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36037154"
---
# <a name="manage-job-steps"></a>管理作業步驟
  作業步驟是指作業對資料庫或伺服器所採取的動作， 每一個作業必須至少有一個作業步驟。 作業步驟可以是：  
  
-   可執行檔程式與作業系統命令。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，包括預存程序和擴充預存程序。  
  
-   PowerShell 指令碼。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX Script。  
  
-   複寫工作。  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 工作。  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 套件。  
  
 每個作業步驟都是在特定的安全性內容中執行。 如果作業步驟指定 Proxy，則作業步驟會在該 Proxy 認證的安全性內容中執行。 如果作業步驟未指定 Proxy，則作業步驟會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶的內容中執行。 只有系統管理員 (sysadmin) 固定伺服器角色的成員，才可以建立未明確指定 Proxy 的作業。  
  
 因為作業步驟是在特定 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 使用者的環境中執行，因此該使用者需具備讓作業步驟執行所需的權限和組態。 例如，如果您建立了一個作業，它需要磁碟機代號或通用命名慣例 (UNC) 路徑，則在測試工作時，其作業步驟可能會在您的 Windows 使用者帳戶下執行。 不過，作業步驟的 Windows 使用者也必須具備必要的權限、磁碟機代號組態或必要磁碟機的存取權， 否則，作業步驟會失敗。 若要防止此問題發生，請確定每一個作業步驟的 Proxy，對於作業步驟所執行的工作都具有必要權限。 如需詳細資訊，請參閱[SQL Server Database Engine 和 Azure SQL Database 的資訊安全中心](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)。  
  
## <a name="job-step-logs"></a>作業步驟記錄  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 可以將某些作業步驟的輸出寫入作業系統檔案，或寫入 msdb 資料庫中的 sysjobstepslogs 資料表。 以下作業步驟類型可以寫入輸出至兩個目的地：  
  
-   可執行檔程式與作業系統命令。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 工作。  
  
 當執行作業步驟的使用者是系統管理員 (sysadmin) 固定伺服器角色的成員時，這些作業步驟才可以將作業步驟輸出寫入作業系統檔案。 如果執行作業步驟的使用者是 msdb 資料庫中的 SQLAgentUserRole、SQLAgentReaderRole 或 SQLAgentOperatorRole 固定資料庫角色的成員，則這些作業步驟的輸出只能寫入 sysjobstepslogs 資料表中。  
  
 當作業或作業步驟遭到刪除時，作業步驟記錄也會跟著自動刪除。  
  
> [!NOTE]  
>  複寫工作和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝作業步驟的記錄是由其個別的子系統處理， 您不能使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 來設定這些作業步驟類型的作業步驟記錄。  
  
## <a name="executable-programs-and-operating-system-commands-as-job-steps"></a>可執行程式和作業系統命令類型的作業步驟  
 可執行程式和作業系統命令可以做為作業步驟， 這些檔案的副檔名為 .bat、.cmd、.com 或 .exe。  
  
 當您使用可執行程式或作業系統命令做為作業步驟時，必須指定：  
  
-   指令成功時傳回的處理序結束代碼。  
  
-   要執行的命令。 若要執行作業系統命令，此處是指命令本身； 若為外部程式，則是指程式名稱和程式的引數，例如： **C:\Program Files\Microsoft SQL Server\100\Tools\Binn\sqlcmd.exe -e -q "sp_who"**  
  
    > [!NOTE]  
    >  如果可執行檔不在系統路徑或執行作業步驟的使用者路徑中，您必須提供可執行檔的完整路徑。  
  
## <a name="transact-sql-job-steps"></a>Transact-SQL 作業步驟  
 當您建立 [!INCLUDE[tsql](../../includes/tsql-md.md)] 作業步驟時，必須：  
  
-   識別用來執行作業的資料庫。  
  
-   輸入要執行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 陳述式可以呼叫預存程序或擴充預存程序。  
  
 (選擇性) 您也可以開啟現有的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 檔案做為作業步驟的命令。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 作業步驟不使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Proxy。 相反地，如果作業步驟的擁有者是系統管理員 (sysadmin) 固定伺服器角色的成員，則作業步驟會以作業步驟的擁有者或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶的身分來執行。 系統管理員 (sysadmin) 固定伺服器角色的成員也可以指定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 作業步驟在另一個使用者內容之下執行，方法是使用 sp_add_jobstep 預存程序的 *database_user_name* 參數。 如需詳細資訊，請參閱[sp_add_jobstep &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql)。  
  
> [!NOTE]  
>  單一 [!INCLUDE[tsql](../../includes/tsql-md.md)] 作業步驟可包含多個批次。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 作業步驟可包含內嵌 GO 命令。  
  
## <a name="powershell-scripting-job-steps"></a>PowerShell 指令碼作業步驟  
 當您建立 PowerShell 指令碼作業步驟時，必須指定其中一個設定當做此步驟的命令：  
  
-   PowerShell 指令碼的文字。  
  
-   要開啟之現有的 PowerShell 指令碼檔案。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent PowerShell 子系統會開啟一個 PowerShell 工作階段，並載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 嵌入式管理單元。當作作業步驟命令使用的 PowerShell 指令碼可以參考 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 提供者和指令程式。 如需使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 嵌入式管理單元撰寫 PowerShell 指令碼的詳細資訊，請參閱 [SQL Server PowerShell](../../powershell/sql-server-powershell.md)。  
  
## <a name="activex-scripting-job-steps"></a>ActiveX Scripting 作業步驟  
  
> [!IMPORTANT]  
>  ActiveX Scripting 作業步驟將從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 未來版本的 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Agent 中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。  
  
 建立 ActiveX Scripting 作業步驟時，您必須：  
  
-   確認撰寫作業步驟所用的指令碼語言。  
  
-   撰寫 ActiveX Script。  
  
 您也可以開啟一個現存的 ActiveX Script 檔做為該作業步驟的指令。 另外，ActiveX Script 命令也可以在外部編譯 (例如，使用 Microsoft Visual Basic)，然後再當成可執行程式來執行。  
  
 當作業步驟指令是一個 ActiveX Script 時，您可以使用 SQLActiveScriptHost 物件將輸出列印到作業步驟記錄，或者是建立 COM 物件。 SQLActiveScriptHost 是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 主控系統導入指令碼命名空間內的全域物件。 此物件具有兩個方法 (Print 和 CreateObject)。 下列範例顯示 ActiveX Scripting 在 Visual Basic Scripting Edition (VBScript) 中如何運作。  
  
```  
' VBScript example for ActiveX Scripting job step  
' Create a Dmo.Server object. The object connects to the  
' server on which the script is running.  
  
Set oServer = CreateObject("SQLDmo.SqlServer")  
oServer.LoginSecure = True  
oServer.Connect "(local)"  
'Disconnect and destroy the server object  
oServer.DisConnect  
Set oServer = nothing  
  
```  
  
## <a name="replication-job-steps"></a>複寫作業步驟  
 當您利用複寫建立發行集和訂閱時，依預設會建立複寫作業。 建立的作業類型取決於複寫類型 (快照式、交易式或合併式) 和所使用的選項。  
  
 複寫作業步驟會啟動以下複寫代理程式的其中之一：  
  
-   快照集代理程式 (快照集作業)  
  
-   記錄讀取器代理程式 (LogReader 作業)  
  
-   散發代理程式 (散發作業)  
  
-   合併代理程式 (合併作業)  
  
-   佇列讀取器代理程式 (QueueReader 作業)  
  
 設定複寫時，您可以指定以三種方式的其中一種來執行複寫代理程式：在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 啟動之後持續執行、視需要執行或根據排程執行。 如需複寫代理程式的詳細資訊，請參閱 [複寫代理程式概觀](../../relational-databases/replication/agents/replication-agents-overview.md)。  
  
## <a name="analysis-services-job-steps"></a>SQL Server Analysis Services 作業步驟  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 支援兩個不同類型的 Analysis Services 作業步驟，即命令作業步驟和查詢作業步驟。  
  
### <a name="analysis-services-command-job-steps"></a>SQL Server Analysis Services 命令作業步驟  
 當您建立 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 命令作業步驟時，必須：  
  
-   識別要執行作業步驟的資料庫 OLAP 伺服器。  
  
-   輸入要執行的陳述式。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] **Execute** 方法的陳述式必須是 XML。 陳述式可能不含完整的 SOAP Envelope 或 XML for [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] **Discover** 方法。 請注意，雖然 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 支援完整的 SOAP Envelope 與 **Discover** 方法，但是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業步驟則不支援。  
  
### <a name="analysis-services-query-job-steps"></a>SQL Server Analysis Services 查詢作業步驟  
 當您建立 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 查詢作業步驟時，必須：  
  
-   識別要執行作業步驟的資料庫 OLAP 伺服器。  
  
-   輸入要執行的陳述式。 陳述式必須為多維度運算式 (MDX) 查詢。  
  
 如需有關 MDX 的詳細資訊，請參閱[MDX 查詢基礎觀念&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)。  
  
## <a name="integration-services-packages"></a>Integration Services 封裝  
 當您建立 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝作業步驟時，必須執行以下動作：  
  
-   識別封裝的來源。  
  
-   識別封裝的位置。  
  
-   如果組態檔是封裝所必要的，請識別組態檔。  
  
-   如果命令檔是封裝所必要的，請識別命令檔。  
  
-   識別要用於封裝的驗證。 例如，您可以指定封裝必須加以簽署，或封裝必須有特定的封裝識別碼。  
  
-   識別封裝的資料來源。  
  
-   識別封裝的記錄提供者。  
  
-   指定在執行封裝之前要設定的變數和值。  
  
-   識別執行選項。  
  
-   新增或修改命令列選項。  
  
 請注意，如果您將套件部署至 SSIS 目錄並將 [SSIS 目錄] 指定為套件來源，此組態資訊的大部分會從套件中自動取得。 在 [組態] 索引標籤下，您可以指定環境、參數值、連接管理員值、屬性覆寫、以及套件是否會在 32 位元執行階段環境中執行。  
  
 如需建立用於執行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 套件之作業步驟的詳細資訊，請參閱[套件的 SQL Server Agent 作業](../../integration-services/packages/sql-server-agent-jobs-for-packages.md)。  
  
## <a name="related-tasks"></a>相關工作  
  
|||  
|-|-|  
|**說明**|**主題**|  
|描述如何建立包含可執行程式的作業步驟。|[建立 CmdExec 作業步驟](create-a-cmdexec-job-step.md)|  
|描述如何重設 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 權限。|[設定使用者可建立及管理 SQL Server Agent 作業](configure-a-user-to-create-and-manage-sql-server-agent-jobs.md)|  
|描述如何建立 [!INCLUDE[tsql](../../includes/tsql-md.md)] 作業步驟。|[Create a Transact-SQL Job Step](create-a-transact-sql-job-step.md)|  
|描述如何定義 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Transact-SQL 作業步驟的選項。|[Define Transact-SQL Job Step Options](define-transact-sql-job-step-options.md)|  
|描述如何建立 ActiveX 指令碼作業步驟。|[Create an ActiveX Script Job Step](create-an-activex-script-job-step.md)|  
|描述如何建立及定義執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Analysis Services 命令與查詢的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業步驟。|[Create an Analysis Services Job Step](create-an-analysis-services-job-step.md)|  
|描述作業執行期間發生錯誤時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 應該採取的動作。|[Set Job Step Success or Failure Flow](set-job-step-success-or-failure-flow.md)|  
|描述如何檢視 [作業步驟屬性] 對話方塊中的作業步驟詳細資料。|[檢視作業步驟資訊](view-job-step-information.md)|  
|描述如何刪除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業步驟記錄。|[Delete a Job Step Log](delete-a-job-step-log.md)|  
  
## <a name="see-also"></a>另請參閱  
 [dbo.sysjobstepslogs &#40;Transact SQL&#41;](/sql/relational-databases/system-tables/dbo-sysjobstepslogs-transact-sql)   
 [建立作業](create-jobs.md)   
 [sp_add_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-job-transact-sql)  
  
  
