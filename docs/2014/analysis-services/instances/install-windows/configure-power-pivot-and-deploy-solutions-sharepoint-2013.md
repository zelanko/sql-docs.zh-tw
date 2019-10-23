---
title: 設定 PowerPivot 及部署方案（SharePoint 2013） |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6401fd92-f43b-450e-8298-12db644c25bc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6d835269f77e563b94c89c3a68c5c82844edc773
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/17/2019
ms.locfileid: "69493974"
---
# <a name="configure-powerpivot-and-deploy-solutions-sharepoint-2013"></a>設定 PowerPivot 及部署方案 (SharePoint 2013)
  本主題將描述如何部署和設定 [!INCLUDE[SPS2013](../../../includes/sps2013-md.md)] 中 PowerPivot 功能的中介層增強功能，包括 PowerPivot 圖庫、排程資料重新整理、管理儀表板和資料提供者。 請執行 **PowerPivot for SharePoint 2013 組態** 工具以完成下列作業：  
  
-   部署 SharePoint 方案檔。  
  
-   建立 PowerPivot 服務應用程式。  
  
-   將 Excel Services 應用程式設定為使用 SharePoint 模式的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 伺服器。 如需後端服務以及在 SharePoint 模式中安裝 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 伺服器的詳細資訊，請參閱[PowerPivot for SharePoint 2013 安裝](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode)。  
  
 如需安裝 PowerPivot for SharePoint 2013 設定工具的詳細資訊，請參閱[安裝或卸載 PowerPivot for SharePoint 增益集&#40;SharePoint 2013&#41; ](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013)  
  
 本主題包含下列幾節：  
  
 [執行 PowerPivot for SharePoint 2013 設定](#bkmk_run_configuration_tool)  
  
 [確認 PowerPivot 設定](#bkmk_verify_powerpivot)  
  
 [疑難排解問題](#bkmk_troubleshoot_issues)  
  
##  <a name="bkmk_run_configuration_tool"></a>執行 PowerPivot for SharePoint 2013 設定  
 **注意：** @No__t_0 安裝程式嚮導會安裝兩個不同的設定工具來進行 [!INCLUDE[ssGeminiLong](../../../includes/ssgeminilong-md.md)]。 它們各支援不同的 SharePoint 版本。  
  
|[屬性]|Description|  
|----------|-----------------|  
|PowerPivot for SharePoint 2013 組態|SharePoint 2013|  
|PowerPivot 組態工具|SharePoint 2010 含 SharePoint 2010 Service Pack 1 (SP1)|  
  
 **注意：** 若要完成下列步驟，您必須是伺服器陣列管理員。 如果您看到類似下列的錯誤訊息：  
  
-   「使用者不是伺服器陣列管理員。 請解決驗證失敗問題，並再試一次。」  
  
 請以安裝 SharePoint 的帳戶登入或將安裝帳戶設定為 SharePoint 管理中心網站的主要管理員。  
  
1.  在 **[開始]** 功能表上，依序按一下 **[所有程式]** 、[ [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]]、 **[組態工具]** 和 **[PowerPivot For SharePoint 2013 組態]** 。 只有在本機伺服器上安裝了 PowerPivot for SharePoint 時，才會列出此工具。  
  
2.  按一下 **[設定或修復 PowerPivot for SharePoint]** ，然後按一下 **[確定]** 。  
  
3.  此工具會執行驗證，以確認 PowerPivot 的目前狀態，而且需要哪些步驟來完成組態。 將視窗展開為全螢幕。 您應該會在視窗底部看到一個按鈕列，其中包含 **[驗證]** 、 **[執行]** 和 **[結束]** 命令。  
  
4.  在 **[參數]** 索引標籤上：  
  
    1.  **預設帳戶使用者名稱**：輸入預設帳戶的網域使用者帳戶。 此帳戶將用來佈建服務，包括 PowerPivot 服務應用程式集區。 請勿指定內建帳戶，例如 Network Service 或 Local System。 此工具會封鎖指定內建帳戶的組態。  
  
    2.  **資料庫伺服器**：您可以使用支援 SharePoint 伺服器陣列的 SQL Server 資料庫引擎。  
  
    3.  複雜**密碼**：輸入複雜密碼。 如果是建立新的 SharePoint 伺服器陣列，則在您將伺服器或應用程式加入至該 SharePoint 伺服器陣列時，都會使用此複雜密碼。 如果伺服器陣列已存在，則輸入可讓您將伺服器應用程式加入至該伺服器陣列的複雜密碼。  
  
    4.  **適用于 Excel Services 的 PowerPivot 服務器**：輸入 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] SharePoint 模式伺服器的名稱。 在單一伺服器部署中，這個名稱與資料庫伺服器相同。 `[ServerName]\powerpivot`  
  
    5.  按一下左邊視窗中的 **[建立網站集合]** 。 請記下 **[網站 URL]** ，以便在後續步驟中參考。 如果尚未設定 SharePoint 伺服器，組態精靈會將 Web 應用程式和網站集合 URL 預設為 `http://[ServerName]`的根目錄。 若要修改預設值，請查看左側視窗中的下列頁面：**建立預設 web 應用程式**和**部署 Web 應用程式方案**  
  
5.  (選擇性) 檢閱用來完成每個動作的其餘輸入值。 按一下左邊視窗中的每個動作，查看並檢閱動作的詳細資料。 如需每一項的詳細資訊，請參閱本主題中的 <<c0>設定或修復 PowerPivot for SharePoint &#40;2010 PowerPivot 設定工具&#41; 中用來設定伺服器的輸入值一節。</c0>  
  
6.  選擇性地移除您不想在此時處理的任何動作。 例如，如果您想要在稍後設定 Secure Store Service，請按一下 **[設定 Secure Store Service]** ，然後清除 **[在工作清單中包含這個動作]** 核取方塊。  
  
7.  按一下 **[驗證]** ，檢查此工具是否有足夠的資訊來處理清單中的動作。 如果您看到驗證錯誤，請按一下左窗格中的警告，查看驗證錯誤的詳細資料。 更正任何驗證錯誤，然後再按一下 **[驗證]** 。  
  
8.  按一下 **[執行]** ，處理工作清單中的所有動作。 請注意， **[執行]** 只在驗證動作之後才可供使用。 如果 **[執行]** 未啟用，請先按一下 **[驗證]** 。  
  
 如需詳細資訊，請參閱[設定或修復&#40;PowerPivot for SharePoint 2010 PowerPivot&#41;設定工具](../../configure-repair-powerpivot-sharepoint-2010.md)  
  
##  <a name="bkmk_verify_powerpivot"></a>確認 PowerPivot 設定  
 **服務：**  
  
1.  在管理中心的 [系統設定] 中，按一下 **[管理伺服器上的服務]** 。  
  
2.  確認 **SQL Server Analysis Services** 和 **SQL Server PowerPivot 系統服務** 都已啟動。  
  
 **伺服器陣列功能：**  
  
1.  在管理中心的 [系統設定] 中，按一下 **[管理伺服器陣列功能]** 。  
  
2.  確認 **[PowerPivot 整合功能]** 為 **[使用中]** 。  
  
 **網站集合功能：**  
  
1.  瀏覽至組態工具所建立的網站 URL。  
  
     按一下 [**設定**] [![SharePoint 設定](https://docs.microsoft.com/analysis-services/analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint 設定")]，然後按一下 [**網站設定**]。  
  
     按一下 **[網站集合功能]** 。  
  
2.  確認 **[網站集合的 PowerPivot 功能整合]** 為 **[使用中]** 。  
  
 **PowerPivot 服務應用程式：**  
  
1.  在管理中心的 **[應用程式管理]** 中，按一下 **[管理服務應用程式]** 。  
  
2.  確認服務應用程式狀態為 **[已啟動]** 。 預設名稱是 **[預設的 PowerPivot 服務應用程式]** 。  
  
     按一下服務應用程式的名稱，即可針對已開啟的服務應用程式開啟 PowerPivot 管理儀表板。 在第一次使用時，需要數分鐘才能載入儀表板。  
  
 如需詳細資訊，請參閱 [Verify a PowerPivot for SharePoint Installation](https://docs.microsoft.com/analysis-services/instances/install-windows/verify-a-power-pivot-for-sharepoint-installation)。  
  
##  <a name="bkmk_troubleshoot_issues"></a> 疑難排解問題  
 為了協助疑難排解問題，建議您最好先確認診斷記錄是否已啟用。  
  
1.  在 SharePoint 管理中心內，按一下 **[監視]** ，然後按一下 **[設定 Usage and Health Data Collection]** 。  
  
2.  確認已選取 **[啟用使用狀況資料收集]** 。  
  
3.  確認已選取下列事件：  
  
    -   教育遙測系統使用欄位定義  
  
    -   PowerPivot 連接  
  
    -   PowerPivot 載入資料使用量  
  
    -   PowerPivot 查詢使用量  
  
    -   PowerPivot 卸載資料使用量  
  
4.  確認已選取 **[啟用健康情況資料收集]** 。  
  
5.  按一下 [確定]。  
  
 如需有關疑難排解資料重新整理問題的詳細資訊，請參閱[疑難排解 PowerPivot 資料](https://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx)重新整理（ https://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx) 。  
  
 如需有關組態工具的詳細資訊，請參閱＜ [PowerPivot Configuration Tools](../../power-pivot-sharepoint/power-pivot-configuration-tools.md)＞。  
  
  
