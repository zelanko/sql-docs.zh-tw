---
title: 正在執行 Upgrade Advisor （命令提示字元） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor [SQL Server], running
- command prompt [Upgrade Advisor]
- UpgradeAdvisorWizardCmd utility
- XML formats [Upgrade Advisor]
ms.assetid: 7c83049b-9227-4723-9b7f-66288bc6bd1d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 997d637d109c04dbecb3105538f51fa6ece0518f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66092435"
---
# <a name="running-upgrade-advisor-command-prompt"></a>執行 Upgrade Advisor (命令提示字元)
  使用**UpgradeAdvisorWizardCmd**公用程式，從命令提示字元執行 Upgrade Advisor。 您可以選擇以 XML 格式或含有逗號分隔值的檔案來接收結果。  
  
## <a name="syntax"></a>語法  
  
```  
  
      UpgradeAdvisorWizardCmd [ -? ]  |   
    [ -ConfigFilefilename | <server_info> ]  
    [ -SqlUserlogin_id-SqlPasswordpassword ]  
    [ -CSV ]  
  
where <server_info> is any combination of the following:  
        -Serverserver_name-Instanceinstance_name-ASInstanceAS_instance_name-RSInstanceRS_instance_name  
```  
  
## <a name="arguments"></a>引數  
 **-?**  
 顯示命令語法。  
  
 **-Read-configfile** _filename_  
 這是 XML 檔案的路徑名稱和檔案名，其中包含當您執行**UpgradeAdvisorWizardCmd**公用程式時所要使用的設定。  
  
 *<server_info>*  
 指定要分析的電腦和執行個體。 如果您不要使用組態檔，請使用這些選項。  
  
 *<server_info>* 可以是下列四個引數的任何組合：  
  
 **-伺服器** _server_name_  
 指定要分析之電腦的名稱。 這可以是本機電腦 (預設值) 或遠端電腦。  
  
 **-實例** _instance_name_  
 指定要分析之執行個體的名稱。 沒有預設值。 如果您沒有指定這個參數，就不會掃描 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。 代表 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預設執行個體的值為 MSSQLSERVER。 若為具名執行個體，請使用執行個體名稱。  
  
 **-ASInstance**  _AS_instance_name_  
 指定要分析之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的名稱。 沒有預設值。 如果您沒有指定這個值，就不會掃描 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 代表 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 預設執行個體的值為 MSSQLServerOLAPService。 若為具名執行個體，請使用執行個體名稱。  
  
 **-RSInstance**  _RS_instance_name_  
 指定要分析之 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體的名稱。 沒有預設值。 如果您沒有指定這個值，就不會掃描 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 代表 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 預設執行個體的值為 ReportServer。 若為具名執行個體，請使用執行個體名稱。  
  
 **-SqlUser** _login_id_  
 如果您要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，這個值就是 Upgrade Advisor 將用來連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 如果您沒有指定登入，就會使用 Windows 驗證來連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
 **-SqlPassword** _密碼_  
 如果您使用 **-SqlUser**引數，請使用這個引數來指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入的密碼。  
  
 **-CSV**  
 指定除了標準 XML 結果以外，還要將結果當做逗號分隔值提供至 .csv 檔案。 結果會寫入 [我的文件\\ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ] 升級 upgrade advisor\110\reports 資料夾。  
  
## <a name="return-values"></a>傳回值  
 下表顯示**UpgradeAdvisorWizardCmd**所傳回的值。  
  
|值|描述|  
|-----------|-----------------|  
|0|分析成功，未找到升級問題。|  
|正整數|分析成功，找到升級問題。|  
|負整數|分析失敗。|  
  
## <a name="remarks"></a>備註  
 除了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證使用者名稱和密碼以外，您可以在 XML 組態檔中提供執行分析所需的所有資訊。 這個 XML 組態檔記載於範本中。 如果您沒有使用組態檔，可以透過指定電腦名稱和執行個體名稱，使用預設設定來分析 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中所有已安裝的元件。 如需預設組態檔設定的描述，請參閱本主題後面的「元素描述」表。  
  
## <a name="configuration-file-template"></a>組態檔範本  
 您可以使用下列 XML 當做範本，以便建立自己的組態檔。 您可以針對組織的需求來修改此範本。  
  
```xml  
<Configuration>  
    <Server> </Server>  
    <Instance></Instance>  
    <Components>  
        <SQLServer>  
            <Databases>  
                <Database></Database>  
            </Databases>  
            <TraceFiles>  
                <TraceFile></TraceFile>  
            </TraceFiles>  
            <BatchFiles>  
                <BatchFile></BatchFile>  
            </BatchFiles>  
            <BatchSeparator></BatchSeparator>  
        </SQLServer>  
        <AnalysisServices>  
            <ASInstance></ASInstance>  
            <Databases>  
                <Database></Database>  
            </Databases>  
        </AnalysisServices>  
        <ReportingServices>  
            <RSInstance></RSInstance>  
        </ReportingServices>  
        <IntegrationServices>  
            <PackagePath></PackagePath>  
        </IntegrationServices>  
    </Components>  
</Configuration>  
```  
  
## <a name="element-descriptions"></a>元素描述  
  
