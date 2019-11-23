---
title: 在 Server Core 上安裝 SQL Server 2014 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 1dd294cc-5b69-4d0c-9005-3e307b75678b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e3e244b2c4892d725e8e3ddf684b55a224138a50
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/06/2019
ms.locfileid: "73637676"
---
# <a name="install-sql-server-2014-on-server-core"></a>在 Server Core 上安裝 SQL Server 2014
  您可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SP1 或 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 的 Server Core 安裝上安裝 [!INCLUDE[win8srv](../../includes/win8srv-md.md)]。 本主題提供在 Server Core 上安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的安裝程式特定詳細資料。  
  
 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 或 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 作業系統的 Server Core 安裝選項提供執行特定伺服器角色的基本環境， 可協助降低這些伺服器角色的維護和管理需求，以及減少其攻擊面。 如需在 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]上執行之 Server Core 的詳細資訊，請參閱[適用于 Windows server 2008 R2 的 Server core](https://go.microsoft.com/fwlink/?LinkId=202439) （ https://go.microsoft.com/fwlink/?LinkId=202439)。 如需在 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 上實作之 Server Core 的詳細資訊，請參閱 [Server Core for Windows Server 2012](https://msdn.microsoft.com/library/hh846323\(VS.85\).aspx) (https://msdn.microsoft.com/library/hh846323(VS.85).aspx)。  
  
## <a name="prerequisites"></a>Prerequisites  
  
|需求|安裝方式|  
|-----------------|--------------------|  
|[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 2.0 SP2|包含在 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 和 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 的 Server Core 安裝中。 如果未啟用，安裝程式預設會予以啟用。<br /><br /> 2\.0、3.0 和 3.5 無法在同一部電腦上並行執行。 當您安裝 .NET Framework 3.5 SP1 時，會自動取得 2.0 和 3.0 層。|  
|[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 3.5 SP1 Full Profile|包含在 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 的 Server Core 安裝中。 如果未啟用，安裝程式預設會予以啟用。<br /><br /> 在 Windows 伺服器作業系統的電腦上，您必須先下載及安裝 .NET Framework 3.5 SP1，才能執行安裝程式以安裝相依於 .NET 3.5 SP1 的元件。<br /><br /> 如需有關如何在 [!INCLUDE[win8srv](../../includes/win8srv-md.md)]中取得和啟用 .NET Framework 3.5 的建議和指導的詳細資訊，請參閱[Microsoft .NET Framework 3.5 部署考慮](https://msdn.microsoft.com/library/windows/hardware/hh975396)（ https://msdn.microsoft.com/library/windows/hardware/hh975396)。|  
|[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4 Server Core Profile|若是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 以外的所有 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 版本，安裝程式會將 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4 Server Core Profile 安裝為必要元件。<br /><br /> 如 [!INCLUDE[ssExpressEd11](../../includes/ssexpressed11-md.md)]，請從[適用于 Server Core 的 Microsoft .NET Framework 4 （獨立安裝程式）](https://www.microsoft.com/download/details.aspx?id=17718)下載 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4 Server Core 設定檔（ https://www.microsoft.com/download/details.aspx?id=17718)並加以安裝，然後再繼續進行安裝。|  
|Windows Installer 4.5|隨附於 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 和 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 的 Server Core 安裝。|  
|Windows PowerShell 2.0|隨附於 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 和 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 的 Server Core 安裝。|  
  
##  <a name="BK_SupportedFeatures"></a> Supported Features  
 您可以使用下表來尋找 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SP1 和 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 的 Server Core 安裝上 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 中支援的功能。  
  
|功能|支援|  
|-------------|---------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 服務|是|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複寫|是|  
|全文檢索搜尋|是|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|是|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|否|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Tools (SSDT)|否|  
|用戶端工具連接性|是|  
|Integration Services 伺服器<sup>[1]</sup>|是|  
|用戶端工具回溯相容性|否|  
|用戶端工具 SDK|否|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書|否|  
|管理工具 - 基本|僅限遠端<sup>[2]</sup>|  
|管理工具 - 完整|僅限遠端<sup>[2]</sup>|  
|Distributed Replay Controller|否|  
|Distributed Replay Client|僅限遠端<sup>[2]</sup>|  
|SQL 用戶端連接性 SDK|是|  
|Microsoft Sync Framework|是<sup>[3]</sup>|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|否|  
|[!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]|否|  
  
 <sup>[1]</sup>如需新 Integration Services 伺服器及其在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中之功能的詳細資訊，[請&#40;參閱&#41; Integration Services SSIS 伺服器](../../integration-services/catalog/integration-services-ssis-server-and-catalog.md)。  
  
 <sup>[2]</sup>不支援在 Server Core 上安裝這些功能。 這些元件可以安裝在與 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 或 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core 不同的伺服器上，並連接至安裝在 Server Core 上的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Services。  
  
 <sup>[3]</sup>Microsoft Sync Framework 未包含在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝套件中。 您可以從這個[Microsoft 下載中心](https://go.microsoft.com/fwlink/?LinkId=221788)（ https://go.microsoft.com/fwlink/?LinkId=221788) 頁面下載適當的 Sync Framework 版本，並將它安裝在執行 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 或 [!INCLUDE[win8srv](../../includes/win8srv-md.md)]之 Server Core 安裝的電腦上。  
  
## <a name="supported-scenario-matrix"></a>支援的案例矩陣  
 下表顯示在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SP1 和 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 的 Server Core 安裝上安裝 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 的支援案例矩陣。  
  
|||  
|-|-|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本|所有 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 64 位版本<sup>[1]</sup>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 語言|所有語言|  
|作業系統語言/地區設定上的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 語言 (組合)|JPN (日文) Windows 上的 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> GER (德文) Windows 上的 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> CHS (簡體中文) Windows 上的 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> ARA (阿拉伯文 (SA)) Windows 上的 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> THA (泰文) Windows 上的 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> TRK (土耳其文) Windows 上的 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> pt-PT (葡萄牙文 - 葡萄牙) Windows 上的 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> ENG (英文) Windows 上的 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Windows 版本|[!INCLUDE[win8srv](../../includes/win8srv-md.md)] 64 位元 x64 Datacenter<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 64 位元 x64 Standard<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64 位元 x64 Data Center Server Core<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64 位元 x64 Enterprise Server Core<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64 位元 x64 Standard Server Core<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64 位元 x64 Web Server Core|  
  
 <sup>[1]</sup>Server Core 不支援安裝32位版本的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本。  
  
## <a name="upgrading"></a>升級  
 在 Server Core 安裝中，可支援從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 升級至 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]。  
  
## <a name="installation"></a>安裝  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 不支援在 Server Core 作業系統上使用 [安裝精靈] 進行安裝。 在 Server Core 上安裝時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式支援使用 /Q 參數的完整無訊息模式或使用 /QS 參數的簡單無訊息模式。 如需詳細資訊，請參閱[從命令提示字元安裝 SQL Server 2014](install-sql-server-from-the-command-prompt.md)。  
  
> [!IMPORTANT]  
>  在執行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Server Core SP1 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Server Core 的電腦上，無法將 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 與舊版 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 並行安裝。  
  
 除非軟體的使用方式受到個別的合約 (例如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 大量授權合約或與 ISV 或 OEM 簽訂的協力廠商合約) 所管制，否則不論安裝方法為何，您都必須確認以個人身分或代表實體接受軟體授權條款。  
  
 這些授權條款會顯示在安裝程式使用者介面中，供您檢閱和接受。 自動安裝 (使用 /Q 或 /QS 參數) 必須包括 /IACCEPTSQLSERVERLICENSETERMS 參數。 您可以另外在 [Microsoft 軟體授權合約](https://go.microsoft.com/fwlink/?LinkId=148209)檢閱授權條款。  
  
> [!NOTE]  
>  根據您收到本軟體的方式 (例如，透過 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 大量授權)，軟體的使用方式可能會受到其他條款與條件的限制。  
  
 若要安裝特定功能，請使用 /FEATURES 參數，然後指定父功能或功能值。 如需有關功能參數及其用法的詳細資訊，請參閱下列章節。  
  
### <a name="feature-parameters"></a>功能參數  
  
|功能參數|描述|  
|-----------------------|-----------------|  
|SQLENGINE|只安裝 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。|  
|REPLICATION|安裝 [!INCLUDE[ssDE](../../includes/ssde-md.md)]時一併安裝複寫元件。|  
|FULLTEXT|安裝 [!INCLUDE[ssDE](../../includes/ssde-md.md)]時一併安裝全文檢索元件。|  
|AS|安裝所有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 元件。|  
|IS|安裝所有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 元件。|  
|CONN|安裝連接元件。|  
  
 請參閱下列功能參數用法的範例：  
  
|參數和值|描述|  
|--------------------------|-----------------|  
|/FEATURES=SQLEngine|只安裝 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。|  
|/FEATURES=SQLEngine,FullText|安裝 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 和全文檢索。|  
|/FEATURES=SQLEngine,Conn|安裝 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 和連接元件。|  
|/FEATURES=SQLEngine,AS,IS,Conn|安裝 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 及連接元件。|  
  
### <a name="installation-options"></a>安裝選項  
 在 Server Core 作業系統上安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 時，安裝程式支援下列安裝選項：  
  
1.  **從命令列安裝**  
  
     若要使用命令提示字元安裝選項安裝特定功能，請使用 /FEATURES 參數，然後指定父功能或功能值。 下面是有關從命令列使用參數的範例：  
  
    ```cmd
    setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,Replication /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /TCPENABLED=1 /IACCEPTSQLSERVERLICENSETERMS  
    ```  
  
2.  **使用組態檔安裝**  
  
     安裝程式僅支援透過命令提示字元使用組態檔。 組態檔是包含參數 (名稱/值組) 和描述性註解基本結構的文字檔。 在命令提示字元指定的組態檔副檔名應該是 .INI。 請參閱下列 ConfigurationFile.INI 的範例：  
  
    -   安裝 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
         下列範例示範如何安裝包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)] 的新獨立執行個體：  
  
        ```  
        ; ssNoVersion Configuration File  
        [OPTIONS]  
  
        ; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE. This is a required parameter.   
  
        ACTION="Install"  
  
        ; Specifies features to install, uninstall, or upgrade. The lists of features include SQLEngine, FullText, Replication, AS, IS, and Conn.   
  
        FEATURES=SQLENGINE  
  
        ; Specify a default or named instance. MSSQLSERVER is the default instance for non-Express editions and SQLExpress for Express editions. This parameter is required when installing the ssNoVersion Database Engine, and Analysis Services (AS).  
  
        INSTANCENAME="MSSQLSERVER"  
  
        ; Specify the Instance ID for the ssNoVersion features you have specified. ssNoVersion directory structure, registry structure, and service names will incorporate the instance ID of the ssNoVersion instance.   
  
        INSTANCEID="MSSQLSERVER"  
  
        ; Account for ssNoVersion service: Domain\User or system account.   
  
        SQLSVCACCOUNT="NT Service\MSSQLSERVER"  
  
        ; Windows account(s) to provision as ssNoVersion system administrators.   
  
        SQLSYSADMINACCOUNTS="<DomainName\UserName>"  
  
        ; Accept the License agreement to continue with Installation  
  
        IAcceptSQLServerLicenseTerms="True"
        ```  
  
    -   安裝連接元件  
  
         下列範例示範如何安裝連接元件：  
  
        ```  
        ; ssNoVersion Configuration File  
        [OPTIONS]  
  
        ; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE. This is a required parameter.   
  
        ACTION="Install"  
  
        ; Specifies features to install, uninstall, or upgrade. The lists of features include SQLEngine, FullText, Replication, AS, IS, and Conn.   
  
        FEATURES=Conn  
  
        ; Specifies acceptance of License Terms  
  
        IAcceptSQLServerLicenseTerms="True
        ```  
  
    -   安裝所有支援的功能  
  
         下列範例示範如何在 Server Core 上安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 支援的所有功能：  
  
        ```  
        ; ssNoVersion Configuration File  
        [OPTIONS]  
        ; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE. This is a required parameter.   
  
        ACTION="Install"  
  
        ; Specifies features to install, uninstall, or upgrade. The lists of features include SQLEngine, FullText, Replication, AS, IS, and Conn.   
  
        FEATURES=SQLENGINE,FullText,Replication,AS,IS,Conn  
  
        ; Specify a default or named instance. MSSQLSERVER is the default instance for non-Express editions and SQLExpress for Express editions. This parameter is required when installing the ssNoVersion Database Engine (SQL), or Analysis Services (AS).  
  
        INSTANCENAME="MSSQLSERVER"  
  
        ; Specify the Instance ID for the ssNoVersion features you have specified. ssNoVersion directory structure, registry structure, and service names will incorporate the instance ID of the ssNoVersion instance.   
  
        INSTANCEID="MSSQLSERVER"  
  
        ; Account for ssNoVersion service: Domain\User or system account.   
  
        SQLSVCACCOUNT="NT Service\MSSQLSERVER"  
  
        ; Windows account(s) to provision as ssNoVersion system administrators.   
  
        SQLSYSADMINACCOUNTS="<DomainName\UserName>"  
  
        ; The name of the account that the Analysis Services service runs under.   
  
        ASSVCACCOUNT= "NT Service\MSSQLServerOLAPService"  
  
        ; Specifies the list of administrator accounts that need to be provisioned.   
  
        ASSYSADMINACCOUNTS="<DomainName\UserName>"  
  
        ; Specifies the server mode of the Analysis Services instance. Valid values are MULTIDIMENSIONAL, POWERPIVOT or TABULAR. ASSERVERMODE is case-sensitive. All values must be expressed in upper case.   
  
        ASSERVERMODE="MULTIDIMENSIONAL"  
  
        ; Optional value, which specifies the state of the TCP protocol for the ssNoVersion service. Supported values are: 0 to disable the TCP protocol, and 1 to enable the TCP protocol.  
  
        TCPENABLED=1  
  
        ;Specifies acceptance of License Terms  
  
        IAcceptSQLServerLicenseTerms="True"  
        ```  
  
     下列範例顯示如何使用組態檔啟動安裝程式。  
  
    -   組態檔  
  
         以下是有關如何使用組態檔的部分範例：  
  
        -   若要在命令提示字元中指定組態檔：  
  
        ```cmd
        setup.exe /QS /ConfigurationFile=MyConfigurationFile.INI  
        ```  
  
        -   若要在命令提示字元而非組態檔中指定密碼：  
  
        ```cmd
        setup.exe /QS /SQLSVCPASSWORD="************" /ASSVCPASSWORD="************"  /ConfigurationFile=MyConfigurationFile.INI  
        ```  
  
    -   DefaultSetup.ini  
  
         如果您在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來源媒體根層級的 \x86 和 \x64 資料夾中具有 DefaultSetup.ini 檔案，請開啟 DefaultSetup.ini 檔案，然後將 *Features* 參數加入檔案。  
  
         如果 DefaultSetup.ini 檔案不存在，請建立檔案並將其複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來源媒體根層級的 \x86 和 \x64 資料夾中。  
  
## <a name="configuring-remote-access-of-includessnoversionincludesssnoversion-mdmd-running-on-server-core"></a>設定在 Server Core 上執行之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的遠端存取  
 執行下面描述的動作，以設定在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SP1 或 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 的 Server Core 安裝上執行之 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 執行個體的遠端存取。  
  
### <a name="enable-remote-connections-on-the-instance-of-includessnoversionincludesssnoversion-mdmd"></a>在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體上啟用遠端連接  
 若要啟用遠端連接，請在本機使用 SQLCMD.exe，然後針對 Server Core 執行個體執行下列陳述式：  
  
-   `EXEC sys.sp_configure N'remote access', N'1'`  
  
     `GO`  
  
-   `RECONFIGURE WITH OVERRIDE`  
  
     `GO`  
  
### <a name="enable-and-start-the-includessnoversionincludesssnoversion-mdmd-browser-service"></a>啟用及啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務  
 根據預設，Browser 服務是停用的。  如果在 Server Core 上執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體已停用此服務，請從命令提示字元執行下列命令，以啟用服務：  
  
 `sc config SQLBROWSER start= auto`  
  
 啟用後，請從命令提示字元執行下列命令，以啟動服務：  
  
 `net start SQLBROWSER`  
  
### <a name="create-exceptions-in-windows-firewall"></a>在 Windows 防火牆中建立例外狀況  
 若要在 Windows 防火牆中建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存取的例外狀況，請遵循[設定 Windows 防火牆以允許 SQL Server 存取](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)中指定的步驟。  
  
### <a name="enable-tcpip-on-the-instance-of-includessnoversionincludesssnoversion-mdmd"></a>在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體上啟用 TCP/IP  
 您可以針對 Server Core 上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，透過 Windows PowerShell 啟用 TCP/IP 通訊協定。 請遵循下列步驟：  
  
1.  在執行 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 或 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core 的電腦上，啟動 [工作管理員]。  
  
2.  在 [應用程式] 索引標籤上，按一下 [新工作]。  
  
3.  在 [建立新工作] 對話方塊的 [開啟] 欄位中輸入 **sqlps.exe**，然後按一下 [確定]。 隨即開啟 [ **[!INCLUDE[msCoName](../../includes/msconame-md.md)] Powershell][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** 視窗。  
  
4.  在 [Microsoft  **Powershell][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** 視窗中，執行下列指令碼以啟用 TCP/IP 通訊協定：  
  
```powershell
$smo = 'Microsoft.SqlServer.Management.Smo.'  
$wmi = New-Object ($smo + 'Wmi.ManagedComputer')  
# Enable the TCP protocol on the default instance.  If the instance is named, replace MSSQLSERVER with the instance name in the following line.  
$uri = "ManagedComputer[@Name='" + (get-item env:\computername).Value + "']/ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
$Tcp = $wmi.GetSmoObject($uri)  
$Tcp.IsEnabled = $true  
$Tcp.Alter()  
$Tcp  
```  
  
## <a name="uninstallation"></a>解除安裝  
 在登入執行 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 或 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core 的電腦之後，即可透過系統管理員命令提示字元使用有限的桌面環境。 您可以使用此命令提示字元啟動 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 執行個體的解除安裝。 若要解除安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的執行個體，請在使用 /Q 參數的完整無訊息模式或使用 /QS 參數的簡單無訊息模式中，從命令提示字元啟動解除安裝。 /QS 參數透過 UI 顯示進度，但是不接受任何輸入。 /Q 會在不含任何使用者介面的無訊息模式中執行。  
  
 解除安裝現有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體：  
  
```cmd
setup.exe /Q /Action=Uninstall /FEATURES=SQLEngine,AS,IS /INSTANCENAME=MSSQLSERVER  
```  
  
 若要移除具名執行個體，請在上述範例中指定執行個體的名稱，而非 "MSSQLSERVER"。  
  
> [!WARNING]
>  如果您不小心關閉命令提示字元，您可以遵循下列步驟啟動新的命令提示字元：  
> 
>  1.  按 Ctrl+Shift+Esc 鍵顯示 [工作管理員]。  
> 2.  在 [應用程式] 索引標籤上，按一下 [新工作]。  
> 3.  在 [建立新工作] 對話方塊的 [開啟] 欄位中，輸入 **cmd**，然後[!INCLUDE[clickOK](../../includes/clickok-md.md)]。  
  
## <a name="see-also"></a>另請參閱  
 [使用設定檔安裝 SQL Server 2014](install-sql-server-using-a-configuration-file.md)   
 [從命令提示字元安裝 SQL Server 2014](install-sql-server-from-the-command-prompt.md)   
 [SQL Server 2014 版本所支援的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [Server Core 安裝選項快速入門指南](https://go.microsoft.com/fwlink/?LinkId=221422)   
 [設定 Server Core 安裝︰概觀](https://go.microsoft.com/fwlink/?LinkId=221423)   
 [Windows PowerShell 中由工作焦點列出的容錯移轉叢集 Cmdlet](https://go.microsoft.com/fwlink/?LinkId=221419)   
 [針對容錯移轉叢集將 Cluster.exe 命令對應到 Windows PowerShell Cmdlet](https://go.microsoft.com/fwlink/?LinkId=221421)  
