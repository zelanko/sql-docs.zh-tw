---
title: 使用 SQL Server Agent 排程封裝 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3d389cce-05af-4e1d-b684-7bbff413c806
caps.latest.revision: 28
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d3112f43436fa7e0a0bb87d58cca062857bae8e4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37215758"
---
# <a name="schedule-a-package-by-using-sql-server-agent"></a>使用 SQL Server Agent 排程封裝
  下列程序會使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 作業步驟執行封裝，藉此提供自動化封裝執行的步驟。  
  
### <a name="to-automate-package-execution-by-using-sql-server-agent"></a>使用 SQL Server Agent 自動化封裝執行  
  
1.  在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中，連接到要在其中建立作業之 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體，或開啟包含要加入步驟之作業的執行個體。  
  
2.  在物件總管中展開 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 節點，並執行下列其中一項作業：  
  
    -   若要建立新作業，請以滑鼠右鍵按一下 [作業]，然後按一下 [新增作業]。  
  
    -   若要將步驟加入至現有的作業，請展開 [作業]，並以滑鼠右鍵按一下該作業，然後按一下 [屬性]。  
  
3.  在 [一般] 頁面上，如果您正在建立新作業，請提供作業名稱、選取擁有者和作業類別，並選擇性地提供作業描述。  
  
4.  若要讓作業可用於排程，請選取 [已啟用]。  
  
5.  若要建立您要排程之封裝的作業步驟，請按一下 [步驟]，然後按一下 [新增]。  
  
6.  選取 [Integration Services 封裝] 作為作業步驟類型。  
  
