---
title: dtutil 公用程式 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- verifying packages
- checking packages
- moving packages
- packages [Integration Services], command line options
- command prompt [Integration Services]
- SQL Server Integration Services packages, command line options
- copying packages
- existence testing [Integration Services]
- Integration Services packages, command line options
- SSIS packages, command line options
- deleting packages
- dtutil utility
- removing packages
- relocating packages
ms.assetid: 6c7975ff-acec-4e6e-82e5-a641e3a98afe
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 19f179ae869a175ea6238ba4ade9e5f87d663e08
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "71297793"
---
# <a name="dtutil-utility"></a>Encrypt

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **dtutil** 命令提示字元公用程式可用來管理 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 套件。 這個公用程式可以複製、移動、刪除封裝，或確認封裝是否存在。 下列三個位置之一所儲存的任何 [!INCLUDE[ssIS](../includes/ssis-md.md)] 套件都可以執行這些動作：[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫、[!INCLUDE[ssIS](../includes/ssis-md.md)] 套件存放區和檔案系統。 如果公用程式存取存放在 **msdb**中的封裝，則命令提示字元可能會需要使用者名稱和密碼。 如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證，則命令提示字元需要使用者名稱和密碼。 如果遺漏使用者名稱， **dtutil** 會嘗試使用 Windows 驗證登入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。 封裝的儲存類型是由 **/SQL**、 **/FILE**和 **/DTS** 等選項來識別。  
  
 **dtutil** 命令提示字元公用程式不支援使用命令檔或重新導向。  
  
 **dtutil** 命令提示公用程式包含下列功能：  
  
-   命令提示字元中的備註，會自動記錄命令提示字元動作，並使其易於了解。  
  
-   覆寫保護，會在您複製或移動封裝時，在覆寫現有封裝之前提示您進行確認。  
  
-   主控台說明，可提供有關 **dtutil**命令選項的資訊。  
  
> [!NOTE]  
>  您也可以在連接到 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 的執行個體時，透過 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]以視覺化方式執行 dtutil 所執行的許多作業。 如需詳細資訊，請參閱[封裝管理 &#40;SSIS 服務&#41;](../integration-services/service/package-management-ssis-service.md)。  
  
 您可以依照任何順序來輸入這些選項。 垂直線 ("|") 字元是 **OR** 運算子，用來顯示可能的值。 您必須使用以 **OR** 垂直線分隔的其中一個選項。  
  
 所有選項的開頭都必須是斜線 (/) 或減號 (-)。 但是，請勿在斜線或減號與選項的文字之間加入空格，否則此命令會失敗。  
  
 引數必須是加上引號的字串，或不含空白的字串。  
  
 加上引號的字串之內的雙引號代表逸出的單引號。  
  
 除了密碼以外，選項和引數都沒有區分大小寫。  
  
 **64 位元電腦上的安裝考量**  
  
 在 64 位元電腦上， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 會安裝 64 位元版本的 **dtexec** 公用程式 (dtexec.exe) 和 **dtutil** 公用程式 (dtutil.exe)。 若要安裝 32 位元版本的這些 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 工具，您必須在安裝期間選取用戶端工具或 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 。  
  
 根據預設，同時安裝了 64 位元和 32 位元版之 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 命令提示字元公用程式的 64 位元電腦將會在命令提示字元上執行 32 位元版本。 執行 32 位元版本是因為 32 位元版本的目錄路徑在 PATH 環境變數中會出現在 64 位元版本的目錄路徑前面 (一般來說，32 位元的目錄路徑是 \<磁碟機>:\Program Files(x86)\Microsoft SQL Server\130\DTS\Binn，而 64 位元的目錄路徑是 \<磁碟機>:\Program Files\Microsoft SQL Server\130\DTS\Binn)。  
  
> [!NOTE]  
>  如果您使用 SQL Server Agent 執行此公用程式，SQL Server Agent 會自動使用 64 位元版的公用程式。 SQL Server Agent 會使用此登錄 (而不是 PATH 環境變數) 來尋找此公用程式的正確可執行檔。  
  
 若要確保您可在命令提示字元上執行 64 位元版的公用程式，您可以採取下列其中一個動作：  
  
-   開啟 [命令提示字元] 視窗，然後將目錄切換到包含 64 位元版公用程式的目錄 (\<磁碟機>:\Program Files\Microsoft SQL Server\130\DTS\Binn)，再從該位置執行公用程式。  
  
-   在命令提示字元上，輸入 64 位元版公用程式的完整路徑 (\<磁碟機>:\Program Files\Microsoft SQL Server\130\DTS\Binn)，以執行此公用程式。  
  
-   在 PATH 環境變數中將 64 位元路徑 (\<磁碟機>:\Program Files\Microsoft SQL Server\130\DTS\Binn) 置於 32 位元路徑 (\<磁碟機>:\ Program Files(x86)\Microsoft SQL Server\130\DTS\Binn) 之前，可以永久變更該變數中的路徑順序。  
  
## <a name="syntax"></a>語法  
  
```dos
dtutil /option [value] [/option [value]]...  
```  
  
#### <a name="parameters"></a>參數  
  
|選項|描述|  
|------------|-----------------|  
|/?|顯示命令提示字元選項。|  
|/C[opy] *location;destinationPathandPackageName*|對 [!INCLUDE[ssIS](../includes/ssis-md.md)] 封裝指定複製動作。 若要使用此參數，您必須先使用 **/FI**、 **/SQ**或 **/DT** 選項來指定封裝的位置。 接下來，指定目的地位置目的地封裝名稱。 *destinationPathandPackageName* 引數指定複製 [!INCLUDE[ssIS](../includes/ssis-md.md)] 封裝所在的位置。 如果目的地 *location* 是 **SQL**，則也必須在命令中指定 *DestUser*、 *DestPassword* 和 *DestServer* 引數。<br /><br /> 當 **Copy** 動作發現目的地有現有的封裝時， **dtutil** 會提示使用者確認是否要刪除封裝。 **Y** 回覆會覆寫封裝， **N** 回覆會結束程式。 當命令包含 *Quiet* 引數時，不會出現提示，並且會覆寫任何現有的封裝。|  
|/Dec[rypt] *password*|(選擇性)。 設定載入含密碼加密的封裝時，所用的解密密碼。|  
|/Del[ete]|刪除 *SQL*、 *DTS* 或 *FILE* 選項所指定的封裝。 如果 **dtutil** 無法刪除封裝，程式便會結束。|  
|/DestP[assword] *password*|指定搭配 SQL 選項來連接使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證之目的地 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體時，所使用的密碼。 如果 *DESTPASSWORD* 是指定在不含 *DTSUSER* 選項的命令列上，則會產生錯誤。<br /><br /> 注意： [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]。|  
|/DestS[erver] *server_instance*|指定以任何動作搭配使用的伺服器名稱，這些動作會使目的地儲存在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中的。 當儲存 [!INCLUDE[ssIS](../includes/ssis-md.md)] 封裝時，它用來識別非本機或非預設的伺服器。 在不含與 *相關聯動作的命令列上指定* DESTSERVER [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]是錯的。 *SIGN SQL*、 *COPY SQL*或 *MOVE SQL* 選項之類的動作，就是結合這個選項的適當命令。<br /><br /> 您可以在伺服器名稱中加入反斜線和執行個體名稱來指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體的名稱。|  
|/DestU[ser] *username*|指定與 *SIGN SQL*、 *COPY SQL*和 *MOVE SQL* 選項一起使用的使用者名稱，以連接到使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體。 在不含 *DESTUSER* 、 *SIGN SQL*或 *COPY SQL*選項的命令列上指定 *MOVE SQL* 是錯的。|  
|/Dump *處理序識別碼*|(選擇性) 讓指定的處理序 ( **dtexec** 公用程式或 **dtsDebugHost.exe** 處理序) 暫停，並建立偵錯傾印檔案 .mdmp 和 .tmp。<br /><br /> 注意：若要使用 **/Dump**選項，您必須被指派「偵錯程式」使用者權限 (SeDebugPrivilege)。<br /><br /> 若要找出您想要暫停之處理序的 *process ID* ，請使用 Windows 工作管理員。<br /><br /> 根據預設，[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 會將偵錯傾印檔案儲存在 \<磁碟機>:\Program Files\Microsoft SQL Server\130\Shared\ErrorDumps 資料夾中。<br /><br /> 如需 **dtexec** 公用程式和 **dtsDebugHost.exe** 處理序的詳細資訊，請參閱 [dtexec Utility](../integration-services/packages/dtexec-utility.md) 和 [Building, Deploying, and Debugging Custom Objects](../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)。<br /><br /> 如需有關偵錯傾印檔案的詳細資訊，請參閱＜ [Generating Dump Files for Package Execution](../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)＞。<br /><br /> 注意：偵錯傾印檔案可能會包含敏感性資訊。 您可以使用存取控制清單 (ACL) 來限制這些檔案的存取權，或將這些檔案複製到具有限制性存取權的資料夾。|  
|/DT[S] *filespec*|指定要處理的 [!INCLUDE[ssIS](../includes/ssis-md.md)] 封裝是在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 封裝存放區中。 *filespec* 引數必須包含資料夾路徑，並以 [!INCLUDE[ssIS](../includes/ssis-md.md)] 封裝存放區的根目錄為開頭。 根據預設，組態檔中根資料夾的名稱為 "MSDB" 和 "File System"。 您必須使用雙引號來隔開包含空格的路徑。<br /><br /> 如果 DT[S] 選項是指定在與下列任何選項相同的命令列上，則會傳回 DTEXEC_DTEXECERROR：<br /><br /> **FILE**<br /><br /> **SQL**<br /><br /> **SOURCEUSER**<br /><br /> **SOURCEPASSWORD**<br /><br /> **SOURCESERVER**|  
|/En[crypt] *{SQL &#124; FILE}; Path;ProtectionLevel[;password]*|(選擇性)。 利用指定的保護等級和密碼來加密載入的封裝，並將它儲存在 *Path*所指定的位置中。 *ProtectionLevel* 用來決定是否需要密碼。<br /><br /> *SQL* - 路徑是目的地封裝名稱。<br /><br /> *FILE* - 路徑是指封裝的完整路徑和檔案名稱。<br /><br /> *DTS* - 目前不支援此選項。<br /><br /> *ProtectionLevel* 選項：<br /><br /> 等級 0：解除機密資訊。<br /><br /> 等級 1：機密資訊使用本機使用者認證加密。<br /><br /> 等級 2：機密資訊使用必要的密碼加密。<br /><br /> 等級 3：封裝使用必要的密碼加密。<br /><br /> 等級 4：封裝使用本機使用者認證加密。<br /><br /> 等級 5：封裝使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 儲存體加密。|  
|/Ex[ists]|(選擇性)。 用來判斷封裝是否存在。 **dtutil** 會嘗試找出透過 *SQL*、 *DTS* 或 *FILE* 選項所指定的封裝。 如果 **dtutil** 找不到指定的封裝，就會傳回 DTEXEC_DTEXECERROR。|  
|/FC[reate] {*SQL* &#124; *DTS*};*ParentFolderPath;NewFolderName*|(選擇性)。 建立內含您在 *NewFolderName*所指定之名稱的新資料夾。 *ParentFolderPath*指出新資料夾的位置。|  
|/FDe[lete] {*SQL* &#124; *DTS*}[;*ParentFolderPath;FolderName]*|(選擇性)。 從 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssIS](../includes/ssis-md.md)] 刪除 *FolderName*中之名稱所指定的資料夾。 *ParentFolderPath*指出要刪除之資料夾的位置。|  
|/FDi[rectory] {*SQL* &#124; *DTS*};*FolderPath[;S]*|(選擇性)。 列出 [!INCLUDE[ssIS](../includes/ssis-md.md)] 或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的資料夾內容，其中包括資料夾和封裝。 選擇性的 *FolderPath* 參數指定您要檢視其內容的資料夾。 選擇性的 *S* 參數指定您想要檢視 *FolderPath*所指定資料夾的子資料夾內容清單。|  
|/FE[xists ] {*SQL* &#124; *DTS*};*FolderPath*|(選擇性)。 確認指定的資料夾存在於 [!INCLUDE[ssIS](../includes/ssis-md.md)] 或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中。 *FolderPath* 參數是要驗證之資料夾的路徑和名稱。|  
|/Fi[le] *filespec*|這個選項指定要處理的 [!INCLUDE[ssIS](../includes/ssis-md.md)] 封裝是在檔案系統中。 *filespec* 值可提供為通用命名慣例 (UNC) 路徑或本機路徑。<br /><br /> 如果在下列任何選項的相同命令列中指定 *File* 選項，就會傳回 DTEXEC_DTEXECERROR：<br /><br /> **DTS**<br /><br /> **SQL**<br /><br /> **SOURCEUSER**<br /><br /> **SOURCEPASSWORD**<br /><br /> **SOURCESERVER**|  
|/FR[ename] {*SQL* &#124; *DTS*} [;*ParentFolderPath; OldFolderName;NewFolderName]*|(選擇性)。 重新命名 [!INCLUDE[ssIS](../includes/ssis-md.md)] 或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的資料夾。 *ParentFolderPath* 是要重新命名之資料夾的位置。 *OldFolderName* 是資料夾目前的名稱， *NewFolderName* 是要提供給資料夾的新名稱。|  
|/H[elp] *選項*|顯示文字擴充說明來示範 **dtutil** 選項及描述其用法。 option 引數是選擇性的。 如果包含這個引數，說明文字會包括指定選項的詳細資訊。 下列範例會顯示所有選項的說明：<br /><br /> `dtutil /H`<br /><br /> 下列兩個範例顯示如何使用 */H* 選項來顯示特定選項的擴充說明，例如本範例中的 */Q [uiet]* 選項：<br /><br /> `dtutil /Help Quiet`<br /><br /> `dtutil /H Q`|  
|/I[DRegenerate]|建立封裝的新 GUID 及更新封裝識別碼屬性。 複製封裝時，封裝識別碼保持不變；因此，記錄檔包含兩個封裝相同的 GUID。 此動做為新複製的封裝建立新的 GUID，以便與原始封裝區別。|  
|/M[ove] {*SQL* &#124; *File* &#124; *DTS*}; *pathandname*|對 [!INCLUDE[ssIS](../includes/ssis-md.md)] 封裝指定移動動作。 若要使用此參數，請先使用 **/FI**、 **/SQ**或 **/DT** 選項來指定封裝的位置。 接下來，指定 **Move** 動作。 這個動作需要兩個以分號分隔的引數：<br /><br /> 目的地引數可指定 *SQL*、 *FILE*或 *DTS*。 *SQL* 目的地可包含 *DESTUSER*、 *DESTPASSWORD*和 *DESTSERVER* 選項。<br /><br /> *pathandname* 引數指定封裝位置： *SQL* 使用封裝路徑和封裝名稱， *FILE* 使用 UNC 或本機路徑， *DTS* 使用相對於 [!INCLUDE[ssIS](../includes/ssis-md.md)] 封裝存放區根目錄的位置。 當目的地為 *FILE* 或 *DTS*時，路徑引數不包含檔案名稱。 而是使用在指定位置的封裝名稱來做為檔案名稱。<br /><br /> <br /><br /> 當 **MOVE** 動作在目的地發現現有的封裝時， **dtutil** 會提示您確認是否要覆寫該封裝。 **Y** 回覆會覆寫封裝， **N** 回覆會結束程式。 當命令包含 *QUIET* 選項時，不會出現提示，並且會覆寫任何現有的封裝。|  
|/Q[uiet]|停止執行包含 **COPY**、 **MOVE**或 **SIGN** 選項的命令時所可能出現的確認提示。 如果目的地電腦中已有指定封裝的同名封裝，或已簽署了指定的封裝，就會出現這些提示。|  
|/R[emark] *text*|在命令列中加入註解。 註解引數是選擇性的。 如果註解文字包括空格，就必須用引號括住文字。 您可以在單一命令列中併入多個 REM 選項。|  
|/Si[gn] {*SQL* &#124; *File* &#124; *DTS*}; *path*; *hash*|簽署 [!INCLUDE[ssIS](../includes/ssis-md.md)] 封裝。 這個動作需要使用三個以分號分隔的引數 (目的地、路徑及雜湊)：<br /><br /> 目的地引數可指定 *SQL*、 *FILE*或 *DTS*。 SQL 目的地可包含 *DESTUSER*、 *DESTPASSWORD* 和 *DESTSERVER* 選項。<br /><br /> path 引數指定要處理之封裝的位置。<br /><br /> hash 引數指定用可變長度十六進位字串來表示的憑證識別碼。<br /><br /> 如需詳細資訊，請參閱 [Identify the Source of Packages with Digital Signatures](../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md)(使用數位簽章識別封裝來源)。<br /><br /> <br /><br /> **\*\* 重要事項 \*\*** 當 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 設定為檢查封裝的簽章時，將只會檢查數位簽章是否存在、是否有效，以及是否來自信任的來源。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]「不會」  檢查套件是否經過變更。|  
|/SourceP[assword] *password*|指定 *SQL* 和 *SOURCEUSER* 選項使用的密碼，以擷取儲存在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 執行個體上之資料庫中的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體時，所使用的密碼。 在不含 *SOURCEUSER* 選項的命令列上指定 **SOURCEPASSWORD** 是錯的。<br /><br /> 注意：[!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]|  
|/SourceS[erver] *server_instance*|指定與 **SQL** 選項一起使用的伺服器名稱，以擷取 [!INCLUDE[ssIS](../includes/ssis-md.md)] 中所儲存之 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 在不含 *SIGN SQL*、*COPY* *SQL* 或 *MOVE* *SQL* 選項的命令列上指定 *SOURCESERVER* 是一項錯誤。<br /><br /> 您可以在伺服器名稱中加入反斜線和執行個體名稱來指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體的名稱。|  
|/SourceU[ser] *username*|指定與 *SOURCESERVER* 選項一起使用的伺服器名稱，以擷取 [!INCLUDE[ssIS](../includes/ssis-md.md)] 驗證之 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體時，所使用的密碼。 在不含 *SOURCEUSER* 、 *SIGN SQL*或 *COPY SQL*選項的命令列上指定 *MOVE SQL* 是錯的。<br /><br /> 注意：[!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]|  
|/SQ[L] *package_path*|指定 [!INCLUDE[ssIS](../includes/ssis-md.md)] 封裝的位置。 這個選項指出封裝儲存在 **msdb** 資料庫中。 *package_path* 引數指定 [!INCLUDE[ssIS](../includes/ssis-md.md)] 封裝的路徑和名稱。 資料夾名稱以反斜線做為結尾。<br /><br /> 如果在下列任何選項的相同命令列中指定 *SQL* 選項，就會傳回 DTEXEC_DTEXECERROR：<br /><br /> *DTS*<br /><br /> *FILE*<br /><br /> *SQL* 選項可附帶下列選項中的零個或一個執行個體：<br /><br /> *SOURCEUSER*<br /><br /> *SOURCEPASSWORD*<br /><br /> *SOURCESERVER*<br /><br /> <br /><br /> 如果未加入 *SOURCEUSERNAME* ，將會使用 Windows 驗證存取封裝。 只有在*SOURCEPASSWORD* 存在時，才允許使用 *SOURCEUSER* 。 如果不包含 *SOURCEPASSWORD* ，則使用空白密碼。<br /><br /> **\*\* 重要事項 \*\*** [!INCLUDE[ssNoteStrongPass](../includes/ssnotestrongpass-md.md)]|  
  
## <a name="dtutil-exit-codes"></a>dtutil 結束碼  
 **dtutil** 可設定結束碼，以便在偵測到語法錯誤、使用不正確的引數或指定無效的選項組合時，向您發出警告。 否則，公用程式就會報告「已成功地完成作業」。下表將列出封裝作業結束時， **dtutil** 公用程式所能設定的值。  
  
|值|描述|  
|-----------|-----------------|  
|0|已順利執行公用程式。|  
|1|公用程式失敗。|  
|4|公用程式找不到所要求的封裝。|  
|5|公用程式無法載入所要求的封裝。|  
|6|公用程式無法解析命令列，因為它包含語法或語意錯誤。|  
  
## <a name="remarks"></a>備註  
 您無法搭配 **dtutil**使用命令檔或重新導向。  
  
 命令列的選項順序不重要。  
  
## <a name="examples"></a>範例  
 下列範例詳細說明一般命令列的使用狀況。  
  
### <a name="copy-examples"></a>複製範例  
 若要將儲存在 **本機執行個體 (使用 Windows 驗證) 上** msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫中的封裝，複製到 SSIS 封裝存放區，請使用下列語法：  
  
```dos
dtutil /SQL srcPackage /COPY DTS;destFolder\destPackage   
```  
  
 若要從檔案系統的某個位置中，將封裝複製到另一個位置，並將這個副本命名為另一個名稱，請使用下列語法：  
  
```dos
dtutil /FILE c:\myPackages\mypackage.dtsx /COPY FILE;c:\myTestPackages\mynewpackage.dtsx  
```  
  
 若要將本機檔案系統中的封裝複製到另一部電腦中的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體，請使用下列語法：  
  
```dos
dtutil /FILE c:\sourcepkg.dtsx /DestServer <servername> /COPY SQL;destpkgname  
```  
  
 因為不使用 */DestU[ser]* 和 */DestP[assword]* 選項，所以採用 Windows 驗證。  
  
 若要在複製封裝之後建立封裝的新識別碼，請使用下列語法：  
  
```dos
dtutil /I /FILE copiedpkg.dtsx   
```  
  
 若要為特定資料夾的所有封裝建立新的識別碼，請使用下列語法：  
  
```dos
for %%f in (C:\test\SSISPackages\*.dtsx) do dtutil.exe /I /FILE %%f  
```  
  
 在命令提示字元下輸入命令時，請使用單一百分比符號 (%)。 若命令是使用在批次檔內，則使用雙百分比符號 (%%)。  
  
### <a name="delete-examples"></a>刪除範例  
 若要刪除使用 Windows 驗證之 **執行個體上** msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫中所儲存的封裝，請使用下列語法：  
  
```dos
dtutil /SQL delPackage /DELETE  
```  
  
 若要刪除使用 **驗證之** 執行個體上 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫中所儲存的封裝，請使用下列語法：  
  
```dos
dtutil /SQL delPackage /SOURCEUSER srcUserName /SOURCEPASSWORD #8nGs*w7F /DELETE  
```  
  
> [!NOTE]  
>  若要刪除具名伺服器中的封裝，請併入 **SOURCESERVER** 選項及其引數。 您只能利用 *SQL* 選項來指定伺服器。  
  
 若要刪除儲存在 SSIS 封裝存放區中的封裝，請使用下列語法：  
  
```dos
dtutil /DTS delPackage.dtsx /DELETE  
```  
  
 若要刪除儲存在檔案系統的封裝，請使用下列語法：  
  
```dos
dtutil /FILE c:\delPackage.dtsx /DELETE  
```  
  
### <a name="exists-examples"></a>存在範例  
 若要判斷使用 Windows 驗證之 **本機執行個體上** msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫中是否存在某個封裝，請使用下列語法：  
  
```dos
dtutil /SQL srcPackage /EXISTS  
```  
  
 若要判斷使用 **驗證之** 本機執行個體上 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫中是否存在某個封裝，請使用下列語法：  
  
```dos
dtutil /SQL srcPackage /SOURCEUSER srcUserName /SOURCEPASSWORD *hY$d56b /EXISTS  
```  
  
> [!NOTE]  
>  若要判斷具名伺服器中是否存在某個封裝，請併入 **SOURCESERVER** 選項及其引數。 您只能利用 SQL 選項來指定伺服器。  
  
 若要判斷封裝是否存在於本機封裝存放區內，請使用下列語法：  
  
```dos
dtutil /DTS srcPackage.dtsx /EXISTS  
```  
  
 若要判斷本機檔案系統中是否存在某個封裝，請使用下列語法：  
  
```dos
dtutil /FILE c:\srcPackage.dtsx /EXISTS  
```  
  
### <a name="move-examples"></a>移動範例  
 若要將儲存在 SSIS 封裝存放區內的封裝移到 **本機執行個體 (使用 Windows 驗證) 上的** msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫中，請使用下列語法：  
  
```dos
dtutil /DTS srcPackage.dtsx /MOVE SQL;destPackage  
```  
  
 若要將儲存在使用 **驗證之** 本機執行個體上 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫中的封裝，移到使用 **驗證之另一個** 本機執行個體上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫，請使用下列語法：  
  
```dos
dtutil /SQL srcPackage /SOURCEUSER srcUserName /SOURCEPASSWORD $Hj45jhd@X /MOVE SQL;destPackage /DESTUSER destUserName /DESTPASSWORD !38dsFH@v  
```  
  
> [!NOTE]  
>  若要在具名伺服器之間移動封裝，請併入 **SOURCES** 和 **DESTS** 選項及其引數。 您只能使用 *SQL* 選項來指定伺服器。  
  
 若要移除儲存在 SSIS 封裝存放區中的封裝，請使用下列語法：  
  
```dos
dtutil /DTS srcPackage.dtsx /MOVE DTS;destPackage.dtsx  
```  
  
 若要移動檔案系統所儲存的封裝，請使用下列語法：  
  
```dos
dtutil /FILE c:\srcPackage.dtsx /MOVE FILE;c:\destPackage.dtsx  
```  
  
### <a name="sign-examples"></a>簽署範例  
 若要簽署使用 Windows 驗證之 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 本機執行個體的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫所儲存的封裝，請使用下列語法：  
  
```dos
dtutil /FILE srcPackage.dtsx /SIGN FILE;destpkg.dtsx;1767832648918a9d989fdac9819873a91f919  
```  
  
 若要尋找憑證相關資訊，請使用 **CertMgr**。 可在 **CertMgr** 公用程式中檢視雜湊碼，方法是選取憑證，然後按一下 [檢視]  來檢視屬性。 **[詳細資料]** 索引標籤提供有關認證的詳細資訊。 **Thumbprint** 屬性是做為雜湊值使用，其空格已移除。  
  
> [!NOTE]  
>  此範例使用的雜湊不是真正的雜湊。  
  
 如需詳細資訊，請參閱＜ [Signing and Checking Code with Authenticode](https://go.microsoft.com/fwlink/?LinkId=78100)＞的＜CertMgr＞一節。  
  
### <a name="encrypt-examples"></a>加密範例  
 下列範例會利用完整的封裝加密和密碼，將檔案基礎的 PackageToEncrypt.dtsx 加密成檔案基礎的 EncryptedPackage.dts。 用於加密的密碼是 *EncPswd*。  
  
```dos
dtutil /FILE PackageToEncrypt.dtsx /ENCRYPT file;EncryptedPackage.dtsx;3;EncPswd  
```  
  
## <a name="see-also"></a>另請參閱  
[執行 Integration Services (SSIS) 套件](../integration-services/packages/run-integration-services-ssis-packages.md)  
  
  
