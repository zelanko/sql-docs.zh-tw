---
title: SQL Server 的預設和具名執行個體的檔案位置 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 463c570e-9f75-4653-b3b8-4d61753b0013
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 0b20fee2459dfb9273abe4e43b79ff76fdfe2dfc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035372"
---
# <a name="file-locations-for-default-and-named-instances-of-sql-server"></a>SQL Server 的預設和具名執行個體的檔案位置
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的安裝是由一個或多個不同的執行個體所組成。 不論是預設或具名，執行個體都有自己的一組程式和資料檔案，以及在電腦上所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之間共用的一組共同檔案。  
  
 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體包括 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，則每一個元件都有一組完整的資料檔案和可執行檔，以及所有元件共用的共同檔案。  
  
 為了隔離每一個元件的安裝位置，會針對給定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體內的每一個元件產生唯一的執行個體識別碼。  
  
> [!IMPORTANT]  
>  程式檔和資料檔案不能安裝在抽取式磁碟機以及使用壓縮的檔案系統上、不能安裝在系統檔案所在的目錄中，也不能安裝在容錯移轉叢集執行個體上的共用磁碟機。  
>   
>  系統資料庫 (Master、Model、MSDB 和 TempDB) 與 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 使用者資料庫可以當做儲存選項與伺服器訊息區塊 (SMB) 檔案伺服器一起安裝。 這同時適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 獨立安裝和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集安裝 (FCI)。 如需詳細資訊，請參閱 [Install SQL Server with SMB Fileshare as a Storage Option](../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md)。  
>   
>  請勿刪除下列任何一個目錄或是其內容：Binn、Data、Ftdata、HTML 或 1033。 必要時，您可以刪除其他目錄。不過，如果您沒有解除安裝後再重新安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的話，可能會無法擷取任何遺失的功能或資料。 請勿刪除或修改 HTML 目錄中的任何 .htm 檔。 這些檔案是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工具得以正常運作所不可或缺的要素。  
  
## <a name="shared-files-for-all-instances-of-includessnoversionincludesssnoversion-mdmd"></a>所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 單一電腦上所有執行個體使用的通用檔案會安裝在 [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)] 資料夾中，其中 \<*drive*> 是元件安裝位置的磁碟機代號。 預設值通常是磁碟機 C。  
  
## <a name="file-locations-and-registry-mapping"></a>檔案位置和登錄對應  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間，系統會為每一個伺服器元件產生一個執行個體識別碼。 這個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中的伺服器元件是 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。  
  
 預設執行個體識別碼是使用以下格式建構的：  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]的 MSSQL，後面接著主要版本號碼、底線、次要版本 (如果適用的話) 和句點，再接著執行個體名稱。  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的 MSAS，後面接著主要版本號碼、底線、次要版本 (如果適用的話) 和句點，再接著執行個體名稱。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的 MSRS，後面接著主要版本號碼、底線、次要版本 (如果適用的話) 和句點，再接著執行個體名稱。  
  
 此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中的預設執行個體識別碼範例如下：  
  
-   MSSQL12.MSSQLSERVER 代表 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 預設執行個體。  
  
-   MSAS12.MSSQLSERVER 代表 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] 預設執行個體。  
  
-   MSSQL12.MyInstance 代表名為 "MyInstance" 的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 具名執行個體。  
  
 包含 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 和 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 而且已安裝到預設目錄之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]具名執行個體 "MyInstance" 的目錄結構將會如下所示：  
  
-   C:\Program Files\Microsoft SQL Server\MSSQL12.MyInstance\  
  
