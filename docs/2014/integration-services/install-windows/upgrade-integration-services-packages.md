---
title: 升級 Integration Services 套件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, migrating
- migrating packages [Integration Services]
ms.assetid: 68dbdf81-032c-4a73-99f6-41420e053980
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a1ff35cfc7d5e8611c06981b2e3a9fe9dd6e82fd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62768994"
---
# <a name="upgrade-integration-services-packages"></a>升級 Integration Services 封裝
  當您升級的執行個體[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]或[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]目前版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，現有[!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]封裝並不會自動升級成目前版本的封裝格式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]會使用。 您必須選取升級方法並手動升級您的封裝。  
  
 當您升級 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 套件時，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會將任何指令碼工作和指令碼元件中的指令碼移轉到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA)。 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中，指令碼工作或指令碼元件中的指令碼會使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] for Applications (VSA)。 如需您可能必須在移轉之前對指令碼進行的變更以及指令碼轉換失敗的詳細資訊，請參閱[將指令碼移轉到 VSTA](../../sql-server/install/migrate-scripts-to-vsta.md)。  
  
 如需將專案轉換為專案部署模型時升級封裝的相關資訊，請參閱[將專案部署至 Integration Services 伺服器](../deploy-projects-to-integration-services-server.md)。  
  
## <a name="sql-server-2000-data-transformation-services-packages"></a>SQL Server 2000 Data Transformation Services 封裝  
 在目前的版本中，已停用針對移轉或執行 Data Transformation Services (DTS) 封裝的支援[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。 下列 DTS 功能已停用：  
  
-   DTS 執行階段  
  
-   DTS API  
  
-   可將 DTS 封裝移轉到下一版 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   DTS 封裝維護的支援 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   執行 DTS 2000 封裝工作  
  
-   DTS 封包的 Upgrade Advisor 掃描。  
  
 下列選項可用於移轉 DTS 封裝。  
  
-   將封裝移轉到 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 或 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]，然後再將封裝升級到 [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]。  
  
     如需將 DTS 套件移轉到 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 和 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 的相關資訊，請參閱[移轉 Data Transformation Services 封裝](https://go.microsoft.com/fwlink/?LinkId=251870) (2005) 和[移轉 Data Transformation Services 封裝](https://go.microsoft.com/fwlink/?LinkId=251871) (2008)。  
  
-   使用 [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)] 重新建立 DTS 封裝。  
  
     如需 [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)] 中新功能的相關資訊，請參閱 [新功能 &#40;Integration Services&#41;](../what-s-new-in-integration-services-in-sql-server-2016.md)。 如需 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 套件之結構的概觀，請參閱 [Integration Services &#40;SSIS&#41; 套件](../integration-services-ssis-packages.md)。  
  
## <a name="selecting-an-upgrade-method"></a>選取升級方法  
 您可以使用各種方法來升級 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 套件。 對於其中某些方法而言，升級只是暫時性。 對於其他方法而言，升級則是永久性。 下表將描述每種方法以及升級是暫時性或永久性。  
  
> [!NOTE]  
>  當您使用隨目前之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本安裝的 **dtexec** 公用程式 (dtexec.exe) 執行 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 套件時，暫時套件升級將會拉長執行的時間。 所增加的封裝執行時間長短，取決於封裝的大小。 如要避免執行時間增加，建議您在執行前先升級封裝。  
  
|升級方法|升級的類型|  
|--------------------|---------------------|  
|使用隨目前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本安裝的 **dtexec** 公用程式 (dtexec.exe) 執行 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 套件。<br /><br /> 如需詳細資訊，請參閱 [dtexec Utility](../packages/dtexec-utility.md)。|封裝升級是暫時性的。 針對 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，指令碼移轉是暫時性的。<br /><br /> 這些變更無法儲存。|  
|在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中，開啟 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 封裝檔案。|如果您儲存了封裝，封裝升級就是永久性。不過，如果您沒有儲存封裝，封裝升級就是暫時性。<br /><br /> 針對 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 封裝，如果您儲存了封裝，指令碼移轉就是永久性。不過，如果您沒有儲存封裝，指令碼移轉就是暫時性。|  
|在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 的現有專案中加入 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 封裝。|封裝升級是永久性的。 針對 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 封裝，指令碼移轉是永久性的。|  
|開啟 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 中的 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 或 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 專案檔案，然後使用 [[!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝升級精靈] 升級專案中的多個封裝。<br /><br /> 如需詳細資訊，請參閱[使用 SSIS 封裝升級精靈來升級 Integration Services 封裝](upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)和 [SSIS 封裝升級精靈 F1 說明](../ssis-package-upgrade-wizard-f1-help.md)。|封裝升級是永久性的。 針對 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 封裝，指令碼移轉是永久性的。|  
|使用隨目前 <xref:Microsoft.SqlServer.Dts.Runtime.Application.Upgrade%2A> 方法來升級一或多個 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。|封裝升級是永久性的。 針對 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 封裝，指令碼移轉是永久性的。|  
  
## <a name="custom-applications-and-custom-components"></a>自訂應用程式和自訂元件  
 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 自訂元件無法搭配目前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]版本使用。  
  
 您可以使用目前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 版本工具執行及管理內含 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssIS](../../includes/ssis-md.md)] 自訂元件的封裝。 我們在下列檔案中加入四個繫結重新導向規則，協助將執行階段元件從 10.0.0.0 版 ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]) 重新導向至 11.0.0.0 版 ([!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])。  
  
