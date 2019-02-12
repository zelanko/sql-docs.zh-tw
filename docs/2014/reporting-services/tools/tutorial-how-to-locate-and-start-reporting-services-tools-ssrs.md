---
title: 教學課程：如何尋找及啟動 Reporting Services 工具 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Builder 1.0, locating and starting tool
- Reporting Services, tutorials
- Reporting Services, tools
- Reporting Services Configuration tool
- Business Intelligence Development Studio, locating and starting tool
- Model Designer [Reporting Services], locating and starting tool
- Report Designer [Reporting Services], tutorials
- tools [Reporting Services]
- tutorials [Reporting Services]
- Report Manager [Reporting Services]
ms.assetid: 51ad69d8-fe92-4662-a7cd-d235692f0c03
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 03fb1d70046fe784fecafd8d9b3092ce21962498
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56036899"
---
# <a name="tutorial-how-to-locate-and-start-reporting-services-tools-ssrs"></a>教學課程：如何尋找及啟動 Reporting Services 工具 (SSRS)
  此教學課程介紹用來設定報表伺服器、管理報表伺服器內容和作業，以及建立並發行報表的工具。 此教學課程的目的是協助新手使用者了解：如何尋找和開啟各項工具。 如果您已經熟悉這些工具，可以移至其他教學課程，協助您了解使用 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]的重要技巧。 如需有關其他教學課程的詳細資訊，請參閱 < [Reporting Services 教學課程&#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md)。  
  
 本主題內容：  
  
-   [Reporting Services 組態管理員 (原生模式)](#bkmk_configuration_manager)  
  
-   [報表管理員 （原生模式）](#bkmk_report_manager)  
  
-   [Management Studio](#bkmk_managements_studio)  
  
-   [含有報表設計師和報表精靈 的 SQL Server Data Tools](#bkmk_ssdt)  
  
-   [報表產生器](#bkmk_report_builder)  
  
##  <a name="bkmk_configuration_manager"></a> Reporting Services 組態管理員 (原生模式)  
 使用原生模式組態管理員來完成下列動作：  
  
-   指定服務帳戶。  
  
-   建立或升級報表伺服器資料庫。  
  
-   修改連接屬性。  
  
-   指定 URL。  
  
-   管理加密金鑰。  
  
-   設定自動報表處理和電子郵件報表傳遞。  
  
 **安裝：** 安裝 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 原生模式時，會同時安裝 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 設定管理員。 如需詳細資訊，請參閱 [安裝 Reporting Services 原生模式報表伺服器](../install-windows/install-reporting-services-native-mode-report-server.md)  
  
#### <a name="to-start-the-reporting-services-configuration-manager"></a>啟動 Reporting Services 組態管理員  
  
1.  在 Windows 開始 畫面中，輸入`reporting`然後在**應用程式**搜尋結果中，按一下  **Reporting Services 組態管理員**。  
  
     ![Reporting Services 組態管理員啟動中](../media/bi-ssrs-configmanager-win8-startscreen.gif "Reporting Services 組態管理員啟動中")  
  
     **Or**  
  
     依序按一下 **[開始]**、 **[程式集]**、[ [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]]、 **[組態工具]** 和 **[Reporting Services 組態管理員]**。  
  
     **[報表伺服器安裝執行個體選取範圍]** 對話方塊隨即出現，以便讓您選取所要設定的報表伺服器執行個體。  
  
2.  在 **[伺服器名稱]** 中，指定安裝報表伺服器執行個體的電腦名稱。 依預設，會指定本機電腦的名稱，但您也可以輸入遠端 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的名稱。  
  
     如果您指定遠端電腦，請按一下 **[尋找]** 來建立連接。 必須事先設定報表伺服器的遠端管理功能。 如需詳細資訊，請參閱 [設定報表伺服器來進行遠端管理](../report-server/configure-a-report-server-for-remote-administration.md)。  
  
3.  在 **在stance Name**中，選擇您要設定的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 執行個體。 只有 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]和 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 報表伺服器執行個體會出現在此清單中。 您不能設定舊版的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]。  
  
4.  按一下 **[連接]**。  
  
5.  若要確認您已啟動工具，請將結果與下圖相比較：  
  
     ![Reporting Services 組態工具](../media/rs-ui-reportserverconfigkatmai.gif "Reporting Services 組態工具")  
  
 **後續步驟：**[設定和管理報表伺服器 &#40;SSRS 原生模式&#41;](../report-server/configure-and-administer-a-report-server-ssrs-native-mode.md) 和[Reporting Services 設定管理員 &#40;原生模式&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
##  <a name="bkmk_report_manager"></a> 報表管理員 （原生模式）  
 使用[報表管理員 」 &#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md)來設定權限、 管理訂閱與排程，以及處理報表。 您也可以使用報表管理員，檢視報表。  
  
 **安裝：** 報表管理員在您安裝時安裝[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]原生模式：[安裝 Reporting Services 原生模式報表伺服器](../install-windows/install-reporting-services-native-mode-report-server.md)  
  
 在您開啟報表管理員之前，必須有足夠的權限 (一開始，只有本機管理員群組成員才有權限，可以存取報表管理員功能)。 依目前使用者的指派角色而定，報表管理員會提供不同的頁面和選項。 沒有權限的使用者就會看到空白頁。 有權限檢視報表的使用者會取得連結，按一下就可以開啟報表。 若要深入了解權限，請參閱[角色與權限 &#40;Reporting Services&#41;](../security/roles-and-permissions-reporting-services.md)。  
  
#### <a name="to-start-report-manager"></a>啟動報表管理員  
  
1.  開啟瀏覽器。 如需支援的瀏覽器和瀏覽器版本，請參閱 <<c0> [ 規劃 Reporting Services 和 Power View 瀏覽器支援&#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md)。</c0>  
  
2.  在網頁瀏覽器的網址列中，輸入報表管理員 URL。 根據預設，URL 是**http://\<伺服器名稱 > /**。 您可以使用 Reporting Services 組態工具，以確認伺服器名稱和 URL。 如需 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中所使用之 URL 的詳細資訊，請參閱[設定報表伺服器 URL &#40;SSRS 組態管理員&#41;](../install-windows/configure-report-server-urls-ssrs-configuration-manager.md)。  
  
3.  報表管理員在瀏覽器視窗中開啟。 啟動頁面是 [主資料夾] 資料夾。 視權限而定，您可能會看到其他資料夾、報表超連結，以及啟動頁面之內的資源檔案。 您也可能會在工具列上看其他按鈕和命令。  
  
4.  如果您在本機報表伺服器上執行報表管理員，請參閱[設定為原生模式報表伺服器進行本機管理&#40;SSRS&#41;](../report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)。  
  
 **後續步驟：**[設定報表管理員&#40;原生模式&#41;](../report-server/configure-web-portal.md)。  
  
##  <a name="bkmk_managements_studio"></a> Management Studio  
 報表伺服器管理員可以使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ，將報表伺服器連同其他 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 元件伺服器一起管理。 如需詳細資訊，請參閱 [Use SQL Server Management Studio](../../database-engine/use-sql-server-management-studio.md)。  
  
#### <a name="to-start-sql-server-management-studio"></a>若要啟動 SQL Server Management Studio  
  
1.  從 Windows 開始 畫面的型別`sql server`然後在**應用程式**搜尋結果中，按一下  **SQL Server Management Studio**。  
  
     ![Windows 開始畫面的 Management Studio](../media/bi-ssms-win8-startscreen.gif "Windows 開始畫面的 Management Studio")  
  
     **Or**  
  
     依序按一下 [開始] 、[所有程式] 和 [ [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]]，然後按一下 [SQL Server Management Studio] 。 此時會出現 **[連接到伺服器]** 對話方塊。  
  
2.  如果 **[連接到伺服器]** 對話方塊沒有出現，請在 **[物件總管]** 中按一下 **[連接]** ，然後選取 **[Reporting Services]**。  
  
3.  在 **[伺服器類型]** 清單中，選取 **[Reporting Services]**。 如果 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 不在清單上，就表示未安裝。  
  
4.  在 **[伺服器名稱]** 清單中，選取一個報表伺服器執行個體。 本機執行個體隨即出現在清單中。 您也可以輸入遠端 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的名稱。  
  
5.  按一下 **[連接]**。 您可以展開根節點以設定伺服器屬性、修改角色定義，或關閉報表伺服器功能。  
  
##  <a name="bkmk_ssdt"></a> 含有報表設計師和報表精靈的 SQL Server 資料工具  
 報表設計師是在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] - Business Intelligence for Visual Studio 2012 中提供的。 工具中的設計介面包括：索引標籤式視窗、精靈和用來存取報表撰寫功能的功能表。 報表設計師工具會在您選擇「報表伺服器專案」或「報表伺服器精靈」範本時提供使用。 若要深入了解，請參閱 [SQL Server Data Tools &#40;SSDT&#41; 中的 Reporting Services](reporting-services-in-sql-server-data-tools-ssdt.md)。  
  
#### <a name="to-start-report-designer"></a>啟動報表設計師  
  
1.  在 Windows 的 [開始] 畫面中，輸入 **data** ，然後在 **[應用程式]** 搜尋結果中，按一下 **[SQL Server Data Tools for Visual Studio 2012]**。  
  
     **Or**  
  
     按一下 **開始**，指向**所有程式**，指向[!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]，然後按一下**SQL Server Data Tools (SSDT)**。  
  
2.  在 [檔案]  功能表中，指向 [新增] ，然後按一下 [專案] 。  
  
3.  在 **[專案類型]** 清單中，按一下 **[商業智慧專案]**。  
  
4.  在 **[範本]** 清單中，按一下 **[報表伺服器專案]**。 下圖顯示專案範本出現在對話方塊中的情形：  
  
     ![新增專案範本對話方塊](../media/rs-ui-newrsproject.gif "新增專案範本對話方塊")  
  
5.  輸入專案的名稱與位置，或者按一下 **[瀏覽]** 然後選取位置。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 會與 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 起始頁面一起開啟。 方案總管提供類別，以供建立報表和資料來源。 您可以使用這些類別，建立新報表和資料來源。 建立報表定義時，會顯示索引標籤式視窗。 索引標籤式視窗包括 [資料]、[配置] 和 [預覽] 等視窗。  
  
 若要著手建立第一份報表，請參閱[建立基本資料表報表 &#40;SSRS 教學課程&#41;](../create-a-basic-table-report-ssrs-tutorial.md)。 若要深入了解您可以使用報表設計師中的查詢設計工具，請參閱[報表設計工具 SQL Server Data Tools 中的查詢設計工具&#40;SSRS&#41;](../report-data/query-design-tools-ssrs.md)。  
  
##  <a name="bkmk_report_builder"></a> 報表產生器  
 使用[報表產生器&#40;SSRS&#41; ](report-builder-authoring-environment-ssrs.md)中建立報表[!INCLUDE[msCoName](../../includes/msconame-md.md)]Office 相似的撰寫環境。 不論報表是利用報表設計師還是利用舊版報表產生器所建立，您都可以自訂與更新所有現有的報表。 如需您可以執行以便在本機電腦上安裝報表產生器之 ReportBuilder3.msi 檔案的位置，請連絡管理員。  
  
 **安裝：** 按一下 -版報表產生器安裝任一方法之後[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]原生模式或 SharePoint 模式。 單機版報表產生器則需要個別下載。  請參閱[安裝單機版報表產生器&#40;報表產生器&#41;](../install-windows/install-report-builder.md)  
  
#### <a name="to-start-report-builder-clickonce-from-report-manager-native-mode"></a>若要從報表管理員啟動報表產生器 ClickOnce (原生模式)  
  
1.  在網頁瀏覽器中，輸入報表伺服器的報表管理員 URL。 根據預設，URL 為 http://\<*伺服器名稱*>/reports。 報表管理員隨即開啟。  
  
2.  按一下 **[報表產生器]**。  
  
     報表產生器隨即開啟，而且您可以在報表伺服器上建立報表或開啟報表。  
  
#### <a name="to-start-report-builder-clickonce-using-a-url"></a>若要使用 URL 來啟動報表產生器 ClickOnce  
  
1.  在網頁瀏覽器中，於網址列中輸入下列 URL：  
  
     **http://\<servername>/reportserver/reportbuilder/ReportBuilder_3_0_0_0.application**  
  
2.  按 ENTER 鍵。  
  
     報表產生器隨即開啟，而且您可以在報表伺服器上建立報表或開啟報表。  
  
#### <a name="to-start-report-builder-clickonce-in-reporting-services-sharepoint-mode"></a>若要以 Reporting Services SharePoint 模式啟動報表產生器 ClickOnce  
  
1.  巡覽至包含您想要建立新報表之文件庫的網站。  
  
2.  開啟文件庫。  
  
3.  在 **[新增]** 功能表上，按一下 **[報表產生器報表]**。  
  
     報表產生器隨即開啟，而且您可以在報表伺服器上建立報表或開啟報表。  
  
#### <a name="to-start-report-builder-stand-alone"></a>若要啟動單機版報表產生器  
  
1.  在 Windows 的 [開始] 畫面中，輸入 **報表產生器** ，然後按一下 **[報表產生器 3.0]**。  
  
     **Or**  
  
     在 [開始] 功能表上，按一下 **[所有程式]**，然後按一下 **[Microsoft SQL Server 2014 報表產生器]**。  
  
2.  按一下 **[報表產生器]**。  
  
     報表產生器隨即開啟，而且您可以建立或開啟報表。  
  
3.  按一下 **[報表產生器說明]** 開啟報表產生器的文件集。  
  
## <a name="see-also"></a>另請參閱  
 [安裝、 解除安裝與報表產生器支援](../install-uninstall-and-report-builder-support.md)   
 [Reporting Services SharePoint 模式安裝&#40;SharePoint 2010 和 SharePoint 2013&#41;](../install-windows/install-reporting-services-sharepoint-mode.md)   
 [Reporting Services Report Server](../reporting-services-report-server.md)   
 [查詢設計工具，在報表設計工具的 SQL Server Data Tools &#40;SSRS&#41;](../report-data/query-design-tools-ssrs.md)   
 [Reporting Services 教學課程 &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md)  
  
  
