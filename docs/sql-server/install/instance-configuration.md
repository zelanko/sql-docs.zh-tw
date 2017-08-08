---
title: "安裝精靈說明 | Microsoft Docs"
ms.custom: 
ms.date: 2017-04-21
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- instance configuration, Setup
helpviewer_keywords:
- Instance Name page [SQL Server Installation Wizard]
- SQL Server Installation Wizard, Instance Name page
ms.assetid: 5bf822fc-6dec-4806-a153-e200af28e9a5
caps.latest.revision: 62
ms.author: mikeray
manager: jhubbard
robots: noindex,nofollow
ms.translationtype: HT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 4b16feb70ed6de54240e3335a42ce6df8fa57b81
ms.contentlocale: zh-tw
ms.lasthandoff: 07/31/2017

---
# <a name="installation-wizard-help"></a>安裝精靈說明

本主題描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝精靈中的部分組態頁面。 

## <a name="instance-configuration"></a>執行個體組態
請使用 **安裝精靈的** [執行個體組態] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 頁面，指定要建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的預設執行個體還是具名執行個體。 如果尚未安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，則除非您指定具名執行個體，否則將會建立預設執行個體。  
  
每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體都包含一組不同的服務，而這些服務對於定序和其他選項具有特定設定。 目錄結構、登錄結構和服務名稱都反映出在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間建立的執行個體名稱和特定的執行個體識別碼。  
  
 執行個體是預設執行個體或具名執行個體。 預設執行個體名稱是 MSSQLSERVER。 它不需要用戶端指定執行個體名稱來進行連接。 具名執行個體由使用者在安裝期間決定。 您可以將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝為具名執行個體，而不需要先安裝預設執行個體。 一次只有一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝 (不論版本為何) 可以是預設執行個體。  
  
> [!NOTE]  
> 透過 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep，當您完成備妥的執行個體時，就可以在 [執行個體組態] 頁面上指定執行個體名稱。 如果電腦上沒有任何現有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預設執行個體，您就可以選擇將所完成的備妥執行個體設定為預設執行個體。  
  
### <a name="multiple-instances"></a>多個執行個體  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援單一伺服器或處理器上的多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，但是只有一個執行個體可以是預設執行個體； 其他所有的執行個體都必須是具名執行個體。 電腦可同時執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的多個執行個體，每一個執行個體的執行與其他執行個體無關。  
  
 如需詳細資訊，請參閱 [Maximum Capacity Specifications for SQL Server](../maximum-capacity-specifications-for-sql-server.md)。  
  
### <a name="options"></a>選項  
 僅限容錯移轉叢集執行個體 - 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集網路名稱。 這個名稱會在網路上識別容錯移轉叢集執行個體。  
  
 預設或具名執行個體 - 在決定要安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的預設執行個體還是具名執行個體時，請考量以下資訊：  
  
-   如果您計劃在資料庫伺服器上安裝單一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，它應該是預設執行個體。  
  
-   當您打算在相同電腦上擁有多個執行個體時，請使用具名執行個體。 一個伺服器只能主控一個預設執行個體。  
  
-   安裝 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 的任何應用程式都應該將它安裝為具名執行個體。 這種作法可以減少將多個應用程式安裝在相同電腦時所造成的衝突。  
  
 **預設執行個體**  
 選取這個選項可安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的預設執行個體。 電腦只能主控一個預設執行個體；所有其他執行個體都必須加以命名。 不過，如果您已安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的預設執行個體，您可將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的預設執行個體加入相同電腦中。  
  
 **具名執行個體**  
 選取這個選項可建立新的具名執行個體。 當您為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體命名時，請注意以下事項：  
  
-   執行個體名稱不區分大小寫。  
  
-   執行個體名稱不能以底線 (_) 開始或結束。  
  
-   執行個體名稱不得包含 "Default" 一詞或其他保留關鍵字。 如果在執行個體名稱中使用了保留關鍵字，會發生安裝程式錯誤。 如需詳細資訊，請參閱[保留關鍵字 &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)。  
  
-   如果您為執行個體名稱指定 MSSQLServer，將會建立預設執行個體。  
  
-   安裝 [!INCLUDE[ssGeminiLong](../../includes/ssgeminilong-md.md)] 時，一律會安裝成 '[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]' 的具名執行個體。 您無法針對這個功能角色指定不同的執行個體名稱。  
  
-   執行個體名稱限制為 16 個字元。  
  
-   執行個體名稱中的第一個字元必須是字母。 可接受的字母是由 Unicode Standard 2.0 所定義的字母。 這些包括拉丁字元 a-z、A-Z 及其他語言的字母字元。  
  
-   後續字元可以是 Unicode 標準 2.0 定義的字母、基本拉丁文或其他國家 (地區) 指令碼中的十進位數字、錢幣符號($) 或底線 (_)。  
  
