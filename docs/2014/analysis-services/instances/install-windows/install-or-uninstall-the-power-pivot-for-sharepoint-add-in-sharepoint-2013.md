---
title: 安裝或解除安裝 PowerPivot for SharePoint 增益集 (SharePoint 2013) |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: fe13ce8b-9369-4126-928a-9426f9119424
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d3a4ec824c5681cdb5d76310ec67cd1b37ba6898
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53350400"
---
# <a name="install-or-uninstall-the-powerpivot-for-sharepoint-add-in-sharepoint-2013"></a>安裝或解除安裝 PowerPivot for SharePoint 增益集 (SharePoint 2013)
  [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] 是應用程式伺服器元件及後端服務的集合，可以在 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 伺服器陣列中提供 [!INCLUDE[SPS2013](../../../includes/sps2013-md.md)] 資料存取功能。 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 增益集 (**spPowerpivot.msi**) 是用來安裝應用程式伺服器元件的安裝程式封裝。  
  
-   SharePoint 2010 部署不需要此增益集。  
  
-   包含 SharePoint 2013 和 SharePoint 模式之 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的單一伺服器部署不需要此增益集。 當您以 SharePoint 模式安裝 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 伺服器時，就會包含此增益集所安裝的元件。 如需部署範例的增益集的圖表，請參閱[在 SharePoint 中的 SQL Server BI 功能的部署拓撲](../../../sql-server/install/deployment-topologies-for-sql-server-bi-features-in-sharepoint.md)。  
  
 **注意：** 本主題將描述如何安裝 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 方案檔以及 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 2013 組態工具。 安裝之後，請參閱下列主題以取得資訊的組態工具和其他功能，[設定 PowerPivot 及部署解決方案&#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md)。  
  
 如需有關如何下載 **spPowerPivot.msi**的詳細資訊，請參閱 [Microsoft® SQL Server® 2014 PowerPivot® for Microsoft SharePoint®](https://go.microsoft.com/fwlink/?LinkID=324854)。  
  
 **本主題內容：**  
  
-   [背景](#bkmk_background)  
  
-   [在何處安裝 spPowerPivot.msi？](#bkmk_where_to_install)  
  
-   [需求和必要條件](#bkmk_prereq)  
  
-   [若要安裝 PowerPivot for SharePoint](#bkmk_install)  
  
-   [部署 SharePoint 方案檔和 PowerPivot for SharePoint 2013 組態工具](#bkmk_deploy_solution)  
  
-   [解除安裝或修復增益集](#bkmk_remove_addin)  
  
##  <a name="bkmk_background"></a> 背景  
  
-   **應用程式伺服器：** [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 功能包括使用活頁簿做為資料來源、排程的資料重新整理與 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 管理儀表板。  
  
     [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] 是部署 Analysis Services 用戶端程式庫和複製 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 安裝檔案到電腦上的**Windows 安裝程式封裝 (** spPowerpivot.msi [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] )。 此安裝程式不會在 SharePoint 中部署或設定 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 功能。 預設會安裝下列元件：  
  
    -   [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 2013.此元件包含 PowerShell 指令碼 (.ps1 檔案)、SharePoint 方案套件 (.wsp)，以及在 SharePoint 2013 伺服器陣列中部署 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 2013 組態工具。  
  
    -   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] OLE DB Provider for Analysis Services (MSOLAP)。  
  
    -   ADOMD.NET 資料提供者。  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分析管理物件。  
  
-   **後端服務：** 如果您使用 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 建立包含分析資料的活頁簿，伺服器環境必須具有以執行 SharePoint 模式 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 之 BI 伺服器設定的 Excel Services，才可存取該資料。 您可以在已安裝 SharePoint Server 2013 的電腦或在沒有 SharePoint 軟體的另一部電腦上執行 SQL Server 安裝程式。 Analysis Services 沒有 SharePoint 的相依性。  
  
     如需有關安裝、解除安裝及設定後端服務的詳細資訊，請參閱以下主題：  
  
    -   [PowerPivot for SharePoint 2013 安裝](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
    -   [解除安裝 PowerPivot for SharePoint](../../../sql-server/install/uninstall-power-pivot-for-sharepoint.md)  
  
##  <a name="bkmk_where_to_install"></a> 在何處安裝 spPowerPivot.msi？  
 建議的最佳作法是在 SharePoint 伺服器陣列的所有伺服器上安裝 **spPowerPivot.msi** 以保持組態一致性，包括應用程式伺服器和 Web 前端伺服器。 安裝程式套件包含 Analysis Services 資料提供者以及 [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] 組態工具。 當您安裝 **spPowerPivot.msi** 時，可以排除個別元件來自訂安裝。  
  
 **資料提供者：** 數項 SharePoint 和 SQL Server 技術使用 Analysis Services 資料提供者，包括 Excel Services、PerformancePoint Services 和 Power View。 在所有 SharePoint 伺服器上安裝 **spPowerPivot.msi** ，可確保完整的 Analysis Services 資料提供者集和 PowerPivot 連接在整個伺服器陣列中是一致可用的。  
  
> [!NOTE]  
>  您必須使用 **spPowerPivot.msi**，在 SharePoint 2013 伺服器上安裝 Analysis Services 資料提供者。 不支援 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 功能套件中的其他安裝程式套件，因為這些套件不包含資料提供者在此環境中需要的 SharePoint 2013 支援檔案。  
  
 **組態工具：** 只有其中一個 SharePoint 伺服器才需要 PowerPivot for SharePoint 2013 組態工具。 不過在多伺服器的伺服器陣列中，建議的最佳作法是在至少兩個伺服器上安裝組態工具，如此一來，即使其中一個伺服器已離線，您也可以存取組態工具。  
  
##  <a name="bkmk_prereq"></a> 需求和必要條件  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SharePoint Server 2013。  
  
-   **spPowerPivot.msi** 只有 64 位元版本，符合 SharePoint 產品和技術的需求。  
  
-   PowerPivot 模式的 [!INCLUDE[ssASCurrent](../../../includes/ssascurrent-md.md)] 伺服器。 Excel Services 會使用 SQL Server Analysis Services 執行個體當做 PowerPivot 伺服器。 Analysis Services 可在本機或遠端電腦上執行。  
  
-   **權限：** 若要安裝 [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)]，目前使用者必須是電腦的系統管理員以及 SharePoint 伺服器陣列管理員群組的成員。  
  
-   如需詳細資訊[!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)]需求和必要條件，請移至[硬體和軟體需求，以 SharePoint 模式的 Analysis Services 伺服器&#40;SQL Server 2014&#41;](../../../sql-server/install/hardware-software-requirements-analysis-services-server-sharepoint-mode.md)。  
  
##  <a name="bkmk_install"></a> 若要安裝 PowerPivot for SharePoint  
 **spPowerpivot.msi** 安裝程式封裝同時支援圖形化使用者介面和命令列模式。 這兩個安裝方法都需要您使用系統管理員權限執行 .msi。 安裝之後，請參閱下列主題以取得資訊的組態工具和其他功能，[設定 PowerPivot 及部署解決方案&#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md)。  
  
### <a name="user-interface-installation"></a>使用者介面安裝  
 若要以圖形化使用者介面安裝 [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] ，請完成下列步驟：  
  
1.  執行 **SpPowerPivot.msi**。  
  
2.  在 [歡迎使用] 頁面上，按 **[下一步]** 。  
  
3.  檢閱並接受授權條款，然後按 **[下一步]**。  
  
4.  在 **[特徵選取]** 頁面上，已預設選取所有功能。  
  
5.  按 [下一步] 。  
  
6.  按一下 **[安裝]** 完成安裝。  
  
### <a name="command-line-installation"></a>命令列安裝  
 對於命令列安裝，請以系統管理權限開啟命令提示字元，然後執行 **spPowerPivot.msi**。 例如：  
  
 `Msiexec.exe /i SpPowerPivot.msi`。  
  
 若要建立安裝記錄檔，請使用標準 MsiExec 記錄參數。 下列範例會建立記錄檔"Install_Log.txt"使用"v"詳細資訊記錄參數。  
  
```  
Msiexec.exe /i SpPowerPivot.msi /L v c:\test\Install_Log.txt  
```  
  
### <a name="quiet-command-line-installation-for-scripting"></a>指令碼的無訊息命令列安裝  
 您可以使用 **/q** 或 **/quiet** 參數，進行不會顯示任何對話方塊或警告的「無訊息」安裝。 如果您想要將增益集的安裝撰寫為指令碼，無訊息安裝相當實用。  
  
> [!IMPORTANT]  
>  如果您使用 **/q** 參數進行無訊息命令列安裝，將不會顯示使用者授權合約。 不論安裝方式為何，使用此軟體皆受到授權合約的限制，同時您有責任遵從授權合約的規定。  
  
 **若要執行無訊息安裝：**  
  
1.  **以系統管理員權限**開啟命令提示字元。  
  
2.  執行下列命令：  
  
    ```  
    Msiexec.exe /i spPowerPivot.msi /q  
    ```  
  
### <a name="command-line-installation-to-include-specific-components"></a>包含特定元件的命令列安裝  
 並非每部 SharePoint 伺服器都需要 [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] 組態工具，不過建議至少在兩部伺服器上安裝組態工具，確保在需要時隨時可用。  
  
 當您安裝 spPowerPivot.msi 時，可以使用命令列選項來安裝特定項目，例如資料提供者，而不安裝 [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] 組態工具。 下列命令列示範如何安裝組態工具以外的所有元件：  
  
```  
Msiexec /i spPowerPivot.msi AGREETOLICENSE="yes" ADDLOCAL=" SQL_OLAPDM,SQL_ADOMD,SQL_AMO,SQLAS_SP_Common"  
```  
  
|選項|描述|  
|------------|-----------------|  
|Analysis_Server_SP_addin|PowerPivot 組態|  
|SQL_OLAPDM|MSOLAP|  
|SQL_ADOMD|ADOMD.net 提供者|  
|SQL_AMO|AMO 提供者|  
|SQLAS_SP_Common|適用於 SharePoint 2013 的 Analysis Services 一般元件|  
  
##  <a name="bkmk_deploy_solution"></a> 部署 SharePoint 方案檔和 PowerPivot for SharePoint 2013 組態工具  
 spPowerPivot.msi 複製到硬碟的其中三個檔案是 SharePoint 方案檔。 其中一個方案檔的範圍是 Web 應用程式層級，其他檔案的範圍則是伺服器陣列層級。 檔案如下：  
  
-   `PowerPivotFarmSolution.wsp`  
  
-   `PowerPivotFarm14Solution.wsp`  
  
-   `PowerPivotWebApplicationSolution.wsp`  
  
 方案檔複製到下列資料夾：  
  
 `C:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools\SPAddinConfiguration\Resources`  
  
 在 .msi 安裝之後，請執行 [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] 組態工具，在 SharePoint 伺服器陣列中設定並部署方案。  
  
 **若要啟動組態工具：**  
  
 在 Windows 開始畫面中，輸入"power"，然後在應用程式 搜尋結果中，按一下  **PowerPivot for SharePoint 2013 組態**。 請注意，搜尋結果可能包含兩個連結，因為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式會分別為 SharePoint 2010 和 SharePoint 2013 安裝不同的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 組態工具。 務必確定啟動 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 2013 組態工具。  
  
 ![兩個 powerpivot 組態工具](../../../analysis-services/media/as-powerpivot-configtools-bothicons.gif "兩個 powerpivot 組態工具")  
  
 **Or**  
  
1.  移至 **[開始]**、 **[所有程式]**。  
  
2.  按一下 **[Microsoft SQL Server 2014]**。  
  
3.  按一下 **[組態工具]**。  
  
4.  按一下 **[PowerPivot for SharePoint 2013 組態]**。  
  
 如需有關組態工具的詳細資訊，請參閱＜ [PowerPivot Configuration Tools](../../power-pivot-sharepoint/power-pivot-configuration-tools.md)＞。  
  
##  <a name="bkmk_remove_addin"></a> 解除安裝或修復增益集  
  
> [!CAUTION]  
>  如果您解除安裝 **spPowerPivot.msi** ，會解除安裝資料提供者和組態工具。 解除安裝資料提供者會使伺服器無法連接到 PowerPivot。  
  
 您可以使用下列其中一個方法來解除安裝或修復 [!INCLUDE[ssGeminiShortvnext](../../../includes/ssgeminishortvnext-md.md)] ：  
  
1.  **Windows 控制台：** 選取  **Microsoft SQL Server 2012 PowerPivot for SharePoint 2013**。 按一下 **[解除安裝]** 或 **[修復]**。  
  
2.  執行 spPowerPivot.msi，然後選取 **[移除]** 選項或 **[修復]** 選項。  
  
 **命令列：** 若要修復或解除安裝 PowerPivot for SharePoint 2013 使用命令列，開啟 命令提示字元**系統管理員權限**並執行下列命令之一：  
  
-   若要修復，請執行下列命令：  
  
    ```  
    msiexec.exe /f spPowerPivot.msi  
    ```  
  
 或  
  
-   若要解除安裝，請執行下列命令：  
  
    ```  
    msiexec.exe /uninstall spPowerPivot.msi  
    ```  
  
  
