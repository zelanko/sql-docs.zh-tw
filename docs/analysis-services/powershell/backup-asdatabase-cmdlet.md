---
title: Backup-asdatabase 指令程式 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: powershell
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ea4e93828aded76fd45ffe6bd279cba8397d8483
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="backup-asdatabase-cmdlet"></a>Backup-ASDatabase 指令程式
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

  將 Analysis Services 多維度或表格式資料庫備份至 Analysis Services 備份 (.abf) 檔案。  

>[!NOTE] 
>這份文件可能包含過時的資訊和範例。 使用 Get-help cmdlet 取得最新。
  
## <a name="syntax"></a>語法  
 `Backup-ASDatabase [-BackupFile] <string> [-Name] <string> [-AllowOverwrite <SwitchParameter>] [-BackupRemotePartitions <SwitchParameter>] [-ApplyCompression <SwitchParameter>] [-FilePassword <SecureString>] [-Locations <Microsoft.AnalysisServices.BackupLocation[]>] [-Server <string>] [-Credential <PSCredential>] [<CommonParameters>]`  
  
 `Backup-ASDatabase –Database <Microsoft.AnalysisServices.Database> [-AllowOverwrite <SwitchParameter>] [-BackupRemotePartitions <SwitchParameter>] [-ApplyCompression <SwitchParameter>] [-FilePassword <SecureString>] [-Locations <Microsoft.AnalysisServices.BackupLocation[]>] [-Server <string>] [-Credential <PSCredential>] [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 讓 Analysis Services 系統管理員能夠將多維度或表格式資料庫備份至備份檔案。 如果未指定位置，則會使用在安裝期間指定的預設備份位置。  
  
 備份的檔案可以加密。 使用 –FilePassword 來加密檔案。 稍後在還原檔案時，必須提供指定用來加密的相同密碼。  
  
 此指令程式支援 –Credential 參數，如果您設定 Analysis Services 執行個體用於 HTTP 存取，就可以使用它。 –Credential 參數會採用提供 Windows 使用者識別的 PSCredential 物件。 然後在連接到 Analysis Services 時，IIS 會模擬此使用者。 此識別必須具有 Analysis Services 執行個體的系統管理員權限，才能執行備份。  
  
## <a name="parameters"></a>參數  
  
### <a name="-backupfile-string"></a>-BackupFile\<字串 >  
 指定備份檔案的路徑和名稱。 如果您只有指定檔案名稱，而沒有指定路徑，則會使用預設備份位置。 此參數只能搭配 -Name 參數使用。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|0|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-name-string"></a>-Name \<string>  
 指定要備份的 Analysis Services 資料庫。 如果要以字串方式傳入資料庫名稱，您可以使用 -Database 參數或 -Name 參數指定資料庫。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|1|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-allowoverwrite-switchparameter"></a>-AllowOverwrite \<SwitchParameter >  
 覆寫同名的備份檔案。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-backupremotepartitions-switchparameter"></a>-BackupRemotePartitions \<SwitchParameter >  
 指定是否將在備份中包含遠端資料分割。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-applycompressionswitchparameter"></a>-ApplyCompression\<SwitchParameter >  
 指定是否要壓縮備份檔案。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-filepassword-securestring"></a>-FilePassword \<SecureString >  
 指定要用於備份檔案加密的密碼。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-locations-microsoftanalysisservicesbackuplocation"></a>位置\<Microsoft.AnalysisServices.BackupLocation [] >  
 指定將儲存備份檔案的位置。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-server-string"></a>-Server \<string>  
 指定指令程式將會連接並執行的 Analysis Services 執行個體。 如果沒有提供伺服器名稱，將會建立 localhost 的連接。 若為預設執行個體，請單獨指定伺服器名稱。 若為具名執行個體，請使用格式 servername\instancename。 若為 HTTP 連接，請使用格式 http[s]://server[:port]/virtualdirectory/msmdpump.dll。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值|localhost|  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-credential-pscredential"></a>-Credential \<PSCredential >  
 指定提供 Windows 使用者名稱和密碼的 PSCredential 物件。 僅當 Analysis Services 執行個體設定用於 HTTP 存取時 (使用基本驗證)，才指定此參數。 對於使用整合式安全性的原生連接，則會忽略此參數。  
  
 如果此參數存在，它提供的認證會附加到連接字串。 連接到 Analysis Services 時，IIS 就會模擬此使用者識別。 如果沒有指定認證，則會使用執行此工具之使用者的預設 Windows 帳戶。  
  
 若要使用此參數，請先使用 Get-Credential 來建立 PSCredential 物件，以便指定使用者名稱和密碼 (例如 `$Cred=Get-Credential “adventure-works\admin”`。 然後，您可以透過管道將這個物件傳送至 -Credential 參數 `(-Credential:$Cred`)。  
  
如需 HTTP 存取的詳細資訊，請參閱[設定 Internet Information Services &#40;IIS&#41; 8.0 上 Analysis Services 的 HTTP 存取](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|True (ByValue)|  
|接受萬用字元？|false|  
  
### <a name="-database-microsoftanalysisservicesdatabase"></a>-資料庫\<Microsoft.AnalysisServices.Database [] >  
 指定要備份的 Analysis Services 資料庫物件。 您可以使用 -Database 參數或 -Name 參數指定資料庫。 如果要透過管道傳入資料庫名稱，請使用 -Database。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|true|  
|接受萬用字元？|false|  
  
### <a name="commonparameters"></a>\<一般參數 >  
 這個指令程式支援一般參數：-Verbose、-Debug、-ErrorAction、-ErrorVariable、-OutBuffer 和 -OutVariable。 如需詳細資訊，請參閱 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)。  
  
## <a name="inputs-and-outputs"></a>輸入和輸出  
 輸入類型是可透過管道傳送至指令程式的物件類型。 傳回類型是指令程式所傳回的物件類型。  
  
|||  
|-|-|  
|輸入|Microsoft.AnalysisServices.Database<br /><br /> 您可以透過管道傳送多個要備份的資料庫，例如特定執行個體的所有資料庫。|  
|輸出|無。|  
  
## <a name="example-1"></a>範例 1  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default >backup-asdatabase awdb-20110930.abf “Adventure Works” -AllowOverwrite -ApplyCompression  
```  
  
 此命令將 Adventure Works 資料庫備份到位於預設備份位置的 .abf 檔案。 如果位置上有同名的現有檔案，則會覆寫它。  
  
## <a name="example-2"></a>範例 2  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default >$AWDB = get-item “databases\Adventure Works”   
PS SQLSERVER:\SQLAS\Localhost\default >Backup-asdatabase –database:$AWDB –AllowOverwrite  
```  
  
 此命令使用 -Database，而不是使用 -Backupfile 和 -Name。 當您要透過管道將資料庫名稱傳送至指令程式時，請使用 -Database。  
  
## <a name="example-3"></a>範例 3  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default\databases >dir * | backup-asdatabase  
```  
  
 此命令備份本機伺服器上的所有資料庫。  
  
## <a name="example-4"></a>範例 4  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default > $pwd = read-host –AsSecureString –Prompt “Password”   
PS SQLSERVER:\SQLAS\Localhost\default > $pwd -is [System.IDisposable]   
PS SQLSERVER:\SQLAS\Localhost\default > backup-asdatabase –backupfile test.abf –name contoso_retail –filepassword:$pwd server myremoteserver  
PS SQLSERVER:\SQLAS\Localhost\default >$pwd.Dispose()  
PS SQLSERVER:\SQLAS\Localhost\default >Remove-Variable –Name pwd  
```  
  
 第 1 和第 2 行用於提示輸入要用於加密檔案的密碼。  
  
 第 3 行將遠端 Analysis Services 伺服器上的 Contoso_Retail 範例資料庫備份至也位於此遠端伺服器上名為 test.abf 的 Analysis Services 備份檔案。 此檔案會儲存至預設執行個體的預設備份資料夾。  
  
 第 4 和第 5 行會移除密碼。  
  
  
  