7.  在 [執行身分] 清單中，選取 [SQL Server Agent 服務帳戶] 或選取具有作業步驟將使用之認證的 Proxy 帳戶。 如需建立 Proxy 帳戶的資訊，請參閱[建立 SQL Server Agent Proxy](../ssms/agent/create-a-sql-server-agent-proxy.md)。  
  
     使用 Proxy 帳戶而非 [SQL Server Agent 服務帳戶]，可解決使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 執行封裝時可能發生的常見問題。 如需這些問題的詳細資訊，請參閱 [!INCLUDE[msCoName](../includes/msconame-md.md)] 知識庫文章：[從 SQL Server Agent 作業步驟呼叫 SSIS 封裝時，SSIS 封裝未執行](http://support.microsoft.com/kb/918760)。  
  
    > [!NOTE]  
    >  如果 Proxy 帳戶所使用認證的密碼變更，您就需要更新認證密碼。 否則，作業步驟將會失敗。  
  
     如需設定 SQL Server Agent 服務帳戶的資訊，請參閱[設定 SQL Server Agent 的服務啟動帳戶 &#40;SQL Server 組態管理員&#41;](../relational-databases/sql-server-configuration-manager.md)。  
  
8.  在 [封裝來源] 清單方塊中，按一下封裝的來源，然後設定作業步驟的選項。  
  
     **下表描述可能的封裝來源。**  
  
    |封裝來源|描述|  
    |--------------------|-----------------|  
    |**SSIS 目錄**|儲存在 SSISDB 資料庫中的封裝。 封裝會包含在部署至 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案中。|  
    |**[SQL Server]**|儲存在 MSDB 資料庫中的封裝。 您會使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務管理這些封裝。|  
    |**SSIS 封裝存放區**|儲存在您電腦上預設資料夾中的封裝。 預設資料夾為 \<磁碟機>:\Program Files\Microsoft SQL Server\110\DTS\Packages。 您會使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務管理這些封裝。<br /><br /> 注意：您可以指定不同的資料夾，或指定檔案系統中 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務要管理的其他資料夾，方法是修改 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 的組態檔。 如需詳細資訊，請參閱[設定 Integration Services 服務 &#40;SSIS 服務&#41;](service/integration-services-service-ssis-service.md)。|  
    |**[File System]**|儲存在您本機電腦上任何資料夾中的封裝。|  
  
     **下表描述根據您選取的封裝來源，可供作業步驟使用的組態選項。**  
  
    > [!IMPORTANT]  
    >  如果封裝受到密碼保護，當您按一下 [新增作業步驟] 對話方塊的 [一般] 頁面上的任何索引標籤時 ([封裝] 索引標籤除外)，會需要在顯示的 [封裝密碼] 對話方塊中輸入密碼。 否則，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 作業將無法執行封裝。  
  
     **封裝來源**：SSIS 目錄  
  
    |索引標籤|選項。|  
    |---------|-------------|  
    |**封裝**|**Server**<br /><br /> 輸入或選取主控 SSISDB 目錄之資料庫伺服器執行個體的名稱。<br /><br /> 如果 [SSIS 目錄] 是封裝來源，您只能使用 Microsoft Windows 使用者帳戶登入伺服器。 無法使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證。|  
    ||**封裝**<br /><br /> 按一下省略符號按鈕並選取封裝。<br /><br /> 您會在**物件總管**的 [Integration Services 目錄] 節點下，選取資料夾中的封裝。|  
    |**參數**<br /><br /> 位於 [組態] 索引標籤上。|輸入包含在封裝中之參數的新值。 您可以輸入常值，或使用包含在已對應至參數之伺服器環境變數中的值。  **\*\* 重要\* \*** 如果您有多個參數及/或連接管理員屬性對應至包含在多個環境中的變數[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]代理程式會顯示一則錯誤訊息。 對於某個特定執行，封裝只能藉由單一伺服器環境中包含的值執行。<br /><br /> 若要輸入常值，請按一下參數旁邊的省略符號按鈕。 [編輯執行的常值] 對話方塊隨即出現。<br /><br /> 若要使用環境變數，請按一下 [環境]，然後選取包含您要使用之變數的環境。<br /><br /> <br /><br /> [參數] 索引標籤會顯示您設計封裝時加入的參數，例如透過使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]。 索引標籤也會顯示您將 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案從封裝部署模型轉換為專案部署模型時加入封裝的參數。 [Integration Services 專案轉換精靈] 可讓您以參數取代封裝組態。<br /><br /> 如需如何建立伺服器環境以及將變數對應至參數的資訊，請參閱[建立和對應伺服器環境](../../2014/integration-services/create-and-map-a-server-environment.md)。|  
    |**連接管理員**<br /><br /> 位於 [組態] 索引標籤上。|變更連接管理員屬性的值。 例如，您可以變更伺服器名稱。<br /><br /> SSIS 伺服器上會自動產生連接管理員屬性的參數。<br /><br /> 若要變更屬性值，您可以輸入常值，或使用包含在已對應至連接管理員屬性之伺服器環境變數中的值。 **\*\* 重要\* \*** 如果您有多個參數及/或連接管理員屬性對應至包含在多個環境中的變數[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]代理程式會顯示一則錯誤訊息。 對於某個特定執行，封裝只能藉由單一伺服器環境中包含的值執行。<br /><br /> 若要輸入常值，請按一下參數旁邊的省略符號按鈕。 [編輯執行的常值] 對話方塊隨即出現。<br /><br /> 若要使用環境變數，請按一下 [環境]，然後選取包含您要使用之變數的環境。<br /><br /> <br /><br /> 如需如何建立伺服器環境以及將變數對應至連線管理員屬性的資訊，請參閱[建立和對應伺服器環境](../../2014/integration-services/create-and-map-a-server-environment.md)。|  
    |**進階**<br /><br /> 位於 [組態] 索引標籤上。|設定封裝執行的下列其他設定。<br /><br /> <br /><br /> **屬性會覆寫**： 按一下 **新增**輸入封裝屬性的新值，指定屬性路徑，以及指出屬性值是否為敏感。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器加密敏感資料。 若要編輯或移除屬性的設定，請按一下 [屬性覆寫] 方塊中的資料列，然後按一下 [編輯] 或 [移除]。 請注意，**屬性會覆寫**選項供您從舊版升級之組態的封裝[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]。 您使用 [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] 建立並部署至 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器的建立會使用參數，而非組態。 您可以執行下列其中一個動作來尋找屬性路徑：<br /><br /> 從 XML 組態檔中複製屬性路徑 (\*.dtsconfig) 檔案。 路徑會在檔案的 [組態] 區段中列出，做為 [路徑] 屬性的值。 以下是 MaximumErrorCount 屬性的路徑範例。<br /><br /> \Package.Properties[MaximumErrorCount]<br /><br /> 執行**封裝組態精靈**，並從最後一個複製屬性路徑**完成精靈**頁面。 然後您就可以取消精靈。|  
    ||**記錄層級**： 您選取的記錄層次會決定 SSISDB 檢視及報告中顯示的資訊[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]伺服器。 請注意，選取 [效能] 或 [詳細資訊] 記錄層級，可能會影響封裝執行的效能。 選取其中一個封裝執行的下列記錄層次：<br /><br /> **無**： 關閉記錄功能。 只記錄封裝執行狀態。<br /><br /> **基本**： 記錄所有事件，但自訂和診斷事件除外。 這是記錄層級的預設值。<br /><br /> **效能**： 記錄只效能統計資料，以及 OnError 和 OnWarning 事件。<br /><br /> **Verbose**： 記錄所有事件，包括自訂和診斷事件。<br /><br /> 如需詳細資訊，請參閱 [在 SSIS 伺服器上啟用封裝執行的記錄功能](../../2014/integration-services/enable-logging-for-package-execution-on-the-ssis-server.md)。|  
    ||**在發生錯誤的傾印**： 指定封裝執行期間發生任何錯誤時，是否產生偵錯傾印檔案。<br /><br /> 這些檔案會包含有關封裝執行的資訊，可幫助您針對問題進行疑難排解。<br /><br /> 當您選取此選項，而在執行期間發生錯誤時，[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 會建立 .mdmp 檔 (二進位檔) 和 .tmp 檔 (文字檔)。 根據預設，[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 會將檔案儲存在 \<磁碟機>:\Program Files\Microsoft SQL Server\110\Shared\ErrorDumps 資料夾中。|  
    ||**32 位元執行階段**指出是否要在 64 位元版本的 64 位元電腦上使用 32 位元版本的 dtexec 公用程式執行封裝[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]和[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]安裝代理程式。<br /><br /> 如果您的封裝使用的原生 OLE DB 提供者無法在 64 位元版本中使用，您可能需要使用 32 位元版本的 dtexec 執行封裝。 如需詳細資訊，請參閱 [Integration Services 的 64 位元考量](http://msdn.microsoft.com/library/ms141766\(SQL.105\).aspx)。<br /><br /> 根據預設，當您選取 [SQL Server Integration Services 封裝] 作業步驟類型時，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 會使用系統自動叫用的 dtexec 公用程式版本執行封裝。 系統會根據電腦處理器以及 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的版本和電腦上執行的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent，叫用 32 位元或 64 位元版本的公用程式。|  
  
     **封裝來源**：SQL Server、SSIS 封裝存放區或檔案系統  
  
     有許多您可以設定儲存在 SQL Server、 SSIS 封裝存放區或檔案系統中，封裝的選項對應至命令列選項`dtexec`命令提示字元公用程式。 如需公用程式和命令列選項的詳細資訊，請參閱 [dtexec 公用程式](packages/dtexec-utility.md)。  
  
    |索引標籤|選項。|  
    |---------|-------------|  
    |**封裝**<br /><br /> 這些是儲存在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssIS](../includes/ssis-md.md)] 封裝存放區之封裝的索引標籤選項。|**Server**<br /><br /> 輸入或選取 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務之資料庫伺服器執行個體的名稱。|  
    ||**[使用 Windows 驗證]**<br /><br /> 選取此選項即可使用 Microsoft Windows 使用者帳戶登入伺服器。|  
    ||**[使用 SQL Server 驗證]**<br /><br /> 當使用者透過不信任連接並指定登入名稱和密碼進行連接時， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會執行驗證，檢查是否已設定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 登入帳戶，以及指定的密碼是否符合先前記錄的密碼。 如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 找不到登入帳戶，驗證將會失敗，且使用者會收到錯誤訊息。|  
    ||**使用者名稱**|  
    ||**密碼**|  
    ||**封裝**<br /><br /> 按一下省略符號按鈕並選取封裝。<br /><br /> 您會在**物件總管**的 [存放的封裝] 節點下，選取資料夾中的封裝。|  
    |**封裝**<br /><br /> 這些是儲存在檔案系統中之封裝的索引標籤選項。|**封裝**<br /><br /> 輸入封裝檔的完整路徑，或按一下省略符號按鈕選取封裝。|  
    |**組態**|加入 XML 組態檔，以特定組態執行封裝。 使用封裝組態在執行階段更新封裝屬性的值。<br /><br /> 此選項對應至 **/ConfigFile**選項`dtexec`。<br /><br /> 如需了解封裝組態套用的方式，請參閱＜ [Package Configurations](../../2014/integration-services/package-configurations.md)＞。 如需如何建立封裝組態的資訊，請參閱[建立封裝組態](../../2014/integration-services/create-package-configurations.md)。|  
    |**命令檔**|指定您想要執行的其他選項`dtexec`，在不同的檔案。<br /><br /> 例如，您可以納入包含 /Dump *errorcode* 選項的檔案，以便在封裝執行過程中發生一個或多個指定的事件時，產生偵錯傾印檔案。<br /><br /> 您可以建立多個檔案，然後使用 [命令檔] 選項指定適當的檔案，藉此以不同的選項組合執行封裝。<br /><br /> **命令檔**選項對應至`/CommandFile`選項`dtexec`。|  
    |**資料來源**|檢視包含在封裝中的連接管理員。 若要修改連接字串，請按一下連接管理員，然後按一下連接字串。<br /><br /> 此選項對應至`/Connection`選項`dtexec`。|  
    |**執行選項**|**發生驗證警告時封裝就失敗**<br /> 指出是否將警告訊息視為錯誤。 如果您選取此選項，而在驗證期間發生警告，則封裝會在驗證期間失敗。 此選項對應至`/WarnAsError`選項`dtexec`。<br /><br /> **驗證封裝但不執行**<br /> 指出在驗證階段之後，是否停止執行封裝 (並不會實際執行封裝)。 此選項對應至`/Validate`選項`dtexec`。<br /><br /> **覆寫 MacConcurrentExecutables 屬性**<br /> 指定封裝可以同時執行的可執行檔數量。 值為 -1，表示封裝可以執行的最大可執行檔數目，等於執行封裝之電腦上的處理器總數再加 2。 此選項對應至`/MaxConcurrent`選項`dtexec`。<br /><br /> **啟用封裝檢查點**<br /> 指出在執行封裝期間，封裝是否要使用檢查點。 如需詳細資訊，請參閱 [使用檢查點來重新啟動封裝](packages/restart-packages-by-using-checkpoints.md)。<br /><br /> 此選項對應 `/CheckPointing` 的 `dtexec` 選項。<br /><br /> **覆寫重新啟動選項**<br /> 指出是否要將新的值設定為`CheckpointUsage`封裝上的屬性。 從 [重新啟動選項] 清單方塊中選取值。<br /><br /> 此選項對應至`/Restart`選項`dtexec`。<br /><br /> **使用 32 位元執行階段**<br /> 指出是否在已安裝 64 位元版本之 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 的 64 位元電腦上，使用 32 位元版本的 dtexec 公用程式執行封裝。<br /><br /> 如果您的封裝使用的原生 OLE DB 提供者無法在 64 位元版本中使用，您可能需要使用 32 位元版本的 dtexec 執行封裝。 如需詳細資訊，請參閱 [Integration Services 的 64 位元考量](http://msdn.microsoft.com/library/ms141766\(SQL.105\).aspx)。<br /><br /> 根據預設，當您選取 [SQL Server Integration Services 封裝] 作業步驟類型時，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 會使用系統自動叫用的 dtexec 公用程式版本執行封裝。 系統會根據電腦處理器以及 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的版本和電腦上執行的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent，叫用 32 位元或 64 位元版本的公用程式。|  
    |**記錄**|讓記錄提供者與執行封裝產生關聯。<br /><br /> **文字檔的 SSIS 記錄提供者**<br /> 將記錄項目寫入 ASCII 文字檔中<br /><br /> **SQL Server 的 SSIS 記錄提供者**<br /> 將記錄項目寫入 MSDB 資料庫中的 sysssislog 資料表。<br /><br /> **SQL Server Profiler 的 SSIS 記錄提供者**<br /> 寫入您可以使用 SQL Server Profiler 檢視的追蹤檔。<br /><br /> **Windows 事件記錄檔的 SSIS 記錄提供者**<br /> 將記錄項目寫入 Windows 事件記錄檔中的應用程式記錄檔。<br /><br /> **XML 檔案的 SSIS 記錄提供者**<br /> 將記錄檔寫入 XML 檔案。<br /><br /> 對於文字檔、XML 檔案和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Profiler 記錄提供者，請選取包含在封裝中的檔案連接管理員。 對於 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 記錄提供者，請選取包含在封裝中的 OLE DB 連線管理員。<br /><br /> 此選項對應至`/Logger`選項`dtexec`。|  
    |**設定值**|覆寫封裝屬性設定。 在 [屬性] 方塊的 [屬性路徑] 和 [值] 資料行中輸入值。 在您輸入某個屬性的值之後，[屬性] 對話方塊中就會出現一個空白資料列，讓您輸入其他屬性的值。<br /><br /> 若要從 [屬性] 方塊中移除屬性，請按一下資料列，然後按一下 [移除]。<br /><br /> 您可以執行下列其中一個動作來尋找屬性路徑。<br /><br /> 從 XML 組態檔中複製屬性路徑 (\*.dtsconfig) 檔案。 路徑會在檔案的 [組態] 區段中列出，做為 [路徑] 屬性的值。 以下是 MaximumErrorCount 屬性的路徑範例。<br /><br /> \Package.Properties[MaximumErrorCount]<br /><br /> 執行**封裝組態精靈**，並從最後一個複製屬性路徑**完成精靈**頁面。 然後您就可以取消精靈。|  
    |**驗證**|**只執行簽署的封裝**<br /> 指出是否已檢查封裝簽章。 如果此封裝未簽署或是簽章無效，此封裝就會失敗。 此選項對應至`/VerifySigned`選項`dtexec`。<br /><br /> **確認封裝組建**<br /> 指出是否已對照此選項旁的 [組建] 方塊中所輸入的組建編號，驗證封裝的組建編號。 如果發生不符的情形，將不會執行封裝。 此選項對應至`/VerifyBuild`選項`dtexec`。<br /><br /> **確認封裝識別碼**<br /> 指出是否已驗證封裝的 GUID，方法是將它與此選項旁的 [封裝識別碼] 方塊中所輸入的封裝識別碼相比較。 此選項對應至`/VerifyPackageID`選項`dtexec`。<br /><br /> **確認版本識別碼**<br /> 指出是否已驗證封裝的版本 GUID，方法是將它與此選項旁的 [版本識別碼] 方塊中所輸入的版本識別碼相比較。 此選項對應至`/VerifyVersionID`選項`dtexec`。|  
    |**命令列**|修改 dtexec 的命令列選項。 如需選項的詳細資訊，請參閱 [dtexec 公用程式](packages/dtexec-utility.md)。<br /><br /> 提示： 您可以將命令列複製到 [命令提示字元] 視窗中，加入`dtexec`，然後從命令列執行封裝。 這是產生命令列文字的簡單方式。<br /><br /> **還原原始選項**<br /> 使用您在 [Job Set Properties (作業集屬性)] 對話方塊的 [封裝]、[組態]、[命令檔]、[資料來源]、[執行選項]、[記錄]、[設定值] 和 [驗證] 索引標籤中設定的命令列選項。<br /><br /> **手動編輯命令**<br /> 在 [命令列] 方塊中輸入其他命令列選項。<br /><br /> 在您按一下 [確定] 儲存作業步驟的變更之前，可以先按一下 [還原原始選項]，移除您在 [命令列] 方塊中輸入的所有其他選項。|  
  
9. 按一下 [確定]，儲存設定並關閉 [新增作業步驟] 對話方塊。  
  
    > [!NOTE]  
    >  對於儲存在 [SSIS 目錄] 中的封裝，如果有未解析的參數或連線管理員屬性設定，則 [確定] 按鈕會停用。 當您使用包含在伺服器環境變數中的值設定參數或屬性，而且符合下列其中一項條件時，未解析的設定就會發生。  
    >   
    >  -   未選取 [組態] 索引標籤的 [環境] 核取方塊。  
    > -   [組態] 索引標籤上的清單方塊中未選取包含變數的伺服器環境。  
  
10. 若要建立作業步驟的排程，請按一下 [選取頁面] 窗格中的 [排程]。 如需如何設定排程的資訊，請參閱[排程作業](../ssms/agent/schedule-a-job.md)。  
  
    > [!TIP]  
    >  當您為排程命名時，請考慮使用唯一的描述性名稱，以便更容易區分此排程與其他 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 排程。  
  
## <a name="see-also"></a>另請參閱  
 [執行專案和套件](packages/run-integration-services-ssis-packages.md)  
  
  
