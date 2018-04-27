---
title: 套件的 SQL Server Agent 作業 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: packages
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- jobs [Integration Services]
- automatic package execution
- scheduling packages [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: ecf7a5f9-b8a7-47f1-9ac0-bac07cb89e31
caps.latest.revision: 54
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 50d8803f21ddb9687bfcc861a683932a0ba53f44
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="sql-server-agent-jobs-for-packages"></a>封裝的 SQL Server Agent 作業
  您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent，自動化並排程 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的執行。 您可以排程部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器，並且儲存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝存放區及檔案系統的封裝。  
  
## <a name="sections-in-this-topic"></a>本主題的章節  
 本主題包含下列幾節：  
  
-   [在 SQL Server Agent 中排程作業](#jobs)  
  
-   [排程 Integration Services 封裝](#packages)  
  
-   [疑難排解已排程封裝](#trouble)  
  
##  <a name="jobs"></a> Scheduling Jobs in SQL Server Agent  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所安裝的服務，可讓您透過執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業，以自動化並排程工作。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務必須先執行，作業才能自動執行。 如需詳細資訊，請參閱 [Configure SQL Server Agent](https://docs.microsoft.com/sql/ssms/agent/configure-sql-server-agent)。  
  
 當您連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體時，[SQL Server Agent] 節點會出現在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的物件總管中。  
  
 若要自動化週期性工作，請使用 [新增作業] 對話方塊建立作業。 如需詳細資訊，請參閱[實作作業](https://docs.microsoft.com/sql/ssms/agent/implement-jobs)。  
  
 建立作業後，您必須加入至少一個步驟。 作業可以包含多個步驟，且每個步驟都能執行不同的工作。 如需詳細資訊，請參閱 [Manage Job Steps](https://docs.microsoft.com/sql/ssms/agent/manage-job-steps)。  
  
 在建立作業和步驟後，您就可以建立執行該作業的排程。 不過，您也可以建立以手動方式執行的未排程作業。 如需詳細資訊，請參閱 [建立及附加排程至作業](https://docs.microsoft.com/sql/ssms/agent/create-and-attach-schedules-to-jobs)。  
  
 透過設定通知選項可以加強作業，例如，指定作業完成時要向其傳送電子郵件的操作員，或加入警示。 如需詳細資訊，請參閱 [警示](https://docs.microsoft.com/sql/ssms/agent/alerts)。  
  
##  <a name="packages"></a> Scheduling Integration Services Packages  
 當您建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業來排程 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝時，必須加入至少一個步驟，並將該步驟的類型設為 [SQL Server Integration Services 封裝]。 作業可以包含多個步驟，且每個步驟都能執行不同的封裝。  
  
 從作業步驟執行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝，如同使用 **dtexec** (dtexec.exe) 和 **DTExecUI** (dtexecui.exe) 公用程式來執行封裝。 但不是透過使用命令列選項或 [執行封裝公用程式] 對話方塊來設定封裝的執行階段選項，而是在 [新增作業步驟] 對話方塊設定執行階段選項。 如需執行封裝之選項的詳細資訊，請參閱 [dtexec 公用程式](../../integration-services/packages/dtexec-utility.md)。  
  
 如需詳細資訊，請參閱 [使用 SQL Server Agent 排程封裝](#schedule)。  
  
 如需示範如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 來執行封裝的影片，請參閱 MSDN Library 中的影片首頁， [如何：使用 SQL Server Agent 讓 SSIS 封裝執行自動化 (SQL Server 影片)](http://go.microsoft.com/fwlink/?LinkId=141771)。  
  
##  <a name="trouble"></a> 疑難排解  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業步驟可能無法啟動封裝，即使封裝在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中以及從命令列都順利執行。 此問題有一些常見的原因，以及數個建議的解決方案。 如需詳細資訊，請參閱下列資源。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 知識庫文件： [從 SQL Server Agent 作業步驟呼叫 SSIS 封裝時，SSIS 封裝未執行](http://support.microsoft.com/kb/918760)  
  
-   位於 MSDN Library 的影片： [疑難排解：使用 SQL Server Agent 的封裝執行 (SQL Server 影片)](http://go.microsoft.com/fwlink/?LinkId=141772)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業步驟啟動封裝後，封裝執行可能失敗，也可能會成功，但產生非預期的結果。 您可以使用下列工具對這些問題進行疑難排解。  
  
-   對於儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] MSDB 資料庫、[!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝存放區，或是本機電腦上資料夾中的封裝，您可以使用 [記錄檔檢視器]，以及在封裝執行期間所產生的任何記錄檔和偵錯傾印檔案。  
  
     **若要使用記錄檔檢視器，請執行下列操作。**  
  
    1.  在物件總管中以滑鼠右鍵按一下 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業]，然後按一下 [檢視記錄]。  
  
    2.  利用 [訊息] 資料行中的 [作業失敗] 訊息，尋找 [記錄檔摘要] 方塊中的作業執行。  
  
    3.  展開作業節點，然後按一下作業步驟，檢視 [記錄檔摘要] 方塊下方區域中訊息的詳細資料。  
  
-   對於儲存在 SSISDB 資料庫中的封裝，您也可以使用 [記錄檔檢視器]，以及在封裝執行期間所產生的任何記錄檔和偵錯傾印檔案。 此外，您可以使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器的報表。  
  
     **若要在報表中尋找與作業執行相關聯之封裝執行的資訊，請執行下列操作。**  
  
    1.  依照上述步驟檢視作業步驟之訊息的詳細資料。  
  
    2.  尋找訊息中列出的執行識別碼。  
  
    3.  在 [物件總管] 中展開 [Integration Services 目錄] 節點。  
  
    4.  以滑鼠右鍵按一下 [SSISDB]，然後依序指向 [報表]、[標準報表]，再按一下 [所有執行]。  
  
    5.  在 [所有執行] 報表中，於 [識別碼] 資料行中尋找執行識別碼。 按一下 [概觀]、[所有訊息] 或 [執行效能]，檢視此封裝執行的相關資訊。  
  
    如需 [概觀]、[所有訊息] 和 [執行效能] 報告的詳細資訊，請參閱 [Integration Services 伺服器的報表](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports)。  

## <a name="schedule"></a> 使用 SQL Server Agent 排程封裝
  下列程序會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業步驟執行封裝，藉此提供自動化封裝執行的步驟。  
  
### <a name="to-automate-package-execution-by-using-sql-server-agent"></a>使用 SQL Server Agent 自動化封裝執行  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，連接到要在其中建立作業之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，或開啟包含要加入步驟之作業的執行個體。  
  
2.  在物件總管中展開 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 節點，並執行下列其中一項作業：  
  
    -   若要建立新作業，請以滑鼠右鍵按一下 [作業]，然後按一下 [新增作業]。  
  
    -   若要將步驟加入至現有的作業，請展開 [作業]，並以滑鼠右鍵按一下該作業，然後按一下 [屬性]。  
  
3.  在 [一般] 頁面上，如果您正在建立新作業，請提供作業名稱、選取擁有者和作業類別，並選擇性地提供作業描述。  
  
4.  若要讓作業可用於排程，請選取 [已啟用]。  
  
5.  若要建立您要排程之封裝的作業步驟，請按一下 [步驟]，然後按一下 [新增]。  
  
6.  選取 [Integration Services 封裝] 作為作業步驟類型。  
  
7.  在 [執行身分] 清單中，選取 [SQL Server Agent 服務帳戶] 或選取具有作業步驟將使用之認證的 Proxy 帳戶。 如需建立 Proxy 帳戶的資訊，請參閱[建立 SQL Server Agent Proxy](http://msdn.microsoft.com/library/142e0c55-a8b9-4669-be49-b9dc602d5988)。  
  
     使用 Proxy 帳戶而非 [SQL Server Agent 服務帳戶]，可解決使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 執行封裝時可能發生的常見問題。 如需這些問題的詳細資訊，請參閱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 知識庫文章： [從 SQL Server Agent 作業步驟呼叫 SSIS 封裝時，SSIS 封裝未執行](http://support.microsoft.com/kb/918760)。  
  
    > **注意：** 如果 Proxy 帳戶所使用認證的密碼變更，您就需要更新認證密碼。 否則，作業步驟將會失敗。  
  
     如需設定 SQL Server Agent 服務帳戶的資訊，請參閱[設定 SQL Server Agent 的服務啟動帳戶 &#40;SQL Server 組態管理員&#41;](http://msdn.microsoft.com/library/46ffe818-ebb5-43a0-840b-923f219a2472)。  
  
8.  在 [封裝來源] 清單方塊中，按一下封裝的來源，然後設定作業步驟的選項。  
  
     **下表描述可能的封裝來源。**  
  
    |封裝來源|描述|  
    |--------------------|-----------------|  
    |**SSIS 目錄**|儲存在 SSISDB 資料庫中的封裝。 封裝會包含在部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案中。|  
    |**[SQL Server]**|儲存在 MSDB 資料庫中的封裝。 您會使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務管理這些封裝。|  
    |**SSIS 封裝存放區**|儲存在您電腦上預設資料夾中的封裝。 預設資料夾為 \<磁碟機>:\Program Files\Microsoft SQL Server\110\DTS\Packages。 您會使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務管理這些封裝。<br /><br /> 注意：您可以指定不同的資料夾，或指定檔案系統中 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務要管理的其他資料夾，方法是修改 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]的組態檔。 如需詳細資訊，請參閱 [Integration Services Service &#40;SSIS Service&#41;](../../integration-services/service/integration-services-service-ssis-service.md) (Integration Services 服務 (SSIS 服務))。|  
    |**[File System]**|儲存在您本機電腦上任何資料夾中的封裝。|  
  
     **下表描述根據您選取的封裝來源，可供作業步驟使用的組態選項。**  
  
    > **重要：**如果套件受到密碼保護，當您按一下 [新增作業步驟] 對話方塊的 [一般] 頁面上的任何索引標籤時 ([套件] 索引標籤除外)，會需要在顯示的 [套件密碼] 對話方塊中輸入密碼。 否則，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業將無法執行封裝。  
  
     **封裝來源**：SSIS 目錄  
  
    |索引標籤|選項。|  
    |---------|-------------|  
    |**封裝**|**Server**<br /><br /> 輸入或選取主控 SSISDB 目錄之資料庫伺服器執行個體的名稱。<br /><br /> 如果 [SSIS 目錄] 是封裝來源，您只能使用 Microsoft Windows 使用者帳戶登入伺服器。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法使用驗證。|  
    ||**封裝**<br /><br /> 按一下省略符號按鈕並選取封裝。<br /><br /> 您會在**物件總管**的 [Integration Services 目錄] 節點下，選取資料夾中的封裝。|  
    |**參數**<br /><br /> 位於 [組態] 索引標籤上。|[Integration Services 專案轉換精靈] 可讓您以參數取代封裝組態。<br /><br /> [參數] 索引標籤會顯示您設計封裝時加入的參數，例如透過使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。 索引標籤也會顯示您將 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案從封裝部署模型轉換為專案部署模型時加入封裝的參數。 輸入包含在封裝中之參數的新值。 您可以輸入常值，或使用包含在已對應至參數之伺服器環境變數中的值。<br /><br /> 若要輸入常值，請按一下參數旁邊的省略符號按鈕。 [編輯執行的常值] 對話方塊隨即出現。<br /><br /> 若要使用環境變數，請按一下 [環境]，然後選取包含您要使用之變數的環境。<br /><br /> **\*\* 重要事項 \*\*** 如果您已將多個參數及/或連線管理員屬性對應至多個環境中包含的變數，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會顯示錯誤訊息。 對於某個特定執行，封裝只能藉由單一伺服器環境中包含的值執行。<br /><br /> 如需如何建立伺服器環境以及將變數對應至參數的資訊，請參閱[部署 Integration Services (SSIS) 專案和套件](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)。|  
    |**連接管理員**<br /><br /> 位於 [組態] 索引標籤上。|變更連接管理員屬性的值。 例如，您可以變更伺服器名稱。 SSIS 伺服器上會自動產生連接管理員屬性的參數。 若要變更屬性值，您可以輸入常值，或使用包含在已對應至連接管理員屬性之伺服器環境變數中的值。<br /><br /> 若要輸入常值，請按一下參數旁邊的省略符號按鈕。 [編輯執行的常值] 對話方塊隨即出現。<br /><br /> 若要使用環境變數，請按一下 [環境]，然後選取包含您要使用之變數的環境。<br /><br /> **\*\* 重要事項 \*\*** 如果您已將多個參數及/或連線管理員屬性對應至多個環境中包含的變數，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會顯示錯誤訊息。 對於某個特定執行，封裝只能藉由單一伺服器環境中包含的值執行。<br /><br /> 如需如何建立伺服器環境以及將變數對應至連線管理員屬性的資訊，請參閱[部署 Integration Services (SSIS) 專案和套件](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)。|  
    |**進階**<br /><br /> 位於 [組態] 索引標籤上。|設定封裝執行的下列其他設定：|  
    ||**屬性覆寫**：<br /><br /> 按一下 [加入] 輸入封裝屬性的新值、指定屬性路徑，以及指出屬性值是否為敏感。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器加密敏感資料。 若要編輯或移除屬性的設定，請按一下 [屬性覆寫] 方塊中的資料列，然後按一下 [編輯] 或 [移除]。 您可以執行下列其中一個動作來尋找屬性路徑：<br /><br /> -從 XML 組態檔 (\*.dtsconfig) 檔案複製屬性路徑。 路徑會在檔案的 [組態] 區段中列出，做為 [路徑] 屬性的值。 以下是 MaximumErrorCount 屬性的路徑範例：\Package.Properties[MaximumErrorCount]<br /><br /> -執行 [封裝組態精靈]，並從最後的 [正在完成精靈] 頁面複製屬性路徑。 然後您就可以取消精靈。<br /><br /> <br /><br /> 注意：[屬性覆寫] 選項主要用於您從舊版 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 升級之組態的封裝。 您使用 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 建立並部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器的建立會使用參數，而非組態。|  
    ||**記錄層次**<br /><br /> 選取下列其中一個封裝執行的記錄層級。 請注意，選取 [效能] 或 [詳細資訊] 記錄層級，可能會影響封裝執行的效能。<br /><br /> **無**：<br />                          關閉記錄功能。 只記錄封裝執行狀態。<br /><br /> **基本**：<br />                          記錄所有事件，自訂和診斷事件除外。 這是記錄層級的預設值。<br /><br /> **效能**：<br />                          只記錄效能統計資料，以及 OnError 和 OnWarning 事件。<br /><br /> **詳細資訊**：<br />                          記錄所有事件，包括自訂和診斷事件。<br /><br /> 您選取的記錄層級會決定 SSISDB 檢視及 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器的報表中顯示的資訊。 如需詳細資訊，請參閱 [Integration Services (SSIS) 記錄](../../integration-services/performance/integration-services-ssis-logging.md)。|  
    ||**在發生錯誤時傾印**<br /><br /> 指定在封裝執行期間發生任何錯誤時，是否產生偵錯傾印檔案。 這些檔案會包含有關封裝執行的資訊，可幫助您針對問題進行疑難排解。 當您選取此選項，而在執行期間發生錯誤時， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會建立 .mdmp 檔 (二進位檔) 和 .tmp 檔 (文字檔)。 根據預設，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會將檔案儲存在 \<磁碟機>:\Program Files\Microsoft SQL Server\110\Shared\ErrorDumps 資料夾中。|  
    ||**32 位元執行階段**<br /><br /> 指出是否在已安裝 64 位元版本之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的 64 位元電腦上，使用 32 位元版本的 dtexec 公用程式執行封裝。<br /><br /> 如果您的封裝使用的原生 OLE DB 提供者無法在 64 位元版本中使用，您可能需要使用 32 位元版本的 dtexec 執行封裝。 如需詳細資訊，請參閱 [Integration Services 的 64 位元考量](http://msdn.microsoft.com/library/ms141766\(SQL.105\).aspx)。<br /><br /> 根據預設，當您選取 [SQL Server Integration Services 封裝] 作業步驟類型時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會使用系統自動叫用的 dtexec 公用程式版本執行封裝。 系統會根據電腦處理器以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的版本和電腦上執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent，叫用 32 位元或 64 位元版本的公用程式。|  
  
     **封裝來源**：SQL Server、SSIS 封裝存放區或檔案系統  
  
     您可以針對儲存在 SQL Server、SSIS 封裝存放區或檔案系統中的封裝設定的許多選項，這些選項會對應至 **dtexec** 命令提示字元公用程式的命令列選項。 如需公用程式和命令列選項的詳細資訊，請參閱 [dtexec 公用程式](../../integration-services/packages/dtexec-utility.md)。  
  
    |索引標籤|選項。|  
    |---------|-------------|  
    |**封裝**<br /><br /> 這些是儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝存放區之封裝的索引標籤選項。|**Server**<br /><br /> 輸入或選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務之資料庫伺服器執行個體的名稱。|  
    ||**[使用 Windows 驗證]**<br /><br /> 選取此選項即可使用 Microsoft Windows 使用者帳戶登入伺服器。|  
    ||**[使用 SQL Server 驗證]**<br /><br /> 當使用者透過不信任連接並指定登入名稱和密碼進行連接時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會執行驗證，檢查是否已設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入帳戶，以及指定的密碼是否符合先前記錄的密碼。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 找不到登入帳戶，驗證將會失敗，且使用者會收到錯誤訊息。|  
    ||**使用者名稱**|  
    ||**密碼**|  
    ||**封裝**<br /><br /> 按一下省略符號按鈕並選取封裝。<br /><br /> 您會在**物件總管**的 [存放的封裝] 節點下，選取資料夾中的封裝。|  
    |**封裝**<br /><br /> 這些是儲存在檔案系統中之封裝的索引標籤選項。|**封裝**<br /><br /> 輸入封裝檔的完整路徑，或按一下省略符號按鈕選取封裝。|  
    |**組態**|加入 XML 組態檔，以特定組態執行封裝。 使用封裝組態在執行階段更新封裝屬性的值。<br /><br /> 此選項對應至 **dtexec** 的 **/ConfigFile**選項。<br /><br /> 如需了解封裝組態套用的方式，請參閱＜ [Package Configurations](../../integration-services/packages/package-configurations.md)＞。 如需如何建立封裝組態的資訊，請參閱 [建立封裝組態](../../integration-services/packages/create-package-configurations.md)。|  
    |**命令檔**|在另一個檔案中，指定要以 **dtexec**執行的其他選項。<br /><br /> 例如，您可以納入包含 /Dump *errorcode* 選項的檔案，以便在封裝執行過程中發生一個或多個指定的事件時，產生偵錯傾印檔案。<br /><br /> 您可以建立多個檔案，然後使用 [命令檔] 選項指定適當的檔案，藉此以不同的選項組合執行封裝。<br /><br /> [命令檔] 選項對應至 **dtexec** 的 **/CommandFile** 選項。|  
    |**資料來源**|檢視包含在封裝中的連接管理員。 若要修改連接字串，請按一下連接管理員，然後按一下連接字串。<br /><br /> 此選項對應至 **dtexec** 的 **/Connection**選項。|  
    |**執行選項**|**發生驗證警告時封裝就失敗**<br /> 指出是否將警告訊息視為錯誤。 如果您選取此選項，而在驗證期間發生警告，則封裝會在驗證期間失敗。 此選項對應至 **dtexec** 的 **/WarnAsError**選項。<br /><br /> **驗證封裝但不執行**<br /> 指出在驗證階段之後，是否停止執行封裝 (並不會實際執行封裝)。 此選項對應至 **dtexec** 的 **/Validate**選項。<br /><br /> **覆寫 MacConcurrentExecutables 屬性**<br /> 指定封裝可以同時執行的可執行檔數量。 值為 -1，表示封裝可以執行的最大可執行檔數目，等於執行封裝之電腦上的處理器總數再加 2。 此選項對應至 **dtexec** 的 **/MaxConcurrent**選項。<br /><br /> **啟用封裝檢查點**<br /> 指出在執行封裝期間，封裝是否要使用檢查點。 如需詳細資訊，請參閱 [使用檢查點來重新啟動封裝](../../integration-services/packages/restart-packages-by-using-checkpoints.md)。<br /><br /> 此選項對應至 **dtexec** 的 **/CheckPointing**選項。<br /><br /> **覆寫重新啟動選項**<br /> 指出是否為封裝上的 **CheckpointUsage** 屬性設定新值。 從 [重新啟動選項] 清單方塊中選取值。<br /><br /> 此選項對應至 **dtexec** 的 **/Restart**選項。<br /><br /> **使用 32 位元執行階段**<br /> 指出是否在已安裝 64 位元版本之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的 64 位元電腦上，使用 32 位元版本的 dtexec 公用程式執行封裝。<br /><br /> 如果您的封裝使用的原生 OLE DB 提供者無法在 64 位元版本中使用，您可能需要使用 32 位元版本的 dtexec 執行封裝。 如需詳細資訊，請參閱 [Integration Services 的 64 位元考量](http://msdn.microsoft.com/library/ms141766\(SQL.105\).aspx)。<br /><br /> 根據預設，當您選取 [SQL Server Integration Services 封裝] 作業步驟類型時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會使用系統自動叫用的 dtexec 公用程式版本執行封裝。 系統會根據電腦處理器以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的版本和電腦上執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent，叫用 32 位元或 64 位元版本的公用程式。|  
    |**記錄**|讓記錄提供者與執行封裝產生關聯。<br /><br /> **文字檔的 SSIS 記錄提供者**<br /> 將記錄項目寫入 ASCII 文字檔中<br /><br /> **SQL Server 的 SSIS 記錄提供者**<br /> 將記錄項目寫入 MSDB 資料庫中的 sysssislog 資料表。<br /><br /> **SQL Server Profiler 的 SSIS 記錄提供者**<br /> 寫入您可以使用 SQL Server Profiler 檢視的追蹤檔。<br /><br /> **Windows 事件記錄檔的 SSIS 記錄提供者**<br /> 將記錄項目寫入 Windows 事件記錄檔中的應用程式記錄檔。<br /><br /> **XML 檔案的 SSIS 記錄提供者**<br /> 將記錄檔寫入 XML 檔案。<br /><br /> 對於文字檔、XML 檔案和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler 記錄提供者，請選取包含在封裝中的檔案連接管理員。 對於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記錄提供者，請選取包含在封裝中的 OLE DB 連線管理員。<br /><br /> 此選項對應至 **dtexec** 的 **/Logger**選項。|  
    |**設定值**|覆寫封裝屬性設定。 在 [屬性] 方塊的 [屬性路徑] 和 [值] 資料行中輸入值。 在您輸入某個屬性的值之後，[屬性] 對話方塊中就會出現一個空白資料列，讓您輸入其他屬性的值。<br /><br /> 若要從 [屬性] 方塊中移除屬性，請按一下資料列，然後按一下 [移除]。<br /><br /> 您可以執行下列其中一個動作來尋找屬性路徑：<br /><br /> -從 XML 組態檔 (\*.dtsconfig) 檔案複製屬性路徑。 路徑會在檔案的 [組態] 區段中列出，做為 [路徑] 屬性的值。 以下是 MaximumErrorCount 屬性的路徑範例：\Package.Properties[MaximumErrorCount]<br /><br /> -執行 [封裝組態精靈]，並從最後的 [正在完成精靈] 頁面複製屬性路徑。 然後您就可以取消精靈。|  
    |**驗證**|**只執行簽署的封裝**<br /> 指出是否已檢查封裝簽章。 如果此封裝未簽署或是簽章無效，此封裝就會失敗。 此選項對應至 **dtexec** 的 **/VerifySigned**選項。<br /><br /> **確認封裝組建**<br /> 指出是否已對照此選項旁的 [組建] 方塊中所輸入的組建編號，驗證封裝的組建編號。 如果發生不符的情形，將不會執行封裝。 此選項對應至 **dtexec** 的 **/VerifyBuild**選項。<br /><br /> **確認封裝識別碼**<br /> 指出是否已驗證封裝的 GUID，方法是將它與此選項旁的 [封裝識別碼] 方塊中所輸入的封裝識別碼相比較。 此選項對應至 **dtexec** 的 **/VerifyPackageID**選項。<br /><br /> **確認版本識別碼**<br /> 指出是否已驗證封裝的版本 GUID，方法是將它與此選項旁的 [版本識別碼] 方塊中所輸入的版本識別碼相比較。 此選項對應至 **dtexec** 的 **/VerifyVersionID**選項。|  
    |**命令列**|修改 dtexec 的命令列選項。 如需選項的詳細資訊，請參閱 [dtexec 公用程式](../../integration-services/packages/dtexec-utility.md)。<br /><br /> **還原原始選項**<br /> 使用您在 [Job Set Properties (作業集屬性)] 對話方塊的 [封裝]、[組態]、[命令檔]、[資料來源]、[執行選項]、[記錄]、[設定值] 和 [驗證] 索引標籤中設定的命令列選項。<br /><br /> **手動編輯命令**<br /> 在 [命令列] 方塊中輸入其他命令列選項。<br /><br /> 在您按一下 [確定] 儲存作業步驟的變更之前，可以先按一下 [還原原始選項]，移除您在 [命令列] 方塊中輸入的所有其他選項。<br /><br /> **\*\* 提示 \*\*** 您可以將命令列複製到 [命令提示字元] 視窗中，加入 `dtexec`，然後從命令列執行封裝。 這是產生命令列文字的簡單方式。|  
  
9. 按一下 [確定]，儲存設定並關閉 [新增作業步驟] 對話方塊。  
  
    > **注意：**對於儲存在 [SSIS 目錄] 中的套件，如果有未解析的參數或連接管理員屬性設定，則會停用 [確定] 按鈕。 當您使用包含在伺服器環境變數中的值設定參數或屬性，而且符合下列其中一項條件時，未解析的設定就會發生。  
    >   
    >  未選取 [組態] 索引標籤的 [環境] 核取方塊。  
    >   
    >  [組態] 索引標籤上的清單方塊中未選取包含變數的伺服器環境。  
  
10. 若要建立作業步驟的排程，請按一下 [選取頁面] 窗格中的 [排程]。 如需如何設定排程的資訊，請參閱[排程作業](http://msdn.microsoft.com/library/f626390a-a3df-4970-b7a7-a0529e4a109c)。  
  
    > [!TIP]  
    >  當您為排程命名時，請考慮使用唯一的描述性名稱，以便更容易區分此排程與其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 排程。  

## <a name="see-also"></a>另請參閱  
 [執行專案和套件](deploy-integration-services-ssis-projects-and-packages.md)  

## <a name="external-resources"></a>外部資源  
  
-   [網站上的知識庫文件：](http://support.microsoft.com/kb/918760)從 SQL Server Agent 作業步驟呼叫 SSIS 封裝時，SSIS 封裝未執行 [!INCLUDE[msCoName](../../includes/msconame-md.md)]  
  
-   位於 MSDN Library 的影片： [疑難排解：使用 SQL Server Agent 的封裝執行 (SQL Server 影片)](http://go.microsoft.com/fwlink/?LinkId=141772)  
  
-   位於 MSDN Library 的影片： [如何：使用 SQL Server Agent 讓 SSIS 封裝執行自動化 (SQL Server 影片)](http://go.microsoft.com/fwlink/?LinkId=141771)  
  
-   位於 mssqltips.com 的技術文件： [Checking SQL Server Agent jobs using Windows PowerShell](http://go.microsoft.com/fwlink/?LinkId=165675)(使用 Windows PowerShell 檢查 SQL Server Agent 作業)  
  
-   mssqltips.com 上的技術文件： [Auto alert for SQL Agent jobs when they are enabled or disabled](http://go.microsoft.com/fwlink/?LinkId=165676)(於 SQL Agent 作業已啟用或停用時自動警示)  
  
-   mssqltips.com 上的部落格文章： [Configuring SQL Agent Jobs to Write to Windows Event Log](http://go.microsoft.com/fwlink/?LinkId=220745)(將 SQL 代理程式工作設定成寫入 Windows 事件記錄檔)。  
  
  
