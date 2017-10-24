---
title: "New-restorelocation 指令程式 |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 5ca13d8c-1c5d-4f02-869c-72e0defce6d7
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a87852e69b55ea26cb56fe6918d1d4310c339f27
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="new-restorelocation-cmdlet"></a>New-RestoreLocation 指令程式

[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  指定用來還原資料庫的資訊。  

>[!NOTE] 
>這份文件可能包含過時的資訊和範例。 使用 Get-help cmdlet 取得最新。
  
## <a name="syntax"></a>語法  
 `New-RestoreLocation [-File <String>] [-DataSourceId <String>] [-ConnectionString <String>] [-DataSourceType <RestoreDataSourceType>] [-Folders <RestoreFolder[]>] [-AsTemplate] [-Server <String>] [-Credential <PSCredential>] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>] [-WhatIf] [-Confirm]`  
  
 `New-RestoreLocation [-Server <String>] [-Credential <PSCredential>] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>] [-WhatIf] [-Confirm]`  
  
 一般參數 (例如 -Verbose、-Debug)、錯誤和警告參數、-Whatif 和 -Confirm 都記載於 Windows PowerShell 參考中。 如需詳細資訊，請參閱 [about_CommonParameters](http://technet.microsoft.com/library/dd315352.aspx)。  
  
## <a name="description"></a>說明  
 New-RestoreLocation 指令程式包含用來還原資料庫的資訊，包括伺服器和資料庫的連接字串、資料來源屬性，以及與所還原之資料庫相關聯的檔案和資料夾。  
  
## <a name="parameters"></a>參數  
  
### <a name="-file-string"></a>-檔案\<字串 >  
 指定您要還原之備份檔案的名稱。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-datasourceid-string"></a>-DataSourceId\<字串 >  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-connectionstring-string"></a>-ConnectionString\<字串 >  
 指定遠端 Analysis Services 執行個體的連接字串。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-datasourcetype-asrestoredatasourcetype"></a>-DataSourceType \<AS.RestoreDataSourceType >  
 指定資料來源是遠端或本機 (根據資料分割的位置)。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-folders-asrestorefolder"></a>-資料夾\<AS.RestoreFolder >  
 指定本機或遠端執行個體上的資料分割資料夾。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-astemplate-switchparameter"></a>-AsTemplate \<SwitchParameter >  
 指定是否應該在記憶體中建立物件並傳回物件。  
  
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
 若為您已經設定為 HTTP 存取的執行個體，這個參數是在使用 Analysis Service 執行個體的 HTTP 連接時用來傳入使用者名稱和密碼。 如需詳細資訊，請參閱[設定 HTTP 存取 Analysis Services，Internet Information Services &#40; IIS &#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)進行 HTTP 連線。  
  
 如果指定了此參數，使用者名稱和密碼將會用來連接到指定的 Analysis Server 執行個體。 如果沒有指定認證，則會使用執行此工具之使用者的預設 Windows 帳戶。  
  
 若要使用此參數，請先使用 Get-Credential 來建立 PSCredential 物件，以便指定使用者名稱和密碼 (例如 `$Cred=Get-Credential “adventure-works\bobh”`。 然後，您可以透過管道將這個物件傳送至 -Credential 參數 `(-Credential:$Cred`)。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|True (ByValue)|  
|接受萬用字元？|false|  
  
## <a name="inputs-and-outputs"></a>輸入和輸出  
 輸入類型是可透過管道傳送至指令程式的物件類型。 傳回類型是指令程式所傳回的物件類型。  
  
|||  
|-|-|  
|輸入|無|  
|輸出|無|  
  
## <a name="examples"></a>範例  
  
  