-   C:\Program Files\Microsoft SQL Server\MSAS12.MyInstance\  
  
 您可以為執行個體識別碼指定任何值，但是請避免特殊字元和保留關鍵字。  
  
 您可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間指定非預設的執行個體識別碼。 如果使用者選擇變更預設安裝目錄，則可以改用 \<自訂路徑>\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，而不使用 \<Program Files>\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 請注意，不支援以底線 (_) 為開頭或是包含數字符號 (#) 或貨幣符號 ($) 的執行個體識別碼。  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和用戶端元件都不會感知執行個體，因此，也不會被指派執行個體識別碼。 根據預設，系統會將非執行個體感知的元件安裝到單一目錄： [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]。 變更某個共用元件的安裝路徑也會變更其他共用元件的安裝路徑。 後續安裝會將非執行個體感知的元件安裝到與原始安裝相同的目錄。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 是安裝之後支援執行個體重新命名的唯一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件。 如果 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體已重新命名，執行個體識別碼將不會變更。 當執行個體重新命名完成之後，目錄和登錄機碼將會繼續使用安裝期間所建立的執行個體識別碼。  
  
 執行個體感知元件的登錄區會建立在 HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<*Instance_ID*> 之下。 例如，  
  
-   HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\mssql12.<instancename>\mssql\。MyInstance  
  
-   HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\msas12.<instanceid>\olap\data\。MyInstance  
  
-   HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSRS12。MyInstance  
  
 登錄也會維護執行個體識別碼到執行個體名稱的對應。 執行個體識別碼到執行個體名稱的對應維護如下：  
  
-   [HKEY_LOCAL_MACHINE\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Instance Names\SQL]"InstanceName"="MSSQL12"  
  
-   [HKEY_LOCAL_MACHINE\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Instance Names\OLAP]"InstanceName"="MSAS12"  
  
-   [HKEY_LOCAL_MACHINE\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Instance Names\RS]"InstanceName"="MSRS12"  
  
## <a name="specifying-file-paths"></a>指定檔案路徑  
 在安裝期間，您可以變更下列功能的安裝路徑：  
  
 只有具有使用者可設定目的資料夾的功能，其安裝路徑才會顯示在安裝程式中：  
  
|元件|預設路徑<sup>1、 2</sup>|可設定<sup>3</sup>或固定路徑|  
|---------------|---------------------------------|--------------------------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 伺服器元件|\Program files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\mssql12.<instancename>\mssql\。\<執行個體識別碼 >\|可設定|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 資料檔|\Program files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\mssql12.<instancename>\mssql\。\<執行個體識別碼 >\|可設定|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器|\Program files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\msas12.<instanceid>\olap\data\。\<執行個體識別碼 >\|可設定|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料檔|\Program files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\msas12.<instanceid>\olap\data\。\<執行個體識別碼 >\|可設定|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器|\Program files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSRS12。\<執行個體識別碼 > services\reportserver\bin\|可設定|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表管理員|\Program files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSRS12。\<執行個體識別碼 > services\reportmanager\|固定的路徑|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|\<安裝目錄 > \120\DTS\|可設定<sup>4</sup>|  
|用戶端元件 (bcp.exe 和 sqlcmd.exe 除外)|\<安裝目錄 > \120\Tools\|可設定<sup>4</sup>|  
|用戶端元件 (bcp.exe 和 sqlcmd.exe)|\<安裝目錄>\Client SDK\ODBC\110\Tools\Binn|固定路徑|  
|複寫和伺服器端 COM 物件|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]COM\\<sup>5</sup>|固定路徑|  
|資料轉換執行階段引擎的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 元件 DLL、資料轉換管線引擎和 `dtexec` 命令提示字元公用程式|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Binn|固定路徑|  
|對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Connections|固定路徑|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 支援的每一種類型之列舉值的 DLL|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\ForEachEnumerators|固定路徑|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務，WMI 提供者|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]共用\|固定的路徑|  
|的所有執行個體之間共用的元件 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]共用\|固定的路徑|  
  
 <sup>1</sup>請確定 \Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\ 資料夾受到有限權限。  
  
 <sup>2</sup>這些位置的預設磁碟機是*systemdrive*，通常磁碟機 c。  
  
 <sup>3</sup>子功能的安裝路徑由父功能的安裝路徑。  
  
 <sup>4</sup>之間共用單一安裝路徑[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]和用戶端元件。 變更一個元件的安裝路徑也會變更其他元件的安裝路徑。 後續安裝會將元件安裝到與原始安裝相同的位置。  
  
 <sup>5</sup>的所有執行個體使用此目錄[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的電腦上。 如果您將更新項目套用至電腦的任何執行個體，則此資料夾之檔案若有任何變更，電腦上所有執行個體都會受到影響。 將功能加入至現有的安裝時，您不能變更先前安裝之功能的位置，也不能指定新功能的位置。 您必須將其他功能安裝到安裝程式所建立的目錄中，或解除安裝後再重新安裝本產品。  
  
> [!NOTE]  
>  如果是叢集組態，您必須選取該叢集的每一個節點上可用的本機磁碟機。  
  
 當您在安裝期間指定伺服器元件或資料檔案的安裝路徑時，除了程式和資料檔案的指定位置之外，安裝程式還會使用執行個體識別碼。 安裝程式不會使用工具和其他共用檔案的執行個體識別碼。 安裝程式也不會使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 程式和資料檔案的任何執行個體識別碼，但是它會使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 儲存機制的執行個體識別碼。  
  
 如果您設定了 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 功能的安裝路徑， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式會使用該路徑做為該安裝作業之所有執行個體特定資料夾的根目錄，包括 SQL 資料檔案在內。 在此情況下，如果您將根目錄設定為"C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\mssql12.<instancename>\mssql\。\<執行個體名稱 > \MSSQL\\"、 執行個體特定目錄會加入該路徑的結尾。  
  
 選擇在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝精靈 (安裝程式 UI 模式) 中使用 USESYSDB 升級功能的客戶，很容易讓自己進入這樣的情況：產品會安裝到遞迴的資料夾結構。 例如， \< *SQLProgramFiles*> \MSSQL12\MSSQL\MSSQL10_50\MSSQL\Data\\。 若要改用 USESYSDB 功能，請設定 SQL 資料檔案功能 (而非 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 功能) 的安裝路徑。  
  
> [!NOTE]  
>  您應該可以在 Data 子目錄中找到資料檔案。 例如，指定 C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\mssql12.<instancename>\mssql\。\<執行個體名稱 > \ 若要在 C:\Program Files 之下找不到資料檔案時，系統資料庫的資料目錄根路徑指定升級期間\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\mssql12.<instancename>\mssql\。\<執行個體名稱 > \MSSQL\Data。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 組態 - 資料目錄](../../../2014/sql-server/install/database-engine-configuration-data-directories.md)   
 [Analysis Services 組態 - 資料目錄](../../../2014/sql-server/install/analysis-services-configuration-data-directories.md)  
  
  