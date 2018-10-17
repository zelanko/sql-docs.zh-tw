---
title: 設定 PowerPivot 及部署方案 (SharePoint 2013) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 6401fd92-f43b-450e-8298-12db644c25bc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4f06745f47bd78df8d9464c090afb46116594e8b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48104798"
---
# <a name="configure-powerpivot-and-deploy-solutions-sharepoint-2013"></a>設定 PowerPivot 及部署方案 (SharePoint 2013)
  本主題描述如何部署和設定 PowerPivot 功能的中介層增強功能[!INCLUDE[SPS2013](../../../includes/sps2013-md.md)]包括 PowerPivot 圖庫、 排程資料重新整理、 管理儀表板和資料提供者。 請執行 **PowerPivot for SharePoint 2013 組態** 工具以完成下列作業：  
  
-   部署 SharePoint 方案檔。  
  
-   建立 PowerPivot 服務應用程式。  
  
-   將 Excel Services 應用程式設定為使用 SharePoint 模式的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 伺服器。 如需有關後端服務和安裝[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]伺服器在 SharePoint 模式中，請參閱[PowerPivot for SharePoint 2013 安裝](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)。  
  
 如需安裝 PowerPivot for SharePoint 2013 組態工具的詳細資訊，請參閱[安裝或解除安裝 PowerPivot for SharePoint 增益集&#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
 本主題包含下列幾節：  
  
 [執行 PowerPivot for SharePoint 2013 組態](#bkmk_run_configuration_tool)  
  
 [確認 PowerPivot 組態](#bkmk_verify_powerpivot)  
  
 [疑難排解問題](#bkmk_troubleshoot_issues)  
  
##  <a name="bkmk_run_configuration_tool"></a> 執行 PowerPivot for SharePoint 2013 組態  
 **注意** ： [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 安裝精靈會為 [!INCLUDE[ssGeminiLong](../../../includes/ssgeminilong-md.md)]安裝兩個不同的組態工具。 它們各支援不同的 SharePoint 版本。  
  
|名稱|描述|  
|----------|-----------------|  
|PowerPivot for SharePoint 2013 組態|SharePoint 2013|  
|PowerPivot 組態工具|SharePoint 2010 含 SharePoint 2010 Service Pack 1 (SP1)|  
  
 **注意：** 若要完成下列步驟，您必須是伺服器陣列管理員。 如果您看到類似下列的錯誤訊息：  
  
-   「使用者不是伺服器陣列管理員。 請解決驗證失敗問題，並再試一次。」  
  
 請以安裝 SharePoint 的帳戶登入或將安裝帳戶設定為 SharePoint 管理中心網站的主要管理員。  
  
1.  上**開始**] 功能表中，按一下**所有程式**，然後按一下[!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]，按一下 **組態工具**，然後按一下  **PowerPivot For SharePoint2013 組態**。 只有在本機伺服器上安裝了 PowerPivot for SharePoint 時，才會列出此工具。  
  
2.  按一下 **[設定或修復 PowerPivot for SharePoint]** ，然後按一下 **[確定]**。  
  
3.  此工具會執行驗證，以確認 PowerPivot 的目前狀態，而且需要哪些步驟來完成組態。 將視窗展開為全螢幕。 您應該會在視窗底部看到一個按鈕列，其中包含 **[驗證]**、 **[執行]** 和 **[結束]** 命令。  
  
4.  在 **[參數]** 索引標籤上：  
  
    1.  **預設帳戶使用者名稱**：輸入預設帳戶的網域使用者帳戶。 此帳戶將用來佈建服務，包括 PowerPivot 服務應用程式集區。 請勿指定內建帳戶，例如 Network Service 或 Local System。 此工具會封鎖指定內建帳戶的組態。  
  
    2.  **資料庫伺服器**：您可以使用支援 SharePoint 伺服器陣列的 SQL Server Database Engine。  
  
    3.  **複雜密碼**：輸入複雜密碼。 如果是建立新的 SharePoint 伺服器陣列，則在您將伺服器或應用程式加入至該 SharePoint 伺服器陣列時，都會使用此複雜密碼。 如果伺服器陣列已存在，則輸入可讓您將伺服器應用程式加入至該伺服器陣列的複雜密碼。  
  
    4.  **適用於 Excel Services 的 PowerPivot 伺服器**： 輸入的名稱[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]SharePoint 模式伺服器。 在單一伺服器部署中，這個名稱與資料庫伺服器相同。 `[ServerName]\powerpivot`  
  
    5.  按一下左邊視窗中的 **[建立網站集合]** 。 請記下 **[網站 URL]** ，以便在後續步驟中參考。 如果尚未設定 SharePoint 伺服器，組態精靈會將 Web 應用程式和網站集合 URL 預設為 `http://[ServerName]`的根目錄。 若要修改預設值，請在左邊視窗中檢閱下列頁面： **[建立預設 Web 應用程式]** 和 **[部署 Web 應用程式方案]**  
  
5.  (選擇性) 檢閱用來完成每個動作的其餘輸入值。 按一下左邊視窗中的每個動作，查看並檢閱動作的詳細資料。 如需每一項的詳細資訊，請參閱下節 「 輸入值用來設定中的伺服器[設定或修復 PowerPivot for SharePoint 2010 &#40;PowerPivot 組態工具&#41;](../../../analysis-services/configure-repair-powerpivot-sharepoint-2010.md) in this 主題。  
  
6.  選擇性地移除您不想在此時處理的任何動作。 例如，如果您想要在稍後設定 Secure Store Service，請按一下 **[設定 Secure Store Service]**，然後清除 **[在工作清單中包含這個動作]** 核取方塊。  
  
7.  按一下 **[驗證]** ，檢查此工具是否有足夠的資訊來處理清單中的動作。 如果您看到驗證錯誤，請按一下左窗格中的警告，查看驗證錯誤的詳細資料。 更正任何驗證錯誤，然後再按一下 **[驗證]** 。  
  
8.  按一下 **[執行]** ，處理工作清單中的所有動作。 請注意， **[執行]** 只在驗證動作之後才可供使用。 如果 **[執行]** 未啟用，請先按一下 **[驗證]** 。  
  
 如需詳細資訊，請參閱 <<c0> [ 設定或修復 PowerPivot for SharePoint 2010 &#40;PowerPivot 組態工具&#41;</c0>](../../../analysis-services/configure-repair-powerpivot-sharepoint-2010.md)  
  
##  <a name="bkmk_verify_powerpivot"></a> 確認 PowerPivot 組態  
 **服務：**  
  
1.  在管理中心的 [系統設定] 中，按一下 **[管理伺服器上的服務]**。  
  
2.  確認 **SQL Server Analysis Services** 和 **SQL Server PowerPivot 系統服務** 都已啟動。  
  
 **伺服器陣列功能：**  
  
1.  在管理中心的 [系統設定] 中，按一下 **[管理伺服器陣列功能]**。  
  
2.  確認 **[PowerPivot 整合功能]** 為 **[使用中]**。  
  
 **網站集合功能：**  
  
1.  瀏覽至組態工具所建立的網站 URL。  
  
     按一下 **設定**![SharePoint 設定](../../../analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint 設定")，然後按一下**站台設定**。  
  
     按一下 **[網站集合功能]**。  
  
2.  確認 **[網站集合的 PowerPivot 功能整合]** 為 **[使用中]**。  
  
 **PowerPivot 服務應用程式：**  
  
1.  在管理中心的 **[應用程式管理]** 中，按一下 **[管理服務應用程式]**。  
  
2.  確認服務應用程式狀態為 **[已啟動]**。 預設名稱是 **[預設的 PowerPivot 服務應用程式]**。  
  
     按一下服務應用程式的名稱，即可針對已開啟的服務應用程式開啟 PowerPivot 管理儀表板。 在第一次使用時，需要數分鐘才能載入儀表板。  
  
 如需詳細資訊，請參閱 < [Verify a PowerPivot for SharePoint 安裝](../../../analysis-services/instances/install-windows/verify-a-power-pivot-for-sharepoint-installation.md)。  
  
##  <a name="bkmk_troubleshoot_issues"></a> 疑難排解問題  
 為了協助疑難排解問題，建議您最好先確認診斷記錄是否已啟用。  
  
1.  在 SharePoint 管理中心內，按一下 **[監視]** ，然後按一下 **[設定 Usage and Health Data Collection]**。  
  
2.  確認已選取 **[啟用使用狀況資料收集]** 。  
  
3.  確認已選取下列事件：  
  
    -   教育遙測系統使用欄位定義  
  
    -   PowerPivot 連接  
  
    -   PowerPivot 載入資料使用量  
  
    -   PowerPivot 查詢使用量  
  
    -   PowerPivot 卸載資料使用量  
  
4.  確認已選取 **[啟用健康情況資料收集]** 。  
  
5.  按一下 [確定] 。  
  
 如需有關疑難排解資料重新整理的詳細資訊，請參閱 <<c0> [ 疑難排解 PowerPivot 資料重新整理](http://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx)(http://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx)。  
  
 如需有關組態工具的詳細資訊，請參閱 < [PowerPivot 組態工具](../../power-pivot-sharepoint/power-pivot-configuration-tools.md)。  
  
  