|Tag|定義|出現次數|  
|---------|----------------|----------------|  
|`Configuration`|Upgrade Advisor 組態檔的父元素。|(必要) 每個組態檔出現一次。|  
|`Server`|要分析之伺服器的名稱。|(選擇性) 每個組態檔出現一次。 預設值為本機電腦。|  
|`Instance`|要分析之 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體的名稱。|(選擇性) 每個組態檔出現一次。 預設值為預設執行個體。<br /><br /> 如果伺服器上出現 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元素或 `IntegrationServices` 元素，則每個組態檔必須出現一次。|  
|`Components`|包含指定要分析之元件的元素。|(必要) 每個組態檔出現一次。|  
|`SQLServer`|包含 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體的分析設定。|(選擇性) 每個組態檔出現一次。 如果沒有指定，就不會分析 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 資料庫。|  
|`Databases` 元素的 `SQLServer`|包含要分析之資料庫的清單。|每個`SQLServer`元素選用一次。 如果這個元素不存在，就會分析執行個體中的所有資料庫。|  
|`Database` 元素的 `SQLServer`|指定要分析之資料庫的名稱。|(必要) 如果 `Databases` 元素存在，就出現一或多次。 如果 `Database` 元素包含 "*" 值，就會分析執行個體中的所有資料庫。 沒有預設值。|  
|`TraceFiles`|包含要分析之追蹤檔案的清單。|每個`SQLServer`元素選用一次。|  
|`TraceFile`|指定要分析之追蹤檔案的路徑和名稱。|(必要) 如果 `TraceFiles` 元素存在，就出現一或多次。 沒有預設值。|  
|`BatchFiles`|包含要分析之批次檔案的清單。|每個`SQLServer`元素選用一次。|  
|`BatchFile`|指定要分析的批次檔案。 可以有多個。|(必要) 如果 `BatchFiles` 元素存在，就出現一或多次。 沒有預設值。|  
|`BatchSeparator`|指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 批次檔案中所使用的批次分隔符號。|每個`SQLServer`元素選用一次。 預設值為 GO。|  
|`AnalysisServices`|包含 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的分析設定。|(選擇性) 每個組態檔出現一次。 如果沒有指定，就不會分析 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫。|  
|`ASInstance`|指定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的名稱。|(必要) 每個 `AnalysisServices` 元素出現一次。 沒有預設值。|  
|`Databases` 元素的 `Analysis Services`|包含要分析之資料庫的清單。|每個`AnalysisServices`元素選用一次。 如果這個元素不存在，就會分析執行個體中的所有資料庫。|  
|`Database` 元素的 `AnalysisServices`|指定要分析之資料庫的名稱。|(必要) 如果 `Databases` 元素存在，就出現一或多次。 如果 `Database` 元素包含 "*" 值，就會分析執行個體中的所有資料庫。 沒有預設值。|  
|`ReportingServices`|指定要針對 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行分析。|(選擇性) 每個組態檔出現一次。 如果沒有指定，就不會分析 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。|  
|`RSInstance`|指定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體的名稱。|(必要) 每個 `ReportingServices` 元素出現一次。 沒有預設值。|  
|`IntegrationServices`|包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的分析設定。|(選擇性) 每個組態檔出現一次。 如果沒有指定，就不會分析 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。|  
|`PackagePath`|指定一組 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的路徑。|每個`IntegrationServices`元素選用一次。 如果這個元素不存在，就會針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體進行分析，而且不會分析儲存於外部的封裝。 沒有預設值。|  
  
## <a name="examples"></a>範例  
  
### <a name="a-run-upgrade-advisor-using-a-configuration-file"></a>A. 使用組態檔來執行 Upgrade Advisor  
 下列範例將示範如何使用指定分析項目的組態檔，從命令提示字元執行 Upgrade Advisor。 這則範例會使用 Windows 驗證來連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
```  
UpgradeAdvisorWizardCmd -ConfigFile "C:\My Documents\UpgradeConfig1.xml"  
```  
  
### <a name="b-run-upgrade-advisor-using-default-configuration-settings"></a>B. 使用預設組態設定來執行 Upgrade Advisor  
 下列範例將示範如何使用預設組態設定和 Windows 驗證，從命令提示字元執行 Upgrade Advisor。  
  
```  
UpgradeAdvisorWizardCmd -Server MyServer -Instance MyInst   
```  
  
### <a name="c-run-upgrade-advisor-using-ssnoversion-authentication"></a>C. 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證來執行 Upgrade Advisor  
 下列範例將示範如何使用組態檔，從命令提示字元執行 Upgrade Advisor。 這則範例會指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者名稱和密碼，以便連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
```  
UpgradeAdvisorWizardCmd -ConfigFile "C:\My Documents\UpgradeConfig1.xml"   
    -SqlUser "MyUserName" -SqlPassword "QweRTy-55"  
```  
  
## <a name="see-also"></a>另請參閱  
 [解決升級問題](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [使用 Upgrade Advisor](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [正在執行 Upgrade Advisor &#40;使用者介面&#41;](../../../2014/sql-server/install/running-upgrade-advisor-user-interface.md)  
  
  
