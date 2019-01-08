---
title: 安裝或解除安裝 Powerpivot for SharePoint 增益集 (SharePoint 2016) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4a3fba818dbedfe7d21f3b3a9527ed3b83f085ef
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52407385"
---
# <a name="install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2016"></a>安裝或解除安裝 PowerPivot for SharePoint 增益集 (SharePoint 2016)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] 是應用程式伺服器元件及後端服務的集合，可以在 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 伺服器陣列中提供 [!INCLUDE[SPS2016](../../../includes/sps2016-md.md)] 資料存取功能。 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 增益集 (**spPowerpivot16.msi**) 是用來安裝應用程式伺服器元件的安裝程式套件。  
  
 **注意：** 本主題描述如何安裝[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]方案檔和[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]for SharePoint 2016 組態工具。 安裝之後，請參閱下列主題以取得組態工具和其他功能的相關資訊：[設定 Power Pivot 及部署方案 &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md)。  
  
 如需如何下載 **spPowerPivot16.msi**的相關資訊，請參閱 [Microsoft® SQL Server® 2016 Power Pivot® for Microsoft SharePoint®](https://www.microsoft.com/download/details.aspx?id=52675)。  
  
##  <a name="bkmk_background"></a> 背景  
  
-   **應用程式伺服器：** [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 功能包括使用活頁簿作為資料來源、排定的資料重新整理與 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 管理儀表板。  
  
     [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] 是部署 Analysis Services 用戶端程式庫和複製 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 安裝檔案到電腦上的**Windows Installer 封裝 (** spPowerpivot16.msi [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] )。 此安裝程式不會在 SharePoint 中部署或設定 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 功能。 預設會安裝下列元件：  
  
    -   [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)]。 此元件包含 PowerShell 指令碼 (.ps1 檔案)、SharePoint 方案套件 (.wsp)，以及在 SharePoint 2016 伺服器陣列中部署 [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] 的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 組態工具。  
  
    -   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] OLE DB Provider for Analysis Services (MSOLAP)。  
  
    -   ADOMD.NET 資料提供者。  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分析管理物件。  
  
-   **後端服務：** 如果您使用[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]for Excel 建立包含分析資料的活頁簿，您必須執行之 BI 伺服器設定的 Office Online Server[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]在[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]來存取該資料的伺服器環境中的模式。 您可以在已安裝 SharePoint Server 2016 的電腦或在沒有 SharePoint 軟體的另一部電腦上執行 SQL Server 安裝程式。 Analysis Services 沒有 SharePoint 的相依性。  
  
     如需有關安裝、解除安裝及設定後端服務的詳細資訊，請參閱以下主題：  
  
    -   [以 Power Pivot 模式安裝 Analysis Services](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
    -   [解除安裝 PowerPivot for SharePoint](../../../sql-server/install/uninstall-power-pivot-for-sharepoint.md)  
  
##  <a name="bkmk_where_to_install"></a> 在何處安裝 spPowerPivot16.msi？  
 建議的最佳做法是在 SharePoint 伺服器陣列的所有伺服器上安裝 **spPowerPivot16.msi** 以保持組態一致性，包括應用程式伺服器和 Web 前端伺服器。 安裝程式套件包含 Analysis Services 資料提供者以及 [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] 組態工具。 當您安裝 **spPowerPivot16.msi** 時，可以排除個別元件來自訂安裝。  
  
 **資料提供者：** 數個 SharePoint 和 SQL Server 技術使用 Analysis Services 資料提供者，包括 PerformancePoint Services 和 Power View。 在所有 SharePoint 伺服器上安裝 **spPowerPivot16.msi** ，可確保完整的 Analysis Services 資料提供者集和 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 連線在整個伺服器陣列中是一致可用的。  
  
> [!NOTE]  
>  您必須使用 **spPowerPivot16.msi**，在 SharePoint 2016 伺服器上安裝 Analysis Services 資料提供者。 不支援 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 功能套件中的其他安裝程式封裝，因為這些封裝不包含資料提供者在此環境中需要的 SharePoint 2016 支援檔案。  
  
 **組態工具：**[!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)]只有其中一個 SharePoint 伺服器上需要組態工具。 不過在多伺服器的伺服器陣列中，建議的最佳作法是在至少兩個伺服器上安裝組態工具，如此一來，即使其中一個伺服器已離線，您也可以存取組態工具。  
  