-   DTExec.exe.config  
  
-   dtshost.exe.config  
  
-   DTSWizard.exe.config  
  
-   DTUtil.exe.config  
  
-   DTExecUI.exe.config  
  
 若要使用[!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]為了設計封裝，包括[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]並[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]自訂元件，您需要修改 devenv.exe.config 檔案則位於*\<磁碟機 >*: files\Microsoft Visual Studio 10.0\Common7\IDE。  
  
 如果要使用這些封裝搭配 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]版本執行階段所建置的應用程式，必須在可執行檔的 *.exe.config 檔案的組態區段中包含重新導向規則。 規則會將執行階段組件重新導向至 11.0.0.0 版 ([!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])。 如需組件版本重新導向的詳細資訊，請參閱 [\<runtime> 的 \<assemblyBinding> 元素](https://msdn.microsoft.com/library/twy1dw1e.aspx)。  
  
### <a name="locating-the-assemblies"></a>尋找組件  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 組件已經升級至 .NET 4.0。 .NET 4 有個別的全域組件快取，位於 \<磁碟機>:\Windows\Microsoft.NET\assembly。 您可以在此路徑底下 (通常在 GAC_MSIL 資料夾中) 找到所有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 組件。  
  
 如同舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，核心 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 擴充性 .dll 檔案也位於 \<磁碟機>:\Program Files\Microsoft SQL Server\100\SDK\Assemblies。  
  
## <a name="understanding-sql-server-package-upgrade-results"></a>了解 SQL Server 封裝升級結果  
 升級封裝期間，[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 及 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 封裝中的大多數元件及功能皆會順利地轉換成目前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的對應項目。 不過，其中有許多元件和功能不會升級，或者具有您應該注意的升級結果。 下表將識別這些元件和功能。  
  
> [!NOTE]  
>  若要識別哪些封裝具有下表所列的問題，請執行 Upgrade Advisor。 如需詳細資訊，請參閱＜ [Use Upgrade Advisor to Prepare for Upgrades](../../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)＞。  
  
|元件或功能|升級結果|  
|--------------------------|---------------------|  
|連接字串|對於 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 及 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 封裝，某些提供者的名稱已有所變更，需要在連接字串中使用不同的值。 若要更新連接字串，請使用下列其中一個程序：<br /><br /> -使用 [[!INCLUDE[ssIS](../../includes/ssis-md.md)] 套件升級精靈] 來升級套件，然後選取 [更新連接字串以使用新的提供者名稱] 選項。<br /><br /> 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] [選項] 對話方塊的 [一般] 頁面上，選取 [更新連接字串以使用新的提供者名稱] 選項。 如需這個選項的詳細資訊，請參閱[一般頁面](../general-page-of-integration-services-designers-options.md)。<br /><br /> -在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，開啟套件並手動變更 ConnectionString 屬性的文字。<br /><br /> 注意:您無法使用先前的程序更新連接字串，當連接字串儲存在組態檔或資料來源檔案，或當運算式設定`ConnectionString`屬性。 在這些情況下，若要更新連接字串，您必須手動更新檔案或運算式。<br /><br /> 如需資料來源的詳細資訊，請參閱[資料來源](../connection-manager/data-sources.md)。|  
|查閱轉換|對於 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 封裝，升級程序會自動將查閱轉換升級為目前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 版本。 但目前版本中的此元件另有一些功能可以供您使用。<br /><br /> 如需相關資訊，請參閱 [Lookup Transformation](../data-flow/transformations/lookup-transformation.md)。|  
|指令碼工作和指令碼元件|針對 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 封裝，升級程序會自動將指令碼工作和指令碼元件中的指令碼，從 VSA 移轉到 VSTA。<br /><br /> 如需您可能必須在移轉之前對指令碼進行的變更以及指令碼轉換失敗的詳細資訊，請參閱[將指令碼移轉到 VSTA](../../sql-server/install/migrate-scripts-to-vsta.md)。|  
  
### <a name="scripts-that-depend-on-adodbdll"></a>以 ADODB.dll 為基礎的指令碼  
 明確參考 ADODB.dll 的指令碼工作和指令碼元件指令碼可能無法升級，或是在未安裝 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的電腦上執行。 為了升級這些指令碼工作或指令碼元件指令碼，建議您移除 ADODB.dll 的相依性。  建議以 Ado.Net 來替代 Managed 程式碼 (例如 VB 和 C# 指令碼)。  
  
## <a name="external-resources"></a>外部資源  
  
-   msdn.microsoft.com 上的技術文章：[5 Tips for a Smooth SSIS Upgrade to SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=235321) (將 SSIS 順利升級至 SQL Server 2012 的 5 個秘訣)。  
  
-   blogs.msdn.com 上的部落格文章： [在 Denali 中製作現有的自訂 SSIS 延伸模組和應用程式工作](https://go.microsoft.com/fwlink/?LinkId=238157)。  
  
-   channel9.msdn.com 上的網路廣播：[Upgrading SSIS Packages to SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=258674) (將 SSIS 套件升級至 SQL Server 2012)。  
  
  
