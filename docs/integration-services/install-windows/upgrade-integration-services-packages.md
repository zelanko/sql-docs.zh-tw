---
title: "升級 Integration Services 封裝 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Integration Services, migrating
- migrating packages [Integration Services]
ms.assetid: 68dbdf81-032c-4a73-99f6-41420e053980
caps.latest.revision: 54
author: MikeRayMSFT
ms.author: mikeray
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: a2e3655bedbb24f2174a62c8792cd168e7642592
ms.openlocfilehash: b04ba24fd90ec81e735933a45fed18294d77ceab
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="upgrade-integration-services-packages"></a>升級 Integration Services 封裝
  當您將 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 執行個體升級為目前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本時，現有的 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 封裝並不會自動升級為目前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 版本所使用的封裝格式。 您必須選取升級方法並手動升級您的封裝。  
  
 您將專案轉換成專案部署模型時升級封裝的資訊，請參閱[部署 Integration Services (SSIS) 專案和封裝](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)
  
## <a name="selecting-an-upgrade-method"></a>選取升級方法  
 您可以使用各種方法來升級 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]或 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 封裝。 對於其中某些方法而言，升級只是暫時性。 對於其他方法而言，升級則是永久性。 下表將描述每種方法以及升級是暫時性或永久性。  
  
> [!NOTE]  
>  當您使用隨目前之 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]版本安裝的 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]dtexec [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]公用程式 (dtexec.exe) 執行 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 、 **、** 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]封裝時，暫時封裝升級將會拉長執行的時間。 所增加的封裝執行時間長短，取決於封裝的大小。 如要避免執行時間增加，建議您在執行前先升級封裝。  
  
|升級方法|升級的類型|  
|--------------------|---------------------|  
|使用隨目前 **版本安裝的** dtexec [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式 (dtexec.exe) 執行 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]或 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 封裝。<br /><br /> 如需詳細資訊，請參閱 [dtexec Utility](../../integration-services/packages/dtexec-utility.md)。|封裝升級是暫時性的。<br /><br /> 這些變更無法儲存。|  
|在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]中，開啟 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 或 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]封裝檔案。|如果您儲存了封裝，封裝升級就是永久性。不過，如果您沒有儲存封裝，封裝升級就是暫時性。|  
|在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]的現有專案中加入 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 或 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]封裝。|封裝升級是永久性的。|  
|開啟 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 中的 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]或更新的專案檔，然後使用 [ [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝升級精靈] 升級專案中的多個封裝。<br /><br /> 如需詳細資訊，請參閱 [使用 SSIS 封裝升級精靈來升級 Integration Services 封裝](../../integration-services/install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md) 和 [SSIS 封裝升級精靈 F1 說明](../../integration-services/ssis-package-upgrade-wizard-f1-help.md)。|封裝升級是永久性的。|  
|使用隨目前 <xref:Microsoft.SqlServer.Dts.Runtime.Application.Upgrade%2A> 方法來升級一或多個 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。|封裝升級是永久性的。|  
  
## <a name="custom-applications-and-custom-components"></a>自訂應用程式和自訂元件  
 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 自訂元件無法搭配目前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]版本使用。  
  
 您可以使用目前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 版本工具來執行及管理內含 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]或 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)][!INCLUDE[ssIS](../../includes/ssis-md.md)] 自訂元件的封裝。 我們在下列檔案中加入四個繫結重新導向規則，協助將執行階段組件從 10.0.0.0 版 ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)])、11.0.0.0 版 ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) 或 12.0.0.0 版 ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) 重新導向至 13.0.0.0 版 ([!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])。  
  
-   DTExec.exe.config  
  
-   dtshost.exe.config  
  
-   DTSWizard.exe.config  
  
-   DTUtil.exe.config  
  
-   DTExecUI.exe.config  
  
 若要使用[!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]為了設計封裝，包括[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]， [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]， [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，或[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]自訂元件，您需要修改 devenv.exe.config 檔案則位於*\<磁碟機 >*: \Program Files\Microsoft Visual Studio 10.0\Common7\IDE。  
  
 如果要使用這些封裝搭配 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本執行階段所建置的應用程式，必須在可執行檔的 *.exe.config 檔案的組態區段中包含重新導向規則。 規則會將執行階段組件重新導向至 13.0.0.0 版 ([!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])。 如需組件版本重新導向的詳細資訊，請參閱[ \<assemblyBinding > 項目\<執行階段 >](http://msdn.microsoft.com/library/twy1dw1e.aspx)。  
  
### <a name="locating-the-assemblies"></a>尋找組件  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 組件已經升級至 .NET 4.0。 沒有.NET 4 中，位於個別的全域組件快取*\<磁碟機 >*: \Windows\Microsoft.NET\assembly。 您可以在此路徑底下 (通常在 GAC_MSIL 資料夾中) 找到所有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 組件。  
  
 如同舊版[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，核心[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]擴充性.dll 檔案也位於*\<磁碟機 >*: \Program Files\Microsoft SQL Server\130\SDK\Assemblies。  
  
## <a name="understanding-sql-server-package-upgrade-results"></a>了解 SQL Server 封裝升級結果  
 升級封裝期間， [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]或 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 封裝中的大多數元件及功能皆會順利地轉換成目前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本的對應項目。 不過，其中有許多元件和功能不會升級，或者具有您應該注意的升級結果。 下表將識別這些元件和功能。  
  
> [!NOTE]  
>  若要識別哪些封裝具有下表所列的問題，請執行 Upgrade Advisor。  
  
|元件或功能|升級結果|  
|--------------------------|---------------------|  
|連接字串|對於 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]或 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 封裝，某些提供者的名稱已有所變更，需要在連接字串中使用不同的值。 若要更新連接字串，請使用下列其中一個程序：<br /><br /> 使用 [[!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝升級精靈] 來升級封裝，然後選取 [更新連接字串以使用新的提供者名稱] 選項。<br /><br /> 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] [選項] 對話方塊的 [一般] 頁面上，選取 [更新連接字串以使用新的提供者名稱] 選項。 如需有關這個選項的詳細資訊，請參閱 [一般] 頁面。<br /><br /> 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟封裝並手動變更 ConnectionString 屬性的文字。<br /><br /> 注意：當連接字串儲存在組態檔或資料來源檔案中，或者運算式設定 **ConnectionString** 屬性時，您無法使用先前的程序來更新連接字串。 在這些情況下，若要更新連接字串，您必須手動更新檔案或運算式。<br /><br /> 如需資料來源的詳細資訊，請參閱 [資料來源](../../integration-services/connection-manager/data-sources.md)。|  
  
### <a name="scripts-that-depend-on-adodbdll"></a>以 ADODB.dll 為基礎的指令碼  
 明確參考 ADODB.dll 的指令碼工作和指令碼元件指令碼可能無法升級，或是在未安裝 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的電腦上執行。 為了升級這些指令碼工作或指令碼元件指令碼，建議您移除 ADODB.dll 的相依性。  建議以 Ado.Net 來替代 Managed 程式碼 (例如 VB 和 C# 指令碼)。  
  
  