##  <a name="bkmk_prereq"></a> 需求和必要條件  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SharePoint Server 2016。  
  
-   **spPowerPivot16.msi** 只有 64 位元版本，符合 SharePoint 產品和技術的需求。  
  
-   中的伺服器[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]模式。 Office Online Server 會使用 SQL Server Analysis Services 執行個體當作 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 伺服器。 Analysis Services 可在本機 SharePoint 伺服器或遠端電腦上執行。 不能安裝在 Office Online Server 上。  
  
-   **權限：** 若要安裝[!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)]，目前的使用者必須是系統管理員在電腦上，以及在 SharePoint 伺服陣列管理員群組中。  
  
-   如需 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 需求和必要條件的詳細資訊，請瀏覽 [Analysis Services SharePoint 模式伺服器的硬體和軟體需求 (SQL Server 2014)](http://msdn.microsoft.com/library/fb86ca0a-518c-4c61-ae78-7680c57fae1f)。  
  
##  <a name="bkmk_install"></a> 安裝 PowerPivot for SharePoint  
 **spPowerpivot16.msi** 安裝程式封裝同時支援圖形化使用者介面和命令列模式。 這兩個安裝方法都需要您使用系統管理員權限執行 .msi。 安裝之後，請參閱下列主題以取得組態工具和其他功能的相關資訊：[設定 Power Pivot 及部署方案 &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md)。  
  
### <a name="user-interface-installation"></a>使用者介面安裝  
 若要以圖形化使用者介面安裝 [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] ，請完成下列步驟：  
  
1.  執行 **spPowerPivot16.msi**。  
  
2.  在 [歡迎使用] 頁面上，選取 [下一步]。  
  
3.  檢閱並接受授權條款，然後選取 [下一步]。  
  
4.  在 **[特徵選取]** 頁面上，已預設選取所有功能。  
  
5.  選取 **[下一步]**。  
  
6.  選取 [安裝] 進行並完成安裝。  
  
### <a name="command-line-installation"></a>命令列安裝  
 若為命令列安裝，請以系統管理權限開啟命令提示字元，然後執行 **spPowerPivot16.msi**。 例如：  
  
 `Msiexec.exe /i spPowerPivot16.msi`。  
  
 若要建立安裝記錄檔，請使用標準 MsiExec 記錄參數。 下列範例會建立記錄檔"Install_Log.txt"使用"v"詳細資訊記錄參數。  
  
```  
Msiexec.exe /i spPowerPivot16.msi /L v c:\test\Install_Log.txt  
```  
  
### <a name="quiet-command-line-installation-for-scripting"></a>指令碼的無訊息命令列安裝  
 您可以使用 **/q** 或 **/quiet** 參數，進行不會顯示任何對話方塊或警告的「無訊息」安裝。 如果您想要將增益集的安裝撰寫為指令碼，無訊息安裝相當實用。  
  
> [!IMPORTANT]  
>  如果您使用 **/q** 參數進行無訊息命令列安裝，將不會顯示使用者授權合約。 不論安裝方式為何，使用此軟體皆受到授權合約的限制，同時您有責任遵從授權合約的規定。  
  
 **若要執行無訊息安裝：**  
  
1.  **以系統管理員權限**開啟命令提示字元。  
  
2.  執行下列命令：  
  
    ```  
    Msiexec.exe /i spPowerPivot16.msi /q  
    ```  
  
### <a name="command-line-installation-to-include-specific-components"></a>包含特定元件的命令列安裝  
 並非每部 SharePoint 伺服器都需要 [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] 組態工具，不過建議至少在兩部伺服器上安裝組態工具，確保在需要時隨時可用。  
  
 當您安裝 spPowerPivot16.msi 時，可以使用命令列選項來安裝特定項目，例如資料提供者，而不安裝 [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] 組態工具。 下列命令列示範如何安裝組態工具以外的所有元件：  
  
```  
Msiexec /i spPowerPivot16.msi AGREETOLICENSE="yes" ADDLOCAL=" SQL_OLAPDM,SQL_ADOMD,SQL_AMO,SQLAS_SP_Common"  
```  
  
|選項|描述|  
|------------|-----------------|  
|Analysis_Server_SP_addin16|[!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] 組態|  
|SQL_OLAPDM|Analysis Services OLE DB Provider for SQL Server 2016|  
|SQL_ADOMD|ADOMD.NET 提供者|  
|SQL_AMO|SQL Server 2016 分析管理物件 (AMO) 提供者|  
|SQLAS_SP16_Common|適用於 SharePoint 2016 的 Analysis Services 一般元件|  
  
##  <a name="bkmk_deploy_solution"></a> 使用 PowerPivot for SharePoint 2016 組態工具部署 SharePoint 方案檔  
 spPowerPivot16.msi 複製到硬碟的其中三個檔案是 SharePoint 方案檔。 其中一個方案檔的範圍是 Web 應用程式層級，其他檔案的範圍則是伺服器陣列層級。 檔案如下：  
  
-   `PowerPivot16FarmSolution.wsp`  

-   `PowerPivot16WebApplicationSolution.wsp`  
  
 方案檔複製到下列資料夾：  
  
 `ssInstallPathTools\PowerPivotTools\SPAddinConfiguration\Resources`  
  
 在 .msi 安裝之後，請執行 [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] 組態工具，在 SharePoint 伺服器陣列中設定並部署方案。  
  
 **若要啟動組態工具：**  
  
 在 Windows [開始畫面中，輸入"power"，並在應用程式] 搜尋結果中，選取**[!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)]組態**。 請注意，搜尋結果可能包含兩個連結，因為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式會分別為 SharePoint 2013 和 SharePoint 2016 安裝不同的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 組態工具。 請務必啟動 [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] 組態工具。  
  
 ![PowerPivot for SharePoint 2016 組態](../../../analysis-services/instances/install-windows/media/powerpivot-for-sharepoint-2016-configuration.png "PowerPivot for SharePoint 2016 組態")  
  
 **Or**  
  
