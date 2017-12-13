---
title: "Restore-asdatabase 指令程式 |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 8ab7a2d0-679c-40e6-b9b9-042184b2dfc9
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5388ca7a351b0e5a0f9d3c820598cb9c42c9d8e9
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="restore-asdatabase-cmdlet"></a>Restore-ASDatabase 指令程式
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]將多維度或表格式資料庫備份 (.abf) 檔案還原到 Analysis Services 執行個體。  

>[!NOTE] 
>這份文件可能包含過時的資訊和範例。 使用 Get-help cmdlet 取得最新。
  
## <a name="syntax"></a>語法  
 `Restore-ASDatabase [-RestoreFile] <string> [-Name] <string> [-AllowOverwrite <SwitchParameter>] Locations <Microsoft.AnalysisServices.RestoreLocation[]>] [-Security <Microsoft.AnalysisServices.RestoreSecurity>] [-Password <System.SecureString>] [-StorageLocation <System.string>] [-Server <string>] [-Credential <PSCredential>] [<CommonParameters>]`  
  
## <a name="description"></a>說明  
 讓 Analysis Services 系統管理員將多維度或表格式資料庫從備份 (.abf) 檔案還原到本機或遠端伺服器執行個體。 如果您要還原的檔案已加密，可以使用 -FilePassword 來提供解密檔案所用的密碼。  
  
 此指令程式支援 –Credential 參數，如果您設定 Analysis Services 執行個體用於 HTTP 存取，就可以使用它。 –Credential 參數會採用提供 Windows 使用者識別的 PSCredential 物件。 然後在連接到 Analysis Services 時，IIS 會模擬此使用者。 此識別必須具有 Analysis Services 執行個體的系統管理員權限，才能還原檔案。  
  
## <a name="parameters"></a>參數  
  
### <a name="-restorefile-string"></a>-RestoreFile\<字串 >  
 指定要還原之檔案的路徑和名稱。 如果您只有指定檔案名稱，而沒有指定路徑，則系統會採用預設備份位置。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|0|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-name-string"></a>-名稱\<字串 >  
 指定要還原的 Analysis Services 資料庫。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|1|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-allowoverwrite-switchparameter"></a>-AllowOverwrite \<SwitchParameter >  
 覆寫使用相同名稱和位置的資料庫。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-locations-microsoftanalysisservicesrestorelocation"></a>位置\<Microsoft.AnalysisServices.RestoreLocation [] >  
 指定要還原之資料分割的遠端位置。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-security-microsoftanalysisservicesrestoresecurity"></a>安全性\<Microsoft.AnalysisServices.RestoreSecurity >  
 表示用於還原作業的安全性設定。 有效的值包括 CopyAll、SkipMembership 和 IgnoreSecurity。 CopyAll 會還原角色和成員資格。 SkipMembership 只會重新建立角色。 IgnoreSecurity 會還原資料庫而不還原角色。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-password-securestring"></a>密碼\<SecureString >  
 指定要用來還原加密備份檔案的密碼。 您必須指定最初用來加密檔案的密碼。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-storagelocation-string"></a>-StorageLocation\<字串 >  
 指定資料庫儲存位置。 這是檔案系統上之資料庫檔案的位置。 如果您不要使用預設位置 (目標執行個體的備份資料夾)，請設定此參數。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-server-string"></a>伺服器\<字串 >  
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
  
### <a name="commonparameters"></a>\<一般參數 >  
 這個指令程式支援一般參數：-Verbose、-Debug、-ErrorAction、-ErrorVariable、-OutBuffer 和 -OutVariable。 如需詳細資訊，請參閱 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)。  
  
## <a name="inputs-and-outputs"></a>輸入和輸出  
 輸入類型是可透過管道傳送至指令程式的物件類型。 傳回類型是指令程式所傳回的物件類型。  
  
|||  
|-|-|  
|輸入|System.string<br /><br /> 您可以透過管道將字串值傳送至指令程式。|  
|輸出|無。|  
  
## <a name="example-1"></a>範例 1  
  
```  
PS SQLSERVER:\SQLAS\localhost\default> restore-asdatabase awtest.abf testawrestoredb –security:CopyAll  
```  
  
 這個命令會將本機備份資料夾中的 Analysis Services 備份檔案 (awtest.abf) 還原至本機 Analysis Services 預設執行個體。 資料庫名稱不需要存在。在本例中，資料庫名稱是在還原作業中指定。 加入 -Security:CopyAll 會將備份資料庫中的角色和角色成員資格擴展至新的還原資料庫。  
  
## <a name="example-2"></a>範例 2  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default > $pwd = read-host –AsSecureString –Prompt “Password”   
PS SQLSERVER:\SQLAS\Localhost\default > $pwd -is [System.IDisposable]   
PS SQLSERVER:\SQLAS\localhost\default> restore-asdatabase –restorefile testdb.abf –name AWTEST2 –password:$pwd  
PS SQLSERVER:\SQLAS\Localhost\default >$pwd.Dispose()  
PS SQLSERVER:\SQLAS\Localhost\default >Remove-Variable –Name pwd  
```  
  
 第 1 和第 2 行用於提示輸入加密檔案所用的密碼。  
  
 第 3 行會從 Analysis Services 預設執行個體的本機備份資料夾中還原加密的 Analysis Services 備份檔案 (testdb.abf)。  
  
 第 4 和第 5 行會移除密碼。  
  
## <a name="example-3-remote-scenario"></a>範例 3 (遠端案例)  
 此範例示範如何將本機備份檔案從檔案共用還原到 Analysis Services 的遠端執行個體。 在此範例中，備份檔案會還原為 **ssas-aw-srv01** 電腦的預設 Analysis Services 執行個體上的 **internetsales**資料庫。  
  
 備份檔案位於具有公用讀取權的網路共用。 遠端 Analysis Services 執行個體必須具有檔案的讀取權限。 檔案位置必須是網路共用 (沒有磁碟機)。  
  
 請注意，此範例不依賴 SQLAS 提供者。 您可以執行此 Cmdlet 作為獨立的命令。  
  
```  
PS SQLSERVER:\> restore-asdatabase -restorefile "\\FileServer01\DBFiles\InternetSalesTabular.abf" -name "internetsales  
" -server "SSAS-AW-SRV01"  
```  
  
## <a name="example-4"></a>範例 4  
  
```  
PS SQLSERVER:\SQLAS\localhost\default> restore-asdatabase –restorefile “\\myremoteserver\backups\testdb.abf” –name Contoso_Retail –server myremoteserver –storagelocation “\\myremoteserver\restoreDBFiles”  
```  
  
 這個命令會在遠端 Analysis Services 預設執行個體上，還原遠端備份資料夾中的加密 Analysis Services 備份檔案 (testdb.abf)。 -StorageLocation 參數是用來將資料庫檔案放在非預設位置 (在本例中，名為 restoreDBfiles 的檔案共用)。  
  
