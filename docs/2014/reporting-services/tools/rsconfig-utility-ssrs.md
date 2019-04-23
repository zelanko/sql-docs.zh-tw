---
title: rsconfig 公用程式 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- connections [Reporting Services], configuring
- rsconfig utility
- report servers [Reporting Services], connections
- command prompt utilities [Reporting Services]
- command prompt utilities [SQL Server], rsconfig
ms.assetid: 84e45a2f-3ca6-4c16-8259-c15ff49d72ad
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9a22983a23e9bd1801de849774836a0a0acd2927
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59947244"
---
# <a name="rsconfig-utility-ssrs"></a>rsconfig 公用程式 (SSRS)
  **rsconfig.exe** 公用程式會加密連接和帳戶值，並會將它們儲存在 RSReportServer.config 檔中。 加密的值包括自動處理報表的程序所用的報表伺服器資料庫連接資訊和帳戶值。  
  
## <a name="syntax"></a>語法  
  
```  
  
      rsconfig {-?}  
{-cconnection}  
{-eunattendedaccount}  
{-mcomputername}  
{-iinstancename}  
{-sservername}  
{-ddatabasename}  
{-aauthmethod}  
{-uusername}  
{-ppassword}  
{-ttrace}  
```  
  
## <a name="arguments"></a>引數  
  
|詞彙|選擇性/必要|定義|  
|----------|------------------------|----------------|  
|**-?**|選擇性。|顯示 Rsconfig.exe 引數的語法。|  
|`-c`|如果未使用 `-e` 引數，這就是必要的。|指定用來將報表伺服器連接到報表伺服器資料庫的連接字串、認證和資料來源值。<br /><br /> 此引數沒有取得值。 不過，您也必須指定其他引數來搭配它，以便提供所有必要的連接值。<br /><br /> 您可以使用指定的引數`-c`包括`-m`， **-s**， `-i`，`-d`，`-a`，`-u`，`-p`，以及`-t`。|  
|`-e`|如果未使用 `-c` 引數，這就是必要的。|指定自動報表執行帳戶。<br /><br /> 此引數沒有取得值。 不過，命令列必須包括其他引數，以便指定組態檔中所加密的值。<br /><br /> 您可以搭配 `-e` 來指定的引數，包括 `-u` 和 `-p`。 您也可以設定 `-t`。|  
|`-m`  *computername*|如果您在設定遠端報表伺服器執行個體，這就是必要的。|指定主控報表伺服器的電腦名稱。 如果省略這個引數，預設值就是 `localhost`。|  
|**-s**  <伺服器名稱>|必要。|指定主控報表伺服器資料庫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。|  
|`-i`  *instancename*|如果您使用具名執行個體，這就是必要的。|如果您利用具名 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體來主控報表伺服器資料庫，這個值會指定具名執行個體。|  
|`-d`  *databasename*|必要。|指定報表伺服器資料庫的名稱。|  
|`-a`  *authmethod*|必要。|指定報表伺服器用來連接到報表伺服器資料庫的驗證方法。 有效值如下：`Windows` 或 `SQL` (這個引數不區分大小寫)。<br /><br /> `Windows` 指定報表伺服器使用 Windows 驗證。<br /><br /> `SQL` 指定報表伺服器使用 SQL Server 驗證。|  
|`-u`  *[domain\\]username*|對 `-e` 而言，這是必要的；對 `-c` 而言，這是選擇性的。|指定報表伺服器資料庫連接或自動帳戶的使用者帳戶。<br /><br /> 若為 **rsconfig -e**，此引數是必要的。 它必須是網域使用者帳戶。<br /><br /> 針對**rsconfig-c**並`-a SQL`，這個引數必須指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入。<br /><br /> 針對**rsconfig-c**和`-a Windows`，這個引數可以指定網域使用者、 內建帳戶或服務帳戶認證。 如果您指定網域帳戶，請以 <網域>\<使用者名稱> 的格式指定 <網域> 和 <使用者名稱>。 如果您是使用內建帳戶，這個引數就是選擇性的。 如果您要使用服務帳戶認證，請省略這個引數。|  
|`-p`  *password*|如果指定 `-u` 的話，這就是必要的。|指定要搭配 <使用者名稱> 引數使用的密碼。 如果帳戶不需要密碼，您可以將這個引數設為空白值。 網域帳戶的這個值會區分大小寫。|  
|`-t`|選擇性。|在追蹤記錄中，輸出錯誤訊息。 此引數沒有取得值。 如需詳細資訊，請參閱 [Report Server Service Trace Log](../report-server/report-server-service-trace-log.md)。|  
  
## <a name="permissions"></a>Permissions  
 您必須是主控您在設定的報表伺服器之電腦的本機管理員。  
  