1.  移至 **[開始]**、 **[所有程式]**。  
  
2.  選取 [[!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]]。  
  
3.  選取 [組態工具]。  
  
4.  選取 [[!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] 組態]。  
  
 如需組態工具的詳細資訊，請參閱 [PowerPivot 組態工具](../../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)。  
  
##  <a name="bkmk_remove_addin"></a> 解除安裝或修復增益集  
  
> [!CAUTION]  
>  如果您解除安裝 **spPowerPivot16.msi** ，也會解除安裝資料提供者和組態工具。 解除安裝資料提供者會使伺服器無法連接到 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]。  
  
 您可以使用下列其中一個方法來解除安裝或修復 [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] ：  
  
1.  **Windows 控制台：** 選取  [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)] **[!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)]**。 選取 [解除安裝] 或 [修復]。  
  
2.  執行 spPowerPivot16.msi，然後選取 [移除] 選項或 [修復] 選項。  
  
 **命令列：** 若要修復或解除安裝[!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)]使用命令列中，開啟命令提示字元**系統管理員權限**並執行下列命令之一：  
  
-   若要修復，請執行下列命令：  
  
    ```  
    msiexec.exe /f spPowerPivot16.msi  
    ```  
  
 或  
  
-   若要解除安裝，請執行下列命令：  
  
    ```  
    msiexec.exe /uninstall spPowerPivot16.msi  
    ```  
  
  
