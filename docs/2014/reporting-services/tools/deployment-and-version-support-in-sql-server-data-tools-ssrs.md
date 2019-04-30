---
title: 部署和版本支援在 SQL Server Data Tools (SSRS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 36f5686d-7e40-4f31-be81-bd197ca33a02
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bfac4568659d03f62294bf6159604ce6230639d2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63218390"
---
# <a name="deployment-and-version-support-in-sql-server-data-tools-ssrs"></a>SQL Server 資料工具中的部署和版本支援 (SSRS)
  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 支援以下案例：  
  
-   開啟報表定義 (*.rdl) 與報表伺服器專案 (\*.rptproj)。  
  
-   建立報表定義。  
  
-   在報表設計師中預覽報表。  
  
-   將報表部署到報表伺服器。  
  
##  <a name="bkmk_ConfigurationandDeploymentProperties"></a> 組態和部署屬性  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 支援專案組態。 專案組態是由一組屬性所組成，這些屬性可指定建立專案的位置和行為，做為預覽或部署報表的步驟。 若要了解有關專案組態的詳細資訊，請參閱 Visual Studio 文件集。  
  
 使用專案組態可控制升級至與目標伺服器相容之結構描述版本的報表定義。 由專案組態所控制的屬性包括目標報表伺服器、建立期間用來暫時儲存用於預覽和部署之報表定義的資料夾，以及錯誤等級。  
  
 系統會先建立報表，然後才將報表轉譯為報表設計師中的預覽或部署到報表伺服器。  
  
 您可以在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] **[專案屬性]** 對話方塊中設定組態屬性。  
  
 建立與部署屬性包括：  
  
-   OutputPath 是會識別資料夾路徑的建置屬性，用於儲存組建驗證、部署與預覽報表時所使用的報表定義。  
  
-   ErrorLevel 是建置屬性，會識別回報為錯誤之建置問題的嚴重性。 嚴重性層級小於或等於 ErrorLevel 值的問題會回報為錯誤；否則，會將這些問題回報為警告。 如需詳細資訊，請參閱[使用報表設計師設計報表 &#40;SSRS&#41;](design-reporting-services-paginated-reports-with-report-designer-ssrs.md) 中的＜報表驗證和錯誤等級＞一節。  
  
-   TargetServerVersion 是部署屬性，可以識別 TargetServerURL 屬性中所指定之目標報表伺服器上安裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 預期版本。  
  
 當您在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 對話方塊中指定舊版 **[專案屬性]** 時，系統不會自動將報表還原到舊版。 因此，報表伺服器專案可以包含來自兩個不同版本之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的報表。 部署報表伺服器專案時，專案中的所有報表會轉換為 TargetServerVersion 中指定的版本。  
  
 您可以在專案中加入一個以上的專案組態。而每一個專案組態都用於不同的狀況，例如，部署到不同版本的報表伺服器。 如需詳細資訊，請參閱[設定部署屬性 &#40;Reporting Services&#41;](set-deployment-properties-reporting-services.md) 和[專案屬性頁對話方塊](project-property-pages-dialog-box.md)。  
  
##  <a name="bkmk_SupportedVersions"></a> 支援的版本  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)](報表伺服器專案的 32 位元開發環境) 不是設計成要在 [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)]架構電腦上執行，而且未安裝在 [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)]架構伺服器上。 不過， [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 仍支援 x64 架構的電腦。  
  
 下表描述在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中撰寫及發行報表所支援的版本。  
  
> [!NOTE]  
>  此結構描述從 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]之後並未變更。  
  
|專案或檔案類型|版本|撰寫報表|發行報表|注意|  
|--------------------------|-------------|--------------------|---------------------|-----------|  
|報表伺服器專案<br /><br /> 中的多個<br /><br /> 報表伺服器精靈專案|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|2014 RDL 結構描述|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|報表伺服器專案<br /><br /> 中的多個<br /><br /> 報表伺服器精靈專案|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|2012 RDL 結構描述|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|報表伺服器專案<br /><br /> 中的多個<br /><br /> 報表伺服器精靈專案|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|2008 R2 RDL 結構描述|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|報表伺服器專案<br /><br /> 中的多個<br /><br /> 報表伺服器精靈專案|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|2008 RDL 結構描述|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器|在本機將 2003 RDL 和 2005 RDL 升級到 2008 RDL 結構描述。|  
|報表伺服器專案<br /><br /> 中的多個<br /><br /> 報表伺服器精靈專案|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|2005 RDL 結構描述|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或是[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]報表伺服器||  
|報表伺服器專案|[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]|2003 RDL 結構描述|不支援||  
|[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] RDLC 報表設計師|[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 2005<br /><br /> [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 2008|2005 RDL 結構描述|不支援|不支援 2008 RDL 結構描述。|  
|[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 檢視器控制項|[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 2005<br /><br /> [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 2008|本機模式中不支援 2008 RDL|N/A|可以在伺服器模式下於 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器上檢視 2008 RDL 報表。|  
  
 如需在舊版報表定義結構描述中開啟報表的詳細資訊，請參閱[升級報表](../install-windows/upgrade-reports.md)。 如需有關特定報表定義結構描述的詳細資訊，請參閱＜ [報表定義語言規格](https://go.microsoft.com/fwlink/?linkid=116865)＞。  
  
## <a name="see-also"></a>另請參閱  
 [發行資料來源與報表](../reports/publishing-data-sources-and-reports.md)  
  
  