## <a name="file-location"></a>檔案位置  
 Rsconfig.exe 位於 **\Program Files\Microsoft SQL Server\110\Tools\Binn**。 您可以從檔案系統上的任何資料夾執行此公用程式。  
  
## <a name="remarks"></a>備註  
 Rsconfig.exe 有兩個用途：  
  
-   修改報表伺服器用來連接報表伺服器資料庫的連接資訊。  
  
-   設定特殊帳戶，供報表伺服器在無法使用其他認證時，用來登入遠端資料庫伺服器。  
  
 您可以在**的本機或遠端執行個體上執行** rsconfig [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]公用程式。 您無法使用 **rsconfig** 公用程式解密及檢視已設定的值。  
  
 在執行這個公用程式之前，您必須先將 Windows Management Instrumentation (WMI) 安裝在您要設定的電腦中。  
  
## <a name="examples"></a>範例  
 下列範例說明 **rsconfig**的使用方式。  
  
#### <a name="specifying-a-domain-user-account"></a>指定網域使用者帳戶  
 這個範例會顯示在連接本機報表伺服器資料庫時，如何設定報表伺服器來使用網域使用者帳戶。  
  
```  
rsconfig -c -s <SQLSERVERNAME> -d reportserver -a Windows -u <MYDOMAIN\MYACCOUNT> -p <PASSWORD>  
```  
  
#### <a name="specifying-a-sql-server-database-user-account"></a>指定 SQL Server 資料庫使用者帳戶  
 這個範例會顯示如何設定報表伺服器，利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入來連接遠端報表伺服器資料庫。  
  
```  
rsconfig -c -m <REMOTECOMPUTERNAME> -s <SQLSERVERNAME> -d reportserver -a SQL -u SA -p <SAPASSWORD>  
```  
  
#### <a name="specifying-a-built-in-account"></a>指定內建帳戶  
 這個範例會顯示在連接本機報表伺服器資料庫時，如何設定報表伺服器來使用內建帳戶。 請注意，不要使用 `-u`。 支援的內建帳戶值範例包括本機系統的 NT AUTHORITY\SYSTEM 和網路服務的 NT AUTHORITY\NETWORKSERVICE (只適用於[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] )。  
  
```  
rsconfig -c -s <SQLSERVERNAME> -d reportserver -a Windows "NT AUTHORITY\SYSTEM"  
```  
  
#### <a name="specifying-a-service-account"></a>指定服務帳戶  
 這個範例會顯示在連接本機報表伺服器資料庫時，如何設定報表伺服器來使用「報表伺服器視窗」服務帳戶和 Web 服務帳戶。 請注意，不要使用 `-u`，也不要指定任何帳戶資訊。 當您從命令中刪除帳戶值， **rsconfig** 公用程式會使用執行各項服務時所用的整合式安全性和服務帳戶。  
  
```  
rsconfig -c -s <SQLSERVERNAME> -d reportserver -a Windows  
```  
  
#### <a name="specifying-the-unattended-account-on-a-local-server"></a>指定本機伺服器中的自動帳戶  
 這個範例會顯示如何設定帳戶，供不會將認證傳給外部資料來源的報表之自動執行報表的作業使用。 這個帳戶必須是 Windows 網域帳戶。 您不能指定這個使用者名稱和密碼的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 這個帳戶設在本機報表伺服器執行個體上。 錯誤訊息放在 ReportingServices\LogFiles 資料夾的追蹤記錄中。  
  
```  
rsconfig -e -u <DOMAIN\ACCOUNT> -p <PASSWORD> -t  
```  
  
#### <a name="specifying-the-unattended-account-on-a-remote-server"></a>指定遠端伺服器中的自動帳戶  
 這個範例會顯示如何設定與 Rsconfig.exe 版本相同的遠端報表伺服器執行個體的帳戶 (例如，報表伺服器和 Rsconfig.exe 都是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 R2 版)。 錯誤訊息的資訊放在遠端伺服器的追蹤記錄中。  
  
```  
rsconfig -e -m <REMOTECOMPUTERNAME> -s <SQLSERVERNAME> -u <DOMAIN\ACCOUNT> -p <PASSWORD> -t  
```  
  
## <a name="see-also"></a>另請參閱  
 [設定報表伺服器資料庫連接 &#40;SSRS 組態管理員&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [設定自動執行帳戶 &#40;SSRS 組態管理員&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)   
 [Reporting Services 報表伺服器 &#40;原生模式&#41;](../report-server/reporting-services-report-server-native-mode.md)   
 [儲存加密的報表伺服器資料 &#40;SSRS 組態管理員&#41;](../install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Reporting Services 組態檔](../report-server/reporting-services-configuration-files.md)   
 [報表伺服器命令提示字元公用程式 &#40;SSRS&#41;](report-server-command-prompt-utilities-ssrs.md)   
 [RSReportServer 設定檔](../report-server/rsreportserver-config-configuration-file.md)  
  
  
