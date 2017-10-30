---
title: "dtexec 公用程式 |Microsoft 文件"
ms.custom: 
ms.date: 08/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7b6867fa-1039-49b3-90fb-85b84678a612
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 0c021c5f17266bfbba65d3d364136dd0d61d74f3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/27/2017

---
# <a name="dtexec-utility"></a>dtexec 公用程式
  **dtexec** 命令提示字元公用程式可用於設定及執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。 **dtexec** 公用程式可存取所有封裝組態及執行功能，例如參數、連線、屬性、變數、記錄與進度指標。 **dtexec** 公用程式可讓您從下列來源載入封裝： [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器、.ispac 專案檔案、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝存放區及檔案系統。  
  
> **注意：** 當您使用最新版 **dtexec** 公用程式來執行舊版 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]所建立的套件，此公用程式會暫時將套件升級為目前的套件格式。 但您無法使用 **dtexec** 公用程式儲存這些升級的封裝。 如需如何永久地將封裝升級到最新版本，請參閱 [Upgrade Integration Services Packages](../../integration-services/install-windows/upgrade-integration-services-packages.md)。  
  
 本主題包含下列各節：  
  
-   [Integration Services 伺服器及專案檔案](#server)  
  
-   [64 位元電腦上的安裝考量](#bit)  
  
-   [擁有並存安裝之電腦的考量](#side)  
  
-   [執行階段](#phases)  
  
-   [傳回的結束碼](#exit)  
  
-   [語法與規則](#syntaxRules)  
  
-   [使用 xp_cmdshell 的 dtexec](#cmdshell)  
  
-   [語法](#syntax)  
  
-   [參數](#parameter)  
  
-   [備註](#remark)  
  
-   [範例](#example)  
  
##  <a name="server"></a> Integration Services 伺服器及專案檔案  
 當您使用 **dtexec** 執行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器上的封裝時，**dtexec** 會呼叫 [catalog.create_execution &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md)、[catalog.set_execution_parameter_value &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md) 和 [catalog.start_execution &#40;SSISDB 資料庫&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md) 預存程序來建立執行、 設定參數值以及啟動執行。 所有執行記錄都可以從伺服器的相關檢視中查看，或透過 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中提供的標準報表查看。 如需報表的詳細資訊，請參閱 [Integration Services 伺服器的報表](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports)。  
  
 以下是執行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器上的封裝範例。  
  
```  
DTExec /ISSERVER "\SSISDB\folderB\Integration Services Project17\Package.dtsx" /SERVER "." /Envreference 2 /Par "$Project::ProjectParameter(Int32)";1 /Par "Parameter(Int32)";21 /Par "CM.sqlcldb2.SSIS_repro.InitialCatalog";ssisdb /Par "$ServerOption::SYNCHRONIZED(Boolean)";True  
```  
  
 當您使用 **dtexec** 從 .ispac 專案檔案執行封裝時，相關的選項為：/Proj[ect] 和 /Pack[age]，這些選項用來指定專案路徑及封裝資料流名稱。 當您從 **執行** [Integration Services 專案轉換精靈] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，以便將專案轉換至專案部署模型時，此精靈會產生一個 .ispac 專案檔案。 如需詳細資訊，請參閱[部署 Integration Services (SSIS) 專案和封裝](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)。  
  
 您可以搭配協力廠商排程工具來使用 **dtexec** ，排程部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器的封裝。  
  
##  <a name="bit"></a> 64 位元電腦上的安裝考量  
 在 64 位元電腦上， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會安裝 64 位元版本的 **dtexec** 公用程式 (dtexec.exe)。 若您必須用 32 位元模式執行特定封裝，則須安裝 32 位元版本的 **dtexec** 公用程式。 若要安裝 32 位元版本的 **dtexec** 公用程式，則必須在安裝期間選取用戶端工具或 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 。  
  
 根據預設，同時安裝了 64 位元和 32 位元版之 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 命令提示字元公用程式的 64 位元電腦將會在命令提示字元上執行 32 位元版本。 執行 32 位元版本是因為 32 位元版本的目錄路徑在 PATH 環境變數中會出現在 64 位元版本的目錄路徑前面 (一般來說，32 位元的目錄路徑是*\<磁碟機 >*: \Program 檔案 (x86) \Microsoft SQL Server\110\DTS\Binn，而 64 位元的目錄路徑是*\<磁碟機 >*: \Program Files\Microsoft SQL Server\110\DTS\Binn。)  
  
> **注意：** 如果您使用 SQL Server Agent 執行此公用程式，SQL Server Agent 會自動使用 64 位元版的公用程式。 SQL Server Agent 會使用此登錄 (而不是 PATH 環境變數) 來尋找此公用程式的正確可執行檔。  
  
 若要確保您可在命令提示字元上執行 64 位元版的公用程式，您可以採取下列其中一個動作：  
  
-   開啟 [命令提示字元] 視窗中，切換到包含 64 位元版公用程式的目錄 (*\<磁碟機 >*: \Program Files\Microsoft SQL Server\110\DTS\Binn)，然後從該位置執行公用程式。  
  
-   在命令提示字元中，執行公用程式輸入完整路徑 (*\<磁碟機 >*: \Program Files\Microsoft SQL Server\110\DTS\Binn) 64 位元版公用程式。  
  
-   永久變更 PATH 環境變數中的路徑順序放置在 64 位元路徑 (*\<磁碟機 >*: \Program Files\Microsoft SQL Server\110\DTS\Binn) 之前在 32 位元路徑 (*\<磁碟機 >*: \程式檔案 (x86) \Microsoft SQL Server\110\DTS\Binn） 在變數中。  
  
##  <a name="side"></a> 擁有並存安裝之電腦的考量  
 如果 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 安裝在已安裝 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 或 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 的電腦上，則會安裝多個版本的 **dtexec** 公用程式。  
  
 若要確保您執行正確版本的公用程式，在命令提示字元中輸入完整路徑，以執行公用程式 (*\<磁碟機 >*: SQL Server \Program Files\Microsoft\\< 版本\>\DTS\Binn)。  
  
##  <a name="phases"></a> 執行階段  
 這個公用程式有四個執行階段。 執行階段如下所示：  
  
1.  命令來源階段：命令提示字元讀取已指定的選項和引數清單。 如果遇到了 **/?** 或 **/HELP** 選項，則會略過所有後續的階段。  
  
2.  封裝載入階段：已載入 **/SQL**、 **/FILE**或 **/DTS** 選項所指定的封裝。  
  
3.  設定階段：選項的處理順序如下：  
  
    -   設定封裝旗標、變數和屬性的選項。  
  
    -   確認封裝的版本和建置的選項。  
  
    -   設定公用程式之執行階段行為的選項，例如報告。  
  
4.  驗證和執行階段：執行封裝，如有指定 **/VALIDATE** 選項，將只會驗證封裝，而不會執行。  
  
##  <a name="exit"></a> 傳回的結束碼  
 **從 dtexec 公用程式傳回的結束碼**  
  
 封裝執行期間， **dtexec** 可能會傳回結束碼。 結束碼可用來擴展 ERRORLEVEL 變數，讓您可以在批次檔內的條件陳述式或分支邏輯中測試此變數的值。 下表列出 **dtexec** 公用程式結束時所能設定的值。  
  
|Value|描述|  
|-----------|-----------------|  
|0|順利執行封裝。|  
|1|封裝失敗。|  
|3|使用者取消封裝。|  
|4|公用程式找不到所要求的封裝。 找不到這個封裝。|  
|5|公用程式無法載入所要求的封裝。 無法載入這個封裝。|  
|6|公用程式在命令列中發現內部語法錯誤或語意錯誤。|  
  
##  <a name="syntaxRules"></a> 語法與規則  
 **公用程式語法規則**  
  
 所有選項的開頭都必須是斜線 (/) 或減號 (-)。 此處顯示的選項的開頭為斜線 (/)，但可以用減號 (-) 來替代。  
  
 如果引數中包含空格，則引數必須包含在引號內。 如果引數沒有用引號括住，則引數不能包含空格。  
  
 加上引號的字串內的雙引號代表逸出的單引號。  
  
 除了密碼以外，選項和引數都沒有區分大小寫。  
  
##  <a name="cmdshell"></a> 使用 xp_cmdshell 的 dtexec  
 **使用 xp_cmdshell 的 dtexec**  
  
 您可以從 **xp_cmdshell** 提示處執行 dtexec。 下列範例顯示如何執行名為 UpsertData.dtsx 的封裝，並忽略傳回碼：  
  
```  
EXEC xp_cmdshell 'dtexec /f "C:\UpsertData.dtsx"'  
```  
  
 下列範例顯示如何執行同一個封裝，並擷取傳回碼：  
  
```  
DECLARE @returncode int  
EXEC @returncode = xp_cmdshell 'dtexec /f "C:\UpsertData.dtsx"'  
```  
  
> **重要！！** 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，新安裝的 **xp_cmdshell** 選項預設為停用。 您可以執行 **sp_configure** 系統預存程序以啟用此選項。 如需詳細資訊，請參閱 [xp_cmdshell 伺服器組態選項](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)。  
  
##  <a name="syntax"></a> 語法  
  
```  
dtexec /option [value] [/option [value]]...  
```  
  
##  <a name="parameter"></a> 參數  
  
-   **/?** [*option_name*]：(選擇性)。 顯示命令提示字元選項，或顯示指定之 *option_name* 的說明，然後關閉公用程式。  
  
     如有指定 *option_name* 引數， **dtexec** 會啟動《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》，並顯示 dtexec 公用程式主題。  
  
-   **/Ca[llerInfo]**：(選擇性)。 指定封裝執行的其他資訊。 當您使用 SQL Server Agent 執行封裝時，代理程式會設定此引數以指示透過 SQL Server Agent 叫用封裝執行。 從命令列執行 **dtexec** 公用程式時，會忽略此參數。  
  
-   **/CheckF[ile]** *filespec*：(選擇性)。 將封裝上的 **CheckpointFileName** 屬性設為 *filespec*所指定的路徑和檔案。 當重新啟動封裝時，會使用這個檔案。 如果指定這個選項時沒有使用檔案名稱值，就會將封裝的 **CheckpointFileName** 設為空字串。 如果沒有指定這個選項，就會保留封裝中的值。  
  
-   **/CheckP[ointing]** *{on\off}* ：(選擇性)。 設定一個值來決定在執行封裝期間，封裝是否要使用檢查點。 **on** 值可指定重新執行失敗的封裝。 當重新執行失敗的封裝時，執行階段引擎會使用檢查點，從失敗點重新啟動封裝。  
  
     如果宣告的選項不含任何值，則預設值是 on。 如果此值設為 on，但找不到檢查點檔案，則封裝執行失敗。 如果沒有指定這個選項，就會保留封裝中所設定的值。 如需詳細資訊，請參閱 [Restart Packages by Using Checkpoints](../../integration-services/packages/restart-packages-by-using-checkpoints.md)。  
  
     dtexec 的 **/CheckPointing on** 選項相當於將封裝的 **SaveCheckpoints** 屬性設定為 [True]，以及將 **CheckpointUsage** 屬性設定為 [Always]。  
  
-   **/Com[mandFile]** *filespec*：(選擇性)。 指定要與 **dtexec**一起執行的命令選項。 *filespec* 中指定的檔案會開啟，並且讀取檔案中的選項，直到在檔案中找到 EOF 為止。 *filespec* 是文字檔。 *filespec* 引數會指定要與封裝的執行產生關聯之命令檔的檔名和路徑。  
  
-   **/Conf[igFile]** *filespec*：(選擇性)。 指定要擷取值的來源組態檔。 使用這個選項時，您可以設定一個執行階段組態，這個執行階段組態與封裝設計階段所指定的組態不同。 您可以將不同的組態設定儲存在 XML 組態檔中，然後在執行封裝之前，利用 **/ConfigFile** 選項載入設定。  
  
     您可以使用 **/ConfigFile** 選項在執行階段載入您未在設計階段指定的其他組態。 但您不可使用 **/ConfigFile** 選項取代您在設計階段指定過的設定值。 如需了解封裝組態套用的方式，請參閱＜ [Package Configurations](../../integration-services/packages/package-configurations.md)＞。  
  
-   **/Conn[ection]** *id_or_name;connection_string [[;id_or_name;connection_string]…]*：(選擇性)。 指定具有指定名稱或 GUID 的連接管理員位於此封裝中，並指定連接字串。  
  
     這個選項需要同時指定這兩個參數：在 *id_or_name* 引數中必須提供連接管理員名稱或 GUID，而且在 *connection_string* 引數中必須指定有效的連接字串。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 連接](../../integration-services/connection-manager/integration-services-ssis-connections.md)。  
  
     您可以在執行階段使用 **/Connection** 選項，從不同於設計時所指定的位置載入封裝組態。 然後這些組態的值會取代您原本指定的值。 但 **/Connection** 選項只可用於使用連接管理員的組態，例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態。 若要了解如何套用封裝組態，請參閱 [封裝組態](../../integration-services/packages/package-configurations.md) 和 [SQL Server 2016 中 Integration Services 功能的行為變更](http://msdn.microsoft.com/library/611d22fa-5ac7-485e-9a40-7131e852f794)。  
  
-   **/Cons[oleLog]** [[*displayoptions*];[*list_options*;*src_name_or_guid*]...]：(選擇性)。 在執行封裝期間，於主控台中顯示指定的記錄項目。 如果省略了這個選項，主控台便不會顯示任何記錄項目。 如果指定了這個選項，但未設定用來限制顯示的參數，就會顯示每個記錄項目。 若要限制主控台顯示的項目，您可以使用 *displayoptions* 參數指定要顯示的資料行，以及使用 *list_options* 參數來限制記錄項目類型。  
  
    > **注意：**  當您使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] /ISSERVER **參數在** 伺服器上執行套件時，主控台輸出會有所限制，且大部分的 **/Cons[oleLog]** 選項皆不適用。 所有執行記錄都可以從伺服器的相關檢視中查看，或透過 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中提供的標準報表查看。 如需報表的詳細資訊，請參閱 [Integration Services 伺服器的報表](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports)。  
  
     *displayoptions* 值如下：  
  
    -   N (名稱)  
  
    -   C (電腦)  
  
    -   O (操作員)  
  
    -   S (來源名稱)  
  
    -   G (來源 GUID)  
  
    -   X (執行 GUID)  
  
    -   M (訊息)  
  
    -   T (開始和結束時間)  
  
     *list_options* 值如下：  
  
    -   *I* - 指定包含清單。 只記錄指定的來源名稱或 GUID。  
  
    -   *E* - 指定排除清單。 不記錄指定的來源名稱或 GUID。  
  
    -   對包含或排除指定的 *src_name_or_guid* 參數為事件名稱、來源名稱或來源 GUID。  
  
     您如在同一個命令提示字元處使用多個 **/ConsoleLog** 選項，這些選項的互動方式如下：  
  
    -   顯示順序不受影響。  
  
    -   如果命令列上沒有包含清單，則排除清單會套用至所有類型的記錄項目。  
  
    -   如果命令列上出現任何包含清單，則排除清單會套用至所有包含清單的聯集。  
  
     如需 **/ConsoleLog** 選項的若干範例，請參閱＜ **備註** ＞一節。  
  
--   **/D [ts]** *package_path*: （選擇性）。 從 SSIS 封裝存放區中載入封裝。 儲存在 SSIS 封裝存放區中的封裝是使用舊版封裝部署模型所部署。 若要使用專案部署模型，執行部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器的封裝，請使用 **/ISServer** 選項。 如需有關封裝和專案部署模型的詳細資訊，請參閱＜ [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx)＞。  
  
     The *package_path* argument specifies the relative path of the [!INCLUDE[ssIS](../../includes/ssis-md.md)] package, starting at the root of the SSIS Package Store, and includes the name of the [!INCLUDE[ssIS](../../includes/ssis-md.md)] package. If the path or file name specified in the *package_path* argument contains a space, you must put quotation marks around the *package_path* argument.  
  
     The **/DTS** option cannot be used together with the **/File** or **/SQL** option. If multiple options are specified, **dtexec** fails.  
  
-   **/De[crypt]**  *密碼*：(選擇性)。 設定載入含密碼加密的封裝時，所用的解密密碼。  
  
-   (選擇性) 如果執行封裝時發生一個或多個指定的事件，會建立偵錯傾印檔案 .mdmp 和 .tmp。 *error code* 引數會指定事件代碼的類型 (錯誤、警告或資訊)，這些事件代碼將會觸發系統建立偵錯傾印檔案。 若要指定多個事件代碼，請用分號 (;) 隔開每一個「錯誤碼」引數。 *error code* 引數中請勿包含引號。  
  
     下列範例會在 DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER 錯誤發生時，產生偵錯傾印檔案。  
  
    ```  
    /Dump 0xC020801C  
    ```  
  
     **/ 傾印***錯誤碼*： 根據預設，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]偵錯傾印檔案儲存在資料夾中， *\<磁碟機 >*: \Program Files\Microsoft SQL Server\110\Shared\ErrorDumps。  
  
    > **注意：** 偵錯傾印檔案可能會包含敏感性資訊。 您可以使用存取控制清單 (ACL) 來限制這些檔案的存取權，或將這些檔案複製到具有限制性存取權的資料夾。 例如，在您將偵錯檔案傳送給 Microsoft 支援服務之前，我們建議您先移除任何敏感性或機密資訊。  
  
     如要將此選項套用到 **dtexec** 公用程式執行的所有封裝，請將 **DumpOnCodes** REG_SZ 值加入 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS\Setup\DtsPath 登錄機碼中。 **DumpOnCodes** 的資料值會指定觸發系統建立偵錯傾印檔案的錯誤碼。 多個錯誤碼必須以分號 (;) 隔開。  
  
     若您將 **DumpOnCodes** 值加入此登錄機碼中，並使用 **/Dump** 選項，系統將會建立以這兩個設定為根據的偵錯傾印檔案。  
  
     如需有關偵錯傾印檔案的詳細資訊，請參閱＜ [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)＞。  
  
-   **/DumpOnError**：(選擇性) 若執行封裝時發生任何錯誤，會建立偵錯傾印檔案 .mdmp 和 .tmp。  
  
     根據預設，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]偵錯傾印檔案儲存在資料夾中， *\<磁碟機 >*: \Program Files\Microsoft SQL Server\110\Shared\ErrorDumps 資料夾。  
  
    > **注意：** 偵錯傾印檔案可能會包含敏感性資訊。 您可以使用存取控制清單 (ACL) 來限制這些檔案的存取權，或將這些檔案複製到具有限制性存取權的資料夾。 例如，在您將偵錯檔案傳送給 Microsoft 支援服務之前，我們建議您先移除任何敏感性或機密資訊。  
  
     如要將此選項套用至 **dtexec** 公用程式執行的所有封裝，請將 **DumpOnError** REG_DWORD 值加入 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS\Setup\DtsPath 登錄機碼中。 **DumpOnError** REG_DWORD 值可指定 **/DumpOnError** 選項是否要與 **dtexec** 公用程式並用：  
  
    -   非零的資料值表示系統將會在發生任何錯誤時建立偵錯傾印檔案，不論您是否搭配 **dtexec** 公用程式使用 **/DumpOnError** 選項。  
  
    -   零的資料值表示系統將不會建立偵錯傾印檔案，除非您搭配 **/DumpOnError** 選項使用 **dtexec** 公用程式。  
  
     如需有關偵錯傾印檔案的詳細資訊，請參閱＜ [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)＞。  
  
-   **/Env[Reference]** *環境參考識別碼*：(選擇性)。 針對部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器的封裝，指定封裝執行所使用的環境參考 (ID)。 設定為繫結至變數的參數將使用環境中包含之變數的值。  
  
     您同時使用了 **/Env[Reference]** 選項以及 **/ISServer** 與 **/Server** 選項。  
  
     此參數是由 SQL Server Agent 所使用。  
  --   **/F [ile]** *filespec*: （選擇性）。 載入儲存在檔案系統中的封裝。 儲存在檔案系統中的封裝是使用舊版封裝部署模型所部署。 若要使用專案部署模型，執行部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器的封裝，請使用 **/ISServer** 選項。 如需封裝和專案部署模型的詳細資訊，請參閱＜ [Deployment of Projects and Packages](deploy-integration-services-ssis-projects-and-packages.md)＞。  

  *filespec* 引數指定封裝的路徑和檔案名稱。 您可以指定路徑為通用命名慣例 (UNC) 路徑或本機路徑。 如果 *filespec* 引數中指定的路徑或檔案名稱包含空格，必須將 *filespec* 引數括以引號。  
  
     **/File** 選項不可與 **/DTS** 或 **/SQL** 選項並用。 若指定了多個選項， **dtexec** 便會失敗。  
  
-   **/H[elp]** [*option_name*]：(選擇性)。 顯示選項的說明，或顯示指定之 *option_name* 的說明，並關閉公用程式。  
  
     如有指定 *option_name* 引數， **dtexec** 會啟動《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》，並顯示 dtexec 公用程式主題。  
  
-   **/ISServer** *packagepath*：(選擇性)。 執行部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器的封裝。 *PackagePath* 引數會指定部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器之封裝的完整路徑和檔案名稱。 如果 *PackagePath* 引數中指定的路徑或檔案名稱包含空格，必須將 *PackagePath* 引數括以引號。  
  
     封裝格式如下所示：  
  
    ```  
    \<catalog name>\<folder name>\<project name>\package file name  
    ```  
  
     您同時使用了 **/Server** 選項和 **/ISSERVER** 選項。 只有 Windows 驗證可以執行 SSIS 伺服器上的封裝。 目前的 Windows 使用者用來存取封裝。 如果省略 /Server 選項，將假設使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的預設本機執行個體。  
  
     **/ISSERVER** 選項不可與 **/DTS**、 **/SQL** 或 **/File** 選項一起使用。 如果指定了多個選項，dtexec 便會失敗。  
  
     此參數是由 SQL Server Agent 所使用。  
  
-   **/L[ogger]** *classid_orprogid;configstring*：(選擇性)。 建立一或多個記錄提供者與 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝執行作業的關聯性。 *classid_orprogid* 參數指定記錄提供者，並可指定為類別 GUID。 *configstring* 是用來設定記錄提供者的字串。  
  
     下列清單顯示可用的記錄提供者：  
  
    -   文字檔：  
  
        -   ProgID: DTS.LogProviderTextFile.1  
  
        -   ClassID: {59B2C6A5-663F-4C20-8863-C83F9B72E2EB}  
  
    -   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]:  
  
        -   ProgID: DTS.LogProviderSQLProfiler.1  
  
        -   ClassID: {5C0B8D21-E9AA-462E-BA34-30FF5F7A42A1}  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
        -   ProgID: DTS.LogProviderSQLServer.1  
  
        -   ClassID: {6AA833A1-E4B2-4431-831B-DE695049DC61}  
  
    -   Windows 事件記錄：  
  
        -   ProgID: DTS.LogProviderEventLog.1  
  
        -   ClassID: {97634F75-1DC7-4F1F-8A4C-DAF0E13AAA22}  
  
    -   XML 檔案：  
  
        -   ProgID: DTS.LogProviderXMLFile.1  
  
        -   ClassID: {AFED6884-619C-484F-9A09-F42D56E1A7EA}  
  
-   **/M[axConcurrent]** *concurrent_executables*：(選擇性)。 指定封裝可以同時執行的可執行檔數量。 指定的值必須是非負數的整數或 -1。 -1 值表示 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 允許同時執行的最大可執行檔數量，等於執行封裝之電腦上的處理器總數再加 2。  
  
-   **/Pack[age]** *PackageName*：(選擇性)。 指定所執行的封裝。 當您從 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]執行封裝時，主要會使用這個參數。  
  
-   **/P[assword]** *密碼*：(選擇性)。 允許擷取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證所保護的封裝。 此選項會與 **/User** 選項一起使用。 若省略 **/Password** 選項而使用 **/User** 選項，將會使用空白密碼。 *password* 值可括以引號。  
  
    > **重要！！** [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
-   **/Par[ameter]** [$Package:: | $Project:: | $ServerOption::] *parameter_name* [(data_type)]; *literal_value*：(選擇性)。 指定參數值。 可以指定多個 **/Parameter** 選項。 資料類型為當做字串的 CLR TypeCodes。 若是非字串的參數，則會在括號中指定資料類型，後面接著參數名稱。  
  
     **/Parameter** 選項只可搭配 **/ISServer** 選項使用。  
  
     您可以使用 $Package、$Project 和 $ServerOption 前置詞個別表示封裝參數、專案參數，以及伺服器選項參數。 預設參數類型為封裝。  
  
     以下範例會執行封裝，以及為專案參數 (myparam) 提供 myvalue，並為封裝參數 (anotherparam) 提供整數值 12。  
  
     `Dtexec /isserver “SSISDB\MyFolder\MyProject\MyPackage.dtsx” /server “.” /parameter $Project::myparam;myvalue /parameter anotherparam(int32);12`  
  
     您也可以使用參數設定連接管理員屬性。 使用 CM 前置詞代表連接管理員參數。  
  
     在以下的範例中，SourceServer 連接管理員的 InitialCatalog 屬性設定為 `ssisdb`。  
  
    ```  
    /parameter CM.SourceServer.InitialCatalog;ssisdb  
    ```  
  
     在下列範例中，SourceServer 連接管理員的 ServerName 屬性設定為句號 (.)，表示本機伺服器。  
  
    ```  
    /parameter CM.SourceServer.ServerName;.  
    ```  
  
-   **/Proj[ect]** *ProjectFile*：(選擇性)。 指定要從中擷取所執行之封裝的專案。 *ProjectFile* 引數會指定 .ispac 檔案名稱。 當您從 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]執行封裝時，主要會使用這個參數。  
  
-   **/Rem** *註解*：(選擇性)。 在命令提示字元或命令檔中加入註解。 引數是選擇性的。 *comment* 的值是一個字串，它必須以引號括住，或不包含空格。 如果未指定引數，將會插入空白行。 命令取得階段將會捨棄*comment* 值。  
  
-   **/Rep[orting]** *層級* [*;event_guid_or_name*[*;event_guid_or_name*[...]]：(選擇性)。 指定要報告的訊息類型。 *level* 可用的報告選項如下：  
  
     **N** ...無報告。  
  
     **E** ...報告錯誤。  
  
     **W** ...報告警告。  
  
     **I** ...報告參考用訊息。  
  
     **C** ...報告自訂事件。  
  
     **D** ...報告資料流程工作事件。  
  
     **P** ...報告進度。  
  
     **V** ...詳細資訊報告。  
  
     V 和 N 引數與所有其他引數互斥；這兩個引數必須單獨指定。 若未指定 **/Reporting** 選項，預設層級為 **E** (錯誤)、 **W** (警告) 及 **P** (進度)。  
  
     所有事件前面都加上 "YY/MM/DD HH:MM:SS" 格式的時間戳記，如果有 GUID 或易記名稱，也會加上它們。  
  
     選擇性參數 *event_guid_or_name* 記錄提供者的例外狀況清單。 例外狀況會指出不要記錄但可能已記錄的事件。  
  
     您不需要排除通常預設為不要記錄的事件。  
  
-   **/Res[tart]** {*deny | force | ifPossible*}：(選擇性)。 為這個封裝中的 <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> 屬性指定新值。 這些參數的意義如下：  
  
     *Deny* 將 <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> 屬性設為 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSCheckpointUsage.DTSCU_NEVER>。  
  
     *Force* 將 <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> 屬性設為 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSCheckpointUsage.DTSCU_ALWAYS>。  
  
     *ifPossible* 將 <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> 屬性設為 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSCheckpointUsage.DTSCU_IFEXISTS>。  
  
     若未指定任何值，將會使用預設值 **force** 。  
  
-   **/Set** [$Sensitive::]*propertyPath;value*：(選擇性)。 覆寫封裝內的參數、變數、屬性、容器、記錄提供者、Foreach 列舉值或連接的組態。 使用此選項時， **/Set** 會將 *propertyPath* 引數變更為指定的值。 可以指定多個 **/Set** 選項。  
  
     除了使用 **/Set** 選項與 **/F[ile]** 選項之外，您也可以使用 **/Set** 選項與 **/ISServer** 選項或 **/Project** 選項。 當您使用 **/Set** 與 **/Project**， **/Set** 會設定參數值。 當您使用 **/Set** 與 **/ISServer**， **/Set** 會設定屬性覆寫。 此外，當您一併使用 **/Set** 與 **/ISServer**時，也可使用選擇性的 $Sensitive 前置詞，指出屬性在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器上應視為要區分大小寫。  
  
     您可以執行 [封裝組態精靈] 來決定 *propertyPath* 的值。 您選取項目的路徑會顯示在最後的 **[正在完成精靈]** 頁面上，並可複製及貼上。 如果您只是為了這個目的而使用精靈，可以在複製路徑之後取消精靈。  
  
     下列範例會執行儲存在檔案系統中的封裝並提供變數的新值：  
  
     `dtexec /f mypackage.dtsx /set \package.variables[myvariable].Value;myvalue`  
  
     下列範例會從 .ispac 專案檔案執行封裝，並設定封裝與專案參數。  
  
     `/Project c:\project.ispac /Package Package1.dtsx /SET \Package.Variables[$Package::Parameter];1 /SET \Package.Variables[$Project::Parameter];1`  
  
     您可以使用 **/Set** 選項變更載入封裝組態的來源位置。 但您不可使用 **/Set** 選項覆寫先前在設計階段由組態所指定的值。 若要了解如何套用封裝組態，請參閱 [封裝組態](../../integration-services/packages/package-configurations.md) 和 [SQL Server 2016 中 Integration Services 功能的行為變更](http://msdn.microsoft.com/library/611d22fa-5ac7-485e-9a40-7131e852f794)。  
  
-   **/Ser[ver]** *伺服器*：(選擇性)。 指定 **/SQL** 或 **/DTS** 選項時，此選項會指定要擷取封裝的來源伺服器名稱。 若省略 **/Server** 選項而指定了 **/SQL** 或 **/DTS** 選項，將會嘗試對本機伺服器執行封裝作業。 *server_instance* 值可能會加上引號。  
  
     指定 **/ISServer** 選項時，需要 **/Ser[ver]** 選項。  
  
--   **/SQ [L]** *package_path*： 載入儲存在封裝[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請在**msdb**資料庫。 儲存在 **msdb** 資料庫中的封裝是使用封裝部署模型所部署。 若要使用專案部署模型，執行部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器的封裝，請使用 **/ISServer** 選項。 如需有關封裝和專案部署模型的詳細資訊，請參閱＜ [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx)＞。   
  
     The *package_path* argument specifies the name of the package to retrieve. If folders are included in the path, they are terminated with backslashes ("\\"). The *package_path* value can be quoted. If the path or file name specified in the *package_path* argument contains a space, you must put quotation marks around the *package_path* argument.  
  
     You can use the **/User**, **/Password**, and **/Server** options together with the **/SQL** option.  
  
     If you omit the **/User** option, Windows Authentication is used to access the package. If you use the **/User** option, the **/User** login name specified is associated with [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentication.  
  
     The **/Password** option is used only together with the **/User** option. If you use the **/Password** option, the package is accessed with the user name and password information provided. If you omit the **/Password** option, a blank password is used.  
  
    > **IMPORTANT!!** [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
     If the **/Server** option is omitted, the default local instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] is assumed.  
  
     The **/SQL** option cannot be used together with the **/DTS** or **/File** option. If multiple options are specified, **dtexec** fails.  
  
-   **/Su[m]**：(選擇性)。 顯示包含下一個元件將接收之列數的累加計數器。  
  
-   **/U[ser]** *user_name*：(選擇性)。 允許擷取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證所保護的封裝。 只有在指定 **/SQL** 選項時，才會使用此選項。 *user_name* 值可以引號括住。  
  
    > **重要！！**  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
-   **/Va[lidate]**：(選擇性)。 在驗證階段之後，停止執行封裝 (並不會實際執行封裝)。 在驗證期間使用 **/WarnAsError** 選項，會導致 **dtexec** 將警告視為錯誤，進而造成驗證期間發生警告，即會致使封裝失敗。  
  
-   **/VerifyB[uild]** *major*[*;minor*[*;build*]]：(選擇性)。 根據驗證階段期間在 *major*、 *minor*及 *build* 引數指定的組建編號，來驗證封裝的組建編號。 如果發生不符的情形，將不會執行封裝。  
  
     這些值是 Long 整數。 此引數可以是下列這三種格式的其中一種，而且 *major* 的值永遠是必要的：  
  
    -   *major*  
  
    -   *major*;*minor*  
  
    -   *major*; *minor*; *build*  
  
-   **/VerifyP[ackageID]** *packageID*：(選擇性)。 將封裝 GUID 與 *package_id* 引數所指定的值進行比較，藉此驗證要執行之封裝的 GUID。  
  
-   **/VerifyS[igned]**：(選擇性)。 使 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 檢查封裝的數位簽章。 如果此封裝未簽署或是簽章無效，此封裝就會失敗。 如需詳細資訊，請參閱 [使用數位簽章來識別封裝的來源](../../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md)。  
  
    > **重要！！** 當 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 設定為檢查封裝的簽章時，將只會檢查數位簽章是否存在、是否有效，以及是否來自信任的來源。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 不會檢查封裝是否經過變更。  
  
    > **注意：** 選擇性的 **BlockedSignatureStates** 登錄值所指定的設定，可以比 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中所設定或 **dtexec** 命令列上所設定的數位簽章選項更具限制性。 在此情況下，更具限制性的登錄設定會覆寫其他設定。  
  
-   **/VerifyV[ersionID]** *versionID*：(選擇性)。 在封裝驗證階段期間，將封裝的版本 GUID 與 *version_id* 引數所指定的值進行比較，藉此驗證要執行之封裝的版本 GUID。  
  
-   **/VLog** *[Filespec]*：(選擇性)。 將所有 Integration Services 封裝事件寫入設計封裝時啟用的記錄提供者。 若要讓 Integration Services 啟用文字檔的記錄提供者，並將記錄事件寫入指定的文字檔，請以 *Filespec* 參數的形式包含路徑和檔案名稱。  
  
     如果您未包含 *Filespec* 參數，Integration Services 將不會啟用文字檔的記錄提供者。 Integration Services 只會將記錄事件寫入設計封裝時啟用的記錄提供者。  
  
-   **/W[arnAsError]**：(選擇性)。 使封裝將警告視為錯誤，因此，當驗證期間發生警告時，封裝便會失敗。 若驗證期間未發生警告，亦未指定 **/Validate** 選項，即會執行封裝。  
  
-   **/X86**：(選擇性)。 使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 在 64 位元電腦上以 32 位元模式執行封裝。 當下列條件都成立時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 就會設定這個選項：  
  
    -   作業步驟類型是 **[SQL Server Integration Services 封裝]**。  
  
    -   已經在 **[新增作業步驟]** 對話方塊的 **[執行選項]** 索引標籤上選取 **[使用 32 位元執行階段]** 選項。  
  
     您也可以針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業步驟設定此選項，方法是使用預存程序或 SQL Server 管理物件 (SMO)，以程式設計方式建立作業。  
  
     這個選項只能由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 使用。 若在命令提示字元處執行 **dtexec** 公用程式，系統將會忽略此選項。  
  
##  <a name="remark"></a> 備註  
 命令選項的指定順序可能會影響封裝的執行方式：  
  
-   依照在命令列中發現選項的順序來處理選項。 在命令列上發現命令檔案時便會加以讀取， 命令檔案中的命令也就會依照發現的順序來處理。  
  
-   如果相同選項、參數或變數在同一個命令列陳述式中重複出現，以選項的最後一個執行個體優先。  
  
-   **/Set** 與 **/ConfigFile** 選項會依據發現的順序進行處理。  
  
##  <a name="example"></a> 範例  
 下列範例示範如何使用 **dtexec** 命令提示字元公用程式，設定及執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
 **執行封裝**  
  
 若要利用 Windows 驗證來執行儲存至 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 封裝，請使用下列程式碼：  
  
```  
dtexec /sq pkgOne /ser productionServer  
```  
  
 若要執行儲存到 SSIS 封裝存放區中檔案系統資料夾的 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝，請使用下列程式碼：  
  
```  
dtexec /dts "\File System\MyPackage"  
```  
  
 若要在不執行封裝的情況下，驗證使用 Windows 驗證且儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的封裝，請使用下列程式碼：  
  
```  
dtexec /sq pkgOne /ser productionServer /va  
```  
  
 若要執行儲存在檔案系統中的 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝，請使用下列程式碼：  
  
```  
dtexec /f "c:\pkgOne.dtsx"   
```  
  
 若要執行儲存在檔案系統中的 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝，且要指定記錄選項，請使用下列程式碼：  
  
```  
dtexec /f "c:\pkgOne.dtsx" /l "DTS.LogProviderTextFile;c:\log.txt"  
```  
  
 若要執行使用 Windows 驗證、儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的預設本機執行個體，且會在執行之前確認版本的封裝，請使用下列程式碼：  
  
```  
dtexec /sq pkgOne /verifyv {c200e360-38c5-11c5-11ce-ae62-08002b2b79ef}  
```  
  
 若要執行儲存在檔案系統中且在外部進行設定的 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝，請使用下列程式碼：  
  
```  
dtexec /f "c:\pkgOne.dtsx" /conf "c:\pkgOneConfig.cfg"  
```  
  
> **注意：** 如果路徑或檔案名稱中包含空格，就必須將 /SQL、/DTS 或 /FILE 選項的 *package_path* 或 *filespec* 引數包含在引號中。 如果引數沒有用引號括住，則引數不能包含空格。  
  
 **記錄選項**  
  
 若有三個記錄項目類型 A、B 和 C，下列不含參數的 **ConsoleLog** 選項會顯示這三個記錄類型及其所有欄位：  
  
```  
/CONSOLELOG  
```  
  
 下列選項會顯示所有記錄類型，但只會顯示 [名稱] 和 [訊息] 資料行：  
  
```  
/CONSOLELOG NM  
```  
  
 下列選項只會顯示記錄項目類型 A 的所有資料行：  
  
```  
/CONSOLELOG I;LogEntryTypeA  
```  
  
 下列選項只會顯示記錄項目類型 A 及其 [名稱] 和 [訊息] 資料行：  
  
```  
/CONSOLELOG NM;I;LogEntryTypeA  
```  
  
 下列選項會顯示記錄項目類型 A 和 B 的記錄項目：  
  
```  
/CONSOLELOG I;LogEntryTypeA;LogEntryTypeB  
```  
  
 您可以利用多個 **ConsoleLog** 選項來達到相同結果：  
  
```  
/CONSOLELOG I;LogEntryTypeA /CONSOLELOG I;LogEntryTypeB  
```  
  
 若使用 **ConsoleLog** 選項時不含參數，則會顯示所有欄位。 若包含 *list_options* 參數會使下列命令只顯示記錄項目 A 及其所有欄位：  
  
```  
/CONSOLELOG NM;I;LogEntryTypeA /CONSOLELOG  
```  
  
 下列項目會顯示記錄項目類型 A 以外的所有記錄項目；也就是說，它只會顯示記錄項目類型 B 和 C：  
  
```  
/CONSOLELOG E;LogEntryTypeA  
```  
  
 下列範例會利用多個 **ConsoleLog** 選項和單一排除項來達到相同結果：  
  
```  
/CONSOLELOG E;LogEntryTypeA /CONSOLELOG  
/CONSOLELOG E;LogEntryTypeA /CONSOLELOG E;LogEntryTypeA  
/CONSOLELOG E;LogEntryTypeA;LogEntryTypeA  
```  
  
 下列範例不會顯示任何記錄訊息，因為當記錄檔類型同時在包含和排除的清單中找到時，就會將它排除。  
  
```  
/CONSOLELOG E;LogEntryTypeA /CONSOLELOG I;LogEntryTypeA  
```  
  
 **SET 選項**  
  
 以下顯示如何使用 **/SET** 選項在從命令列啟動封裝時，變更任何封裝屬性或變數的值。  
  
```  
/SET \package\DataFlowTask.Variables[User::MyVariable].Value;newValue  
```  
  
 **專案選項**  
  
 下列範例顯示如何使用 **/Project** 及 **/Package** 選項。  
  
```  
/Project c:\project.ispac /Package Package1.dtsx  
```  
  
 下列範例顯示如何使用 **/Project** 和 **/Package** 選項，以及設定封裝和專案參數。  
  
```  
/Project c:\project.ispac /Package Package1.dtsx /SET \Package.Variables[$Package::Parameter];1 /SET \Package.Variables[$Project::Parameter];1  
  
```  
  
 **ISServer 選項**  
  
 下列範例顯示如何使用 **/ISServer** 選項。  
  
```  
dtexec /isserver "\SSISDB\MyFolder\MyProject\MyPackage.dtsx" /server "."  
```  
  
 下列範例顯示如何使用 **/ISServer** 選項，以及設定專案和連接管理員參數。  
  
```  
/Server localhost /ISServer “\SSISDB\MyFolder\Integration Services Project1\Package.dtsx” /Par "$Project::ProjectParameter(Int32)";1 /Par "CM.SourceServer.InitialCatalog";SourceDB  
  
```  
  
## <a name="related-content"></a>相關內容  
 www.mattmasson.com 上的部落格文章： [結束碼、DTEXEC 和 SSIS 目錄](http://www.mattmasson.com/2012/02/exit-codes-dtexec-and-ssis-catalog/)。  
  
  