-   執行個體名稱中不允許內嵌空格或其他特殊字元。 此外，也不允許反斜線 (\\)、逗號 (,)、冒號 (:)、分號 (;)、單引號 (')、＆ 符號 (&)、連字號 (-) 和 At 符號 (@)。  
  
     只有目前 Windows 字碼頁中有效的字元，才可以用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱。 如果使用不受支援的 Unicode 字元，將會發生安裝程式錯誤。  
  
 **偵測到的執行個體和功能**  
 在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式的電腦上檢視已安裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體和元件的清單。  
  
 **執行個體識別碼** ：依預設，此執行個體名稱會當作執行個體識別碼使用。 這是用來識別 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的安裝目錄和登錄機碼。 這是預設執行個體和具名執行個體的狀況。 如果是預設執行個體，執行個體名稱和執行個體識別碼將會是 MSSQLSERVER。 若要使用非預設的執行個體識別碼，請在 **[執行個體識別碼]** 欄位中指定它。  
  
> [!IMPORTANT]  
>  透過 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep，顯示在這個頁面上的執行個體識別碼就是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep 程序之準備映像步驟期間所指定的執行個體識別碼。 您無法在完成映像步驟期間指定不同的執行個體識別碼。  
  
> [!NOTE]  
>  不支援以底線 (_) 為開頭或是包含數字符號 (#) 或貨幣符號 ($) 的執行個體識別碼。  
  
 如需目錄、檔案位置和執行個體識別碼命名的詳細資訊，請參閱 [SQL Server 的預設和具名執行個體的檔案位置](file-locations-for-default-and-named-instances-of-sql-server.md)。  
  
 給定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的所有元件都會當做一個單位來管理。 所有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Pack 和升級項目都會套用至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的每一個元件。  
  
 所有共用相同執行個體名稱之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的所有元件，都必須符合下列準則：  
  
-   **相同的版本**  
  
-   **相同的版本**  
  
-   **相同語言設定**  
  
-   **相同叢集狀態**  
  
    > [!NOTE]  
    >  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 無法識別叢集。  
  
-   **相同作業系統**  
  
## <a name="analysis-services-configuration---account-provisioning"></a>Analysis Services 組態 - 帳戶提供
  此用此頁面可以設定伺服器模式，以及將管理權限授與需要無限制存取 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的使用者或服務。 安裝程式不會自動將本機 Windows 群組 BUILTIN\Administrators 加入您所安裝之執行個體的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器管理員角色。 如果您想要將本機 Administrators 群組加入至伺服器管理員角色，就必須明確指定該群組。  
  
 如果您要安裝 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]，請務必將管理權限授與負責在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 伺服陣列中進行 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 部署的 SharePoint 伺服陣列管理員或服務管理員。  
  
### <a name="options"></a>選項。  
 **伺服器模式** - 伺服器模式指定可以部署到伺服器的 Analysis Services 資料庫類型。 伺服器模式是在安裝期間決定，之後不能修改。 每個模式是互斥的，也就是說，您需要兩個 Analysis Services 執行個體，各設定為不同的模式，以便同時支援傳統 OLAP 和表格式模型方案。  
  
 **指定管理員** - 您必須為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體至少指定一個伺服器管理員。 您所指定的使用者或群組將成為所安裝之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的伺服器管理員角色成員。 這些都必須是與安裝該軟體的電腦處於相同網域中的 Windows 網域使用者帳戶。  
  
> [!NOTE]  
>  使用者帳戶控制 (UAC) 為 Windows 安全性功能，會要求系統管理員明確地核准系統管理動作或應用程式，之後才會允許這些項目執行。 由於 UAC 預設為開啟，系統將會提示您允許需要更高權限的特定作業。 您可以設定 UAC，以變更預設行為或針對特定程式自訂 UAC。 如需 UAC 和 UAC 組態的詳細資訊，請參閱[使用者帳戶控制逐步指南](http://go.microsoft.com/fwlink/?linkid=196350)和[使用者帳戶控制 (Wikipedia)](http://go.microsoft.com/fwlink/?linkid=196351)。  
  
### <a name="see-also"></a>另請參閱  
 [設定服務帳戶和 &#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md) [設定 Windows 服務帳戶與權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  

 ## <a name="analysis-services-configuration---data-directories"></a>Analysis Services 組態 - 資料目錄
  下表的預設目錄可在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間由使用者設定。 存取這些檔案的權限會授與本機系統管理員，以及安裝期間建立及佈建的 SQLServerMSASUser$\<執行個體> 安全性群組成員。  
  
### <a name="uielement-list"></a>UIElement 清單  
  
|描述|預設目錄|建議|  
|-----------------|-----------------------|---------------------|  
|資料根目錄|C:\Program Files\Microsoft SQL Server\MSAS*nn*.\<執行個體識別碼>\OLAP\Data\ |請確定 \Program files\Microsoft SQL Server\ 資料夾受到有限權限的保護。 在許多組態中，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 效能取決於資料目錄所在之儲存體的效能。 請將這個目錄放置於附加至系統的最高效能儲存體上。 若為容錯移轉叢集安裝，請確定資料目錄位於共用磁碟上。|  
|記錄檔目錄|C:\Program Files\Microsoft SQL Server\MSAS*nn*.\<執行個體識別碼>\OLAP\Log\ |這是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 記錄檔的目錄，而且它包括了 FlightRecorder 記錄檔。 如果您增加了飛行記錄器持續時間，請確定記錄檔目錄具有足夠的空間。|  
|暫存目錄|C:\Program Files\Microsoft SQL Server\MSAS*nn*.\<執行個體識別碼>\OLAP\Temp\ |請將暫存目錄放置於高效能的儲存體子系統上。|  
|備份目錄|C:\Program Files\Microsoft SQL Server\MSAS*nn*.\<執行個體識別碼>\OLAP\Backup\ |這是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 預設備份檔案的目錄。 對於 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 安裝來說，這也是 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務快取 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料檔案的位置。<br /><br /> 請確定已設定適當的權限來防止資料遺失，並且確定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服務的使用者群組具有足夠的權限，可寫入備份目錄。 不支援針對備份目錄使用對應的磁碟機。|  
  
### <a name="notes"></a>注意  
  
-   部署在 SharePoint 伺服陣列上的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體會將應用程式檔案、資料檔案和屬性儲存在內容資料庫與服務應用程式資料庫中。  
  
-   將功能加入至現有的安裝時，您不能變更先前安裝之功能的位置，也不能指定新功能的位置。  

-   您可能需要設定掃描軟體，例如防毒和反間諜軟體應用程式，以排除 SQL Server 資料夾和檔案類型。 如需詳細資訊，請參閱下列支援文章︰[Antivirus software on computers running SQL Server](https://support.microsoft.com/kb/309422) (執行 SQL Server 的電腦上的防毒軟體)。
  
-   如果您要指定非預設的安裝目錄，請確定安裝資料夾對於此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體是唯一的。 此對話方塊上的任何目錄都不應該與其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中的目錄共用。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體內的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件也應該安裝在不同的目錄中。  
  
-   程式檔和資料檔案無法安裝在下列位置中：  
  
    -   抽取式磁碟機  
  
    -   使用壓縮的檔案系統  
  
    -   系統檔案所在的目錄  
  
### <a name="see-also"></a>另請參閱  
 如需目錄、檔案位置和執行個體識別碼命名的詳細資訊，請參閱 [SQL Server 的預設和具名執行個體的檔案位置](file-locations-for-default-and-named-instances-of-sql-server.md)。  
  
## <a name="database-engine-configuration---data-directories"></a>Database Engine 組態 - 資料目錄
  請使用此頁面來指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]程式和資料檔案的安裝位置。 根據安裝類型，支援的儲存體可能包括本機磁碟、共用儲存體或 SMB 檔案伺服器。  
  
 若要將 SMB 檔案共用指定為目錄，您必須手動輸入支援的 UNC 路徑。 不支援瀏覽 SMB 檔案共用。 以下是 SMB 檔案共用支援的 UNC 路徑格式： \\\Servername\ShareName\\....  
  
### <a name="stand-alone-instance-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的獨立執行個體  
 下表列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 獨立執行個體支援的儲存類型，以及使用者可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間設定的預設目錄。  
  
### <a name="uielement-list"></a>UIElement 清單  
  
|描述|支援的儲存類型|預設目錄|建議|  
|-----------------|----------------------------|-----------------------|---------------------|  
|資料根目錄|本機磁碟, SMB 檔案伺服器, 共用儲存體* |C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\ |進行組態設定時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式將會設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目錄的 ACL 並中斷繼承。|  
|使用者資料庫目錄|本機磁碟, SMB 檔案伺服器, 共用儲存體*|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<執行個體識別碼>\MSSQL\Data |使用者資料目錄的最佳作法取決於工作負載和效能需求。|  
|使用者資料庫記錄檔目錄|本機磁碟, SMB 檔案伺服器, 共用儲存體*|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<執行個體識別碼>\MSSQL\Data|請確定記錄檔目錄具有足夠的空間。|  
|備份目錄|本機磁碟, SMB 檔案伺服器, 共用儲存體*|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<執行個體識別碼>\MSSQL\Backup|請設定適當的權限來防止資料遺失，並且確定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的使用者帳戶具有足夠的權限，可寫入備份目錄。 不支援針對備份目錄使用對應的磁碟機。|  
  
 *儘管支援共用磁碟，但不建議對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 獨立執行個體採用這種做法。  
  
### <a name="failover-cluster-instance-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體  
 下表列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體支援的儲存類型，以及使用者可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間設定的預設目錄。  
  
|描述|支援的儲存類型|預設目錄|建議|  
|-----------------|----------------------------|-----------------------|---------------------|  
|資料根目錄|共用儲存體、SMB 檔案伺服器|\<磁碟機：>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<br /><br /> 秘訣：如果在 [叢集磁碟選取]  頁面上選取共用磁碟，預設為第一個共用磁碟。 如果在 **[叢集磁碟選取]** 頁面上沒有進行任何選擇，此欄位預設為空白。|進行組態設定時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式將會設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目錄的 ACL 並中斷繼承。|  
|使用者資料庫目錄|共用儲存體、SMB 檔案伺服器|\<磁碟機:>Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<執行個體識別碼>\MSSQL\Data<br /><br /> 秘訣：如果在 [叢集磁碟選取]  頁面上選取共用磁碟，預設為第一個共用磁碟。 如果在 **[叢集磁碟選取]** 頁面上沒有進行任何選擇，此欄位預設為空白。|使用者資料目錄的最佳作法取決於工作負載和效能需求。|  
|使用者資料庫記錄檔目錄|共用儲存體、SMB 檔案伺服器|\<磁碟機:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<執行個體識別碼>\MSSQL\Data<br /><br /> 秘訣：如果在 [叢集磁碟選取]  頁面上選取共用磁碟，預設為第一個共用磁碟。 如果在 **[叢集磁碟選取]** 頁面上沒有進行任何選擇，此欄位預設為空白。|請確定記錄檔目錄具有足夠的空間。|  
|備份目錄|本機磁碟、共用儲存體、SMB 檔案伺服器|\<磁碟機:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<執行個體識別碼>\MSSQL\Backup<br /><br /> 秘訣：如果在 [叢集磁碟選取]  頁面上選取共用磁碟，預設為第一個共用磁碟。 如果在 **[叢集磁碟選取]** 頁面上沒有進行任何選擇，此欄位預設為空白。|請設定適當的權限來防止資料遺失，並且確定 SQL Server 服務的使用者帳戶具有足夠的權限，可寫入備份目錄。 不支援針對備份目錄使用對應的磁碟機。|  
  
### <a name="security-considerations"></a>安全性考量  
 進行組態設定時，安裝程式將會設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目錄的 ACL 並中斷繼承。  
  
 以下建議適用於 SMB 檔案伺服器：  
  
-   如果使用 SMB 檔案伺服器， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶必須是網域帳戶。  
  
-   用於安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的帳戶應該擁有當做資料目錄之 SMB 檔案共用資料夾的 FULL CONTROL NTFS 權限。  
  
-   用於安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的帳戶應該具有 SMB 檔案伺服器的 SeSecurityPrivilege 權限。 若要授與此權限，請使用檔案伺服器上的 [本機安全性原則] 主控台，將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式帳戶新增至 **[管理稽核和安全性記錄檔]** 原則中。 在 **[本機安全性原則]** 主控台中 **[本機原則]** 下的 **[使用者權限指派]** 區段可以找到此設定。  
  
### <a name="notes"></a>注意  
  
-   將功能加入現有的安裝時，您不能變更先前安裝之功能的位置，也不能指定新功能的位置。  
  
-   如果您要指定非預設的安裝目錄，請確定安裝資料夾對於此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體是唯一的。 此對話方塊上的任何目錄都不應該與其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中的目錄共用。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體內的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件也應該安裝在不同的目錄中。  
  
-   程式檔和資料檔案無法安裝在下列位置中：  
  
    -   抽取式磁碟機  
  
    -   使用壓縮的檔案系統  
  
    -   系統檔案所在的目錄  
  
    -   容錯移轉叢集執行個體上的對應網路磁碟機  
  
### <a name="see-also"></a>另請參閱  
### <a name="analysis-services-configuration---data-directories"></a>Analysis Services 組態 - 資料目錄
  下表的預設目錄可在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間由使用者設定。 存取這些檔案的權限會授與本機系統管理員，以及安裝期間建立及佈建的 SQLServerMSASUser$\<執行個體> 安全性群組成員。  
  
#### <a name="uielement-list"></a>UIElement 清單  
  
|描述|預設目錄|建議|  
|-----------------|-----------------------|---------------------|  
|資料根目錄 |C:\Program Files\Microsoft SQL Server\MSAS*nn*.\<執行個體識別碼>\OLAP\Data |請確定 \Program files\Microsoft SQL Server\ 資料夾受到有限權限的保護。 在許多組態中，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 效能取決於資料目錄所在之儲存體的效能。 請將這個目錄放置於附加至系統的最高效能儲存體上。 若為容錯移轉叢集安裝，請確定資料目錄位於共用磁碟上。|  
|記錄檔目錄|C:\Program Files\Microsoft SQL Server\MSAS*nn*.\<執行個體識別碼>\OLAP\Log |這是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 記錄檔的目錄，而且它包括了 FlightRecorder 記錄檔。 如果您增加了飛行記錄器持續時間，請確定記錄檔目錄具有足夠的空間。|  
|暫存目錄|C:\Program Files\Microsoft SQL Server\MSAS*nn*.\<執行個體識別碼>\OLAP\Temp |請將暫存目錄放置於高效能的儲存體子系統上。|  
|備份目錄|C:\Program Files\Microsoft SQL Server\MSAS*nn*.\<執行個體識別碼>\OLAP\Backup |這是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 預設備份檔案的目錄。 對於 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 安裝來說，這也是 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務快取 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料檔案的位置。<br /><br /> 請確定已設定適當的權限來防止資料遺失，並且確定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服務的使用者群組具有足夠的權限，可寫入備份目錄。 不支援針對備份目錄使用對應的磁碟機。|  
  
#### <a name="notes"></a>注意  
  
-   部署在 SharePoint 伺服陣列上的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體會將應用程式檔案、資料檔案和屬性儲存在內容資料庫與服務應用程式資料庫中。  
  
-   將功能加入至現有的安裝時，您不能變更先前安裝之功能的位置，也不能指定新功能的位置。  

-   您可能需要設定掃描軟體，例如防毒和反間諜軟體應用程式，以排除 SQL Server 資料夾和檔案類型。 如需詳細資訊，請參閱下列支援文章︰[Antivirus software on computers running SQL Server](https://support.microsoft.com/kb/309422) (執行 SQL Server 的電腦上的防毒軟體)。
  
-   如果您要指定非預設的安裝目錄，請確定安裝資料夾對於此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體是唯一的。 此對話方塊上的任何目錄都不應該與其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中的目錄共用。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體內的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件也應該安裝在不同的目錄中。  
  
-   程式檔和資料檔案無法安裝在下列位置中：  
  
    -   抽取式磁碟機  
  
    -   使用壓縮的檔案系統  
  
    -   系統檔案所在的目錄  
  
#### <a name="see-also"></a>另請參閱  
 如需目錄、檔案位置和執行個體識別碼命名的詳細資訊，請參閱 [SQL Server 的預設和具名執行個體的檔案位置](file-locations-for-default-and-named-instances-of-sql-server.md)。  
  
    
 [檔案伺服器的共用及 NTSF 權限](http://go.microsoft.com/fwlink/?LinkID=206571) 

## <a name="database-engine-configuration---filestream"></a>Database Engine 組態 - Filestream
  您可以使用這個頁面，針對這個 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝啟用 FILESTREAM。 FILESTREAM 會將 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] varbinary(max) **二進位大型物件 (BLOB) 資料作為檔案儲存在檔案系統上，以整合** 與 NTFS 檔案系統。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式可以插入、更新、查詢、搜尋和備份 FILESTREAM 資料。 Win32 檔案系統介面提供了資料的資料流方式存取。  
  
### <a name="uielement-list"></a>UIElement 清單  
 **對 Transact-SQL 存取啟用 FILESTREAM**  
 選取此選項即可針對 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存取啟用 FILESTREAM。 您必須先核取這個控制項，然後才能使用其他控制選項。  
  
 **對檔案 I/O 資料流存取啟用 FILESTREAM**  
 選取此選項即可針對 Win32 資料流存取啟用 FILESTREAM。  
  
 **Windows 共用名稱**  
 使用這個控制項即可輸入即將儲存 FILESTREAM 資料之 Windows 共用的名稱。  
  
 **允許遠端用戶端具有 FILESTREAM 資料的資料流存取權**  
 選取這個控制項即可允許遠端用戶端在此伺服器上存取這項 FILESTREAM 資料。  
  
### <a name="see-also"></a>另請參閱  
 [啟用及設定 FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  

  
## <a name="database-engine-configuration---server-configuration"></a>Database Engine 組態 - 伺服器組態
  您可以使用此頁面來設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性模式，以及加入 Windows 使用者或群組做為 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的管理員。  
  
### <a name="considerations-for-running-includesscurrentincludessscurrent-mdmd"></a>執行[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 時的考量  
 在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上， **BUILTIN\Administrators** 群組是提供成 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的登入，而且本機 Administrators 群組的成員可以使用其管理員認證登入。 使用較高的權限並非最佳做法。 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中， **BUILTIN\Administrators** 群組並未提供成登入。 因此，您應該為每個管理使用者建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，並在安裝新的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]執行個體期間，將該登入加入至系統管理員 (sysadmin) 固定伺服器角色。 您也應該針對用來執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式作業的 Windows 帳戶進行上述作業。 這些作業包括複寫代理程式作業。  
  
### <a name="options"></a>選項  
 **安全性模式** - 為您的安裝選取 Windows 驗證或混合模式驗證。  
  
 **Windows 主體提供** - 在舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，Windows Builtin\Administrator 本機群組置於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員伺服器角色中，可有效授與 Windows 管理員對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的存取權。 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，Builtin\Administrator 群組不會提供在系統管理員 (sysadmin) 伺服器角色中。 您應該改在安裝期間針對新的安裝明確提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理員。  
  
> [!IMPORTANT]  
>  您必須在安裝期間針對新的安裝明確提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理員。 要等到您完成此步驟之後，安裝程式才允許您繼續。  
  
 **指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理員** - 您必須為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體指定至少一個 Windows 主體。 若要加入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式執行所用的帳戶，請按一下 [目前使用者] 按鈕。 若要從系統管理員清單中加入或移除帳戶，請按一下 **[加入]** 或 **[移除]**，然後編輯在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體中將會有管理員權限的使用者、群組或電腦清單。  
  
 當您完成清單的編輯之後，請按一下 [確定]，然後在組態對話方塊中確認管理員的清單。 當此清單完成時，請按 **[下一步]**。  
  
 如果您選取混合模式驗證，您必須為內建 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員 (SA) 帳戶提供登入認證。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 **Windows 驗證模式**  
 當使用者透過 Windows 使用者帳戶連接時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用作業系統中的 Windows 主體 Token 來驗證帳戶名稱和密碼。 這是預設驗證模式，比混合模式更加安全。 Windows 驗證利用 Kerberos 安全性通訊協定，在增強式密碼的複雜驗證方面提供密碼原則強化，並提供對帳戶鎖定的支援，同時支援密碼逾期。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] 絕對不可設定空白或弱式 sa 密碼。  
  
 **混合模式 (Windows 驗證或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證)**  
 允許使用者利用 Windows 驗證或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證來連接。 透過 Windows 使用者帳戶連接的使用者可以使用 Windows 已驗證的信任連接。  
  
 如果您必須選擇混合模式驗證，而且需要使用 SQL 登入來配合舊版應用程式，則您必須為所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶設定增強式密碼。  
  
> [!NOTE]  
>  提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的目的，只是為了回溯相容性。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 **輸入密碼**  
 輸入並確認系統管理員 (sa) 登入。 密碼是對抗入侵者的第一道防線，因此，設定增強式密碼對於系統的安全性很重要。 不得設定空白或弱式 sa 密碼。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 密碼可包含 1 到 128 個字元，包括字母、符號和數字的任意組合。 如果您選擇混合模式驗證，則在您可以繼續到安裝精靈的下一頁之前，必須先輸入增強式 sa 密碼。  
  
 **增強式密碼方針**  
 增強式密碼不會很快被猜到，使用電腦程式也不容易破解。 增強式密碼不得使用禁止條件或詞彙，包括：  
  
-   空白或 NULL 條件  
  
-   "Password"  
  
-   "Admin"  
  
-   "Administrator"  
  
-   "sa"  
  
-   "sysadmin"  
  
 增強式密碼不得為與安裝電腦相關的下列詞彙：  
  
-   目前登入機器的使用者名稱。  
  
-   電腦名稱。  
  
 增強式密碼的長度必須為 8 個字元以上，且至少滿足下列四項準則中的三項：  
  
-   必須包含大寫字母。  
  
-   必須包含小寫字母。  
  
-   必須包含數字。  
  
-   必須包含非英數字元；例如 #、% 或 ^。  
  
 此頁面中輸入的密碼必須符合增強式密碼原則的需求。 如果您有使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的任何自動化作業，請確定此密碼符合增強式密碼原則的需求。  
  
### <a name="related-content"></a>相關內容  
 如需有關選擇 Windows 驗證和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的詳細資訊，請參閱[選擇驗證模式](../../relational-databases/security/choose-an-authentication-mode.md)。  
  
 如需選擇帳戶以執行 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的詳細資訊，請參閱[設定 Windows 服務帳戶與權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。
  
## <a name="database-engine-configuration---tempdb"></a>資料庫引擎組態 - TempDB
  請使用此頁面來指定 **tempdb** 資料和記錄檔位置、大小、成長設定，以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)] 的檔案數目。 根據安裝類型，支援的儲存體可能包括本機磁碟、共用儲存體或 SMB 檔案伺服器。  
  
 若要將 SMB 檔案共用指定為目錄，您必須手動輸入支援的 UNC 路徑。 不支援瀏覽 SMB 檔案共用。 以下是 SMB 檔案共用支援的 UNC 路徑格式： \\\Servername\ShareName\\....  
  
### <a name="data-and-log-directories-for--a-stand-alone-instance-of--includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 獨立執行個體的資料與記錄目錄  
 下表列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 獨立執行個體支援的儲存類型，以及您可以在安裝期間設定的預設目錄。  
  
|描述|支援的儲存類型|預設目錄|建議|  
|-----------------|----------------------------|-----------------------|---------------------|  
|**資料目錄**|本機磁碟、SMB 檔案伺服器、共用儲存體* |C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<執行個體識別碼>\MSSQL\Data|進行組態設定時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式將會設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目錄的 ACL 並中斷繼承。<br /><br /> **temdb** 目錄的最佳做法取決於工作負載和效能需求。 指定多個資料夾/磁碟機，以將資料檔案分散到數個磁碟區。|  
|**記錄目錄**|本機磁碟、SMB 檔案伺服器、共用儲存體*|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<執行個體識別碼>\MSSQL\Data|請確定記錄檔目錄具有足夠的空間。|  
  
 *儘管支援共用磁碟，但不建議對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 獨立執行個體採用這種做法。  
  
### <a name="data-and-log-directories-for-a-failover-cluster-instance-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體的資料與記錄目錄  
 下表列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體支援的儲存類型，以及使用者可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間設定的預設目錄。  
  
|描述|支援的儲存類型|預設目錄|建議|  
|-----------------|----------------------------|-----------------------|---------------------|  
|**tempdb** 資料目錄|本機磁碟、共用儲存體、SMB 檔案伺服器|\<磁碟機:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<執行個體識別碼>\Data<br /><br /> 秘訣：如果在 [叢集磁碟選取]  頁面上選取共用磁碟，預設為第一個共用磁碟。 如果在 **[叢集磁碟選取]** 頁面上沒有進行任何選擇，此欄位預設為空白。|進行組態設定時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式將會設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目錄的 ACL 並中斷繼承。<br /><br /> 請確定指定的一或多個目錄 (如果指定了多個檔案) 適用於所有叢集節點。 在容錯移轉期間，如果容錯移轉目標節點上的 **tempdb** 目錄無法使用，則 SQL Server 資源將無法上線。|  
|**tempdb** 記錄目錄|本機磁碟、共用儲存體、SMB 檔案伺服器|\<磁碟機:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<執行個體識別碼>\MSSQL\Data<br /><br /> 秘訣：如果在 [叢集磁碟選取]  頁面上選取共用磁碟，預設為第一個共用磁碟。 如果在 **[叢集磁碟選取]** 頁面上沒有進行任何選擇，此欄位預設為空白。|使用者資料目錄的最佳作法取決於工作負載和效能需求。<br /><br /> 請確定指定的目錄對所有叢集節點都有效。 在容錯移轉期間，如果容錯移轉目標節點上的 **tempdb** 目錄無法使用，則 SQL Server 資源將無法上線。<br /><br /> 請確定記錄檔目錄具有足夠的空間。|  
  
### <a name="uielement-list"></a>UIElement 清單  
 根據您的工作負載和需求來設定 **tempdb** 的設定。 下列設定會套用到 **tempdb** 資料檔案︰  
  
-   **檔案數目** 是適用於 **tempdb**的資料檔案總數。 預設值是低於 8 的數字，或是安裝程式偵測到的邏輯核心數目。 一般而言，如果邏輯處理器的數目小於或等於 8，請使用與邏輯處理器數目相同的資料檔案數目。 如果邏輯處理器的數目大於 8，請使用 8 個資料檔案，之後如果競爭的情況持續發生，請以 4 的倍數增加資料檔案數目 (最多為邏輯處理器數目)，直到競爭縮減到可接受的程度，或是對工作負載/程式碼進行變更。 
  
-   [初始大小 (MB)] 是每個 **tempdb** 資料檔案的初始大小 (MB)。 預設值為 8 MB ([!INCLUDE[ssexpress](../../includes/ssexpress_md.md)] 則為 4 MB)。 [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] 引入的初始檔案大小上限為 262,144 MB (256 GB)。 [!INCLUDE[sssql15](../../includes/sssql15-md.md)] 的初始檔案大小上限則為 1024 MB。 所有 **tempdb** 資料檔案的初始大小都一樣。 因為 **tempdb** 會在每次啟動 SQL Server 或容錯移轉重新建立，所以，您應該將大小指定為接近您的工作負載進行正常作業所需的大小。 若要在啟動期間進一步最佳化 **tempdb** 的建立，可啟用[資料庫檔案立即初始化](../../relational-databases/databases/database-instant-file-initialization.md)。  
  
-   [初始大小總計 (MB)] 是所有 **tempdb** 資料檔案的累計大小。  
  
-   [自動成長 (MB)] 是以 MB 為單位的空間量，其中的每個 **tempdb** 資料檔案將會在其空間用盡時自動成長。 在 [!INCLUDE[sssql15](../../includes/sssql15-md.md)] 和更新版本中，所有資料檔案將依據此設定中指定的數量同時成長。  
  
-   [自動成長總計 (MB)] 是每個自動成長事件的累計大小。  
  
-   **資料目錄** 會顯示所有保留 **tempdb** 資料檔案的目錄。 有多個目錄時，資料檔案會以循環配置資源方式放置於目錄中。 例如，假設您建立 3 個目錄並指定 8 個資料檔案，將會第一個目錄中建立號碼為 1、4、7 的資料檔案。 資料檔案 2、 5 和 8 將建立於第二個目錄中。 資料檔案 3 到 6 則會在第三個目錄中。  
  
-   若要新增目錄，可按一下 [新增...] 。  
  
-   若要移除目錄，可選取目錄，然後按一下 [移除] 。  
  
 **TempDB 記錄檔** 是記錄檔的名稱。 它會自動建立。 下列設定只會套用到 **tempdb** 記錄檔︰  
  
-   [初始大小 (MB)] 是 **tempdb** 記錄檔的初始大小。 預設值為 8 MB ([!INCLUDE[ssexpress](../../includes/ssexpress_md.md)] 則為 4 MB)。 [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] 引入的初始檔案大小上限為 262,144 MB (256 GB)。 [!INCLUDE[sssql15](../../includes/sssql15-md.md)] 的初始檔案大小上限則為 1024 MB。 因為 **tempdb** 會在每次啟動 SQL Server 或容錯移轉重新建立，所以，您應該將大小指定為接近您的工作負載進行正常作業所需的大小。 若要在啟動期間進一步最佳化 **tempdb** 的建立，可啟用[資料庫檔案立即初始化](../../relational-databases/databases/database-instant-file-initialization.md)。  
  
-   **注意** ︰Tempdb 會使用最低限度的記錄。 **Tempdb** 記錄檔無法備份。 它會在每次啟動 SQL Server，或當容錯移轉叢集執行個體時重新建立。  
  
-   [自動成長 (MB)] 是 **tempdb** 記錄的成長增量 (MB)。  64 MB 的預設值會初始化期間建立最佳數目的虛擬記錄檔。  
  
-   **注意** ︰Tempdb 記錄檔不會使用檔案立即初始化。  
  
-   **記錄目錄** 是建立 **tempdb** 記錄檔的目錄。 只會有一個 **tempdb** 記錄目錄。  
  
### <a name="security-considerations"></a>安全性考量  
 進行組態設定時，安裝程式將會設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目錄的 ACL 並中斷繼承。  

 以下建議適用於 SMB 檔案伺服器：  
  
-   如果使用 SMB 檔案伺服器， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶必須是網域帳戶。  
  
-   用於安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的帳戶應該擁有當做資料目錄之 SMB 檔案共用資料夾的 FULL CONTROL NTFS 權限。  
  
-   用於安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的帳戶應該具有 SMB 檔案伺服器的 SeSecurityPrivilege 權限。 若要授與此權限，請使用檔案伺服器上的 [本機安全性原則] 主控台，將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式帳戶新增至 **[管理稽核和安全性記錄檔]** 原則中。 在 **[本機安全性原則]** 主控台中 **[本機原則]** 下的 **[使用者權限指派]** 區段可以找到此設定。  
  
### <a name="notes"></a>注意  
  
-   如果您要指定非預設的安裝目錄，請確定安裝資料夾對於此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體是唯一的。 此對話方塊上的任何目錄都不應該與其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中的目錄共用。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體內的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件也應該安裝在不同的目錄中。  
  
### <a name="see-also"></a>另請參閱  
 [設定 Windows 服務帳戶與權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [檔案伺服器的共用及 NTSF 權限](http://go.microsoft.com/fwlink/?LinkID=206571)  

## <a name="database-engine-configuration---user-instance"></a>資料庫引擎組態 - 使用者執行個體
使用 **[使用者執行個體]** 頁面，即可為不具管理員權限的使用者產生個別的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體，並將使用者加入至管理員角色。  
  
### <a name="option"></a>選項  
 啟用使用者執行個體  
 預設值為開啟。 若要停用啟用使用者執行個體的功能，請清除該核取方塊。  
  
 使用者執行個體 (也稱為子系或用戶端執行個體) 是父執行個體 (當做服務執行的主要執行個體，例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ) 代表使用者所產生的 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]執行個體。 使用者執行個體是在該使用者的安全性內容下，以使用者處理序的形式執行。 使用者執行個體與父執行個體和電腦上執行的其他使用者執行個體隔離。 使用者執行個體功能也稱為「以一般使用者的身分執行」(RANU)。  
  
> [!NOTE]  
>  在安裝期間佈建為 **sysadmin** (系統管理員) 固定伺服器角色成員的登入，會佈建為範本資料庫中的管理員。 除非移除，否則這些登入會是使用者執行個體上 **sysadmin** (系統管理員) 固定伺服器角色的成員。  
  
 將使用者加入至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理員角色  
 預設值不是開啟。 若要將目前的安裝程式使用者加入至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理員角色，請選取該核取方塊。  
  
 身為 BUILTIN\Administrators 成員的 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] 使用者並不會在連接到 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 時，自動加入系統管理員固定伺服器角色中。 只有已明確地加入至伺服器層級之管理員角色的 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] 使用者可以管理 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]。 Built-In\Users 群組的任何成員都可以連接至 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 執行個體，但這些成員僅具有執行資料庫工作的有限權限。 因為這個原因，所以必須在 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 上執行的 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 執行個體中，明確地為從舊版 Windows 的 BUILTIN\Administrators 和 Built-In\Users 繼承 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)]權限的使用者授與管理員權限。  
  
 若要在此安裝程式結束後，對使用者角色進行任何變更，請使用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 介面區組態工具 (SQLSAC.exe)。 若要更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員角色中的使用者清單，按一下 **[新增管理員]** 連結。  
  
 請確定 [User to provision (要提供的使用者)] 欄位有列出其權限應該更新之使用者的 DomainName\UserName。 從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [可用權限] **窗格的** 執行個體清單中選取要更新的角色，然後按一下向右鍵。 若要將使用者加入至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的所有可用執行個體及可用角色的可用角色，按一下雙重向右鍵。  
  
 若要在完成選擇時實作變更，請 [!INCLUDE[clickOK](../../includes/clickok-md.md)]。 若要結束工具而不進行變更，按一下 **[取消]**。  
  
  

