---
title: 設定入口網站 | Microsoft Docs
ms.date: 05/10/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- the web portal [Reporting Services], configuring
ms.assetid: e918986c-af15-48f6-8178-256aed829c6a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f37cb519981b0f3ac0be532ad82e6ed74d073d8f
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2018
ms.locfileid: "50031700"
---
# <a name="configure-the-web-portal"></a>設定入口網站

入口網站是一個 Web 前端應用程式，可用來檢視報表、管理報表伺服器內容，以及將原生模式報表伺服器的存取權授與使用者。 如果您在安裝程式中選取 [Install in the default native mode configuration] (以預設原生模式設定安裝) 選項，入口網站就會與報表伺服器 Web 服務一起安裝在相同的報表伺服器執行個體中，而且進行選擇性設定。 您也可以將入口網站設定為後續安裝工作。 本主題會提供有關下列入口網站設定狀況的資訊：

## <a name="prerequisites"></a>Prerequisites

若要使用入口網站，您必須滿足下列必要條件：

- 您必須擁有以最低限度方式設定的報表伺服器。 如需如何以最低限度方式設定報表伺服器的詳細資訊，請參閱[設定報表伺服器](../../reporting-services/report-server/configure-a-report-server-reporting-services-native-mode.md)。

- 您的報表伺服器必須以原生模式執行。 您無法使用入口網站搭配針對 SharePoint 整合模式所設定的報表伺服器。 在 SQL Server 2012 中，您無法將報表伺服器從一種模式切換為另一種模式。 如果您要變更您環境使用之報表伺服器的類型，必須安裝所需之模式的報表伺服器，然後將報表項目複製或移動到新的報表伺服器。 這種程序通常稱為「移轉」。 移轉所需的步驟，取決於您要移轉到哪個模式以及您要從哪個版本移轉。 如需詳細資訊，請參閱＜ [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)＞。

- 您也必須擁有啟用指令碼的 Internet Explorer 11 或更新版本。 如需詳細資訊，請參閱 [Reporting Services 和 Power View 的瀏覽器支援](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)。

## <a name="configure-the-web-portal-to-use-the-default-url"></a>設定入口網站，以使用預設 URL

入口網站是使用者在網頁瀏覽器中存取的 Web 應用程式。 您至少必須定義用來在瀏覽器視窗中開啟應用程式的 URL。 此 URL 包含主機名稱、通訊埠和虛擬目錄。 此 URL 的預設值包括您針對報表伺服器 Web 服務 URL 所定義的主機名稱和通訊埠值，再加上 **reports** 虛擬目錄名稱。 如果您擁有具名執行個體，此虛擬目錄就是 **reports_instance**，其中 **instance** 是您 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體的名稱。

根據預設，入口網站 URL 包含唯一的虛擬目錄名稱，再加上針對在相同執行個體中執行報表伺服器 Web 服務所定義的通訊埠和主機名稱。 在大部分情況下，主機名稱就是報表伺服器電腦的網路名稱，但是它可能也是解析電腦的 IP 位址或主機標頭。 若要將入口網站設定為使用預設 URL，請使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 設定工具中的 [入口網站 URL] 頁面。

> [!TIP]
> 如果您嘗試存取遠端電腦上的入口網站，但是在瀏覽器中收到連線錯誤訊息，常見的原因會是防火牆設定。 如需詳細資訊，請參閱 [設定供報表伺服器存取的防火牆](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)。

#### <a name="to-configure-the-default-the-web-portal-url-and-virtual-directory"></a>設定預設的入口網站 URL 和虛擬目錄

1. 啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具，並連接到報表伺服器執行個體。

2. 在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 設定工具中，按一下 [入口網站 URL] 開啟設定 URL 的頁面。

3. 針對入口網站輸入唯一的虛擬目錄名稱。

4. 按一下 **[套用]**。

5. 如果您正在使用 [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] 或 Windows Server 2008，可能需要進行其他步驟，才能使用入口網站。 如需詳細資訊，請參閱 [設定原生模式報表伺服器進行本機管理 &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)。

## <a name="configure-the-web-portal-to-use-a-specific-report-server-url"></a>將入口網站設定為使用特定報表伺服器 URL

根據預設，入口網站會連線至在相同報表伺服器服務內執行的報表伺服器 Web 服務。 入口網站會使用報表伺服器 Web 服務 URL 來建立連線。 如果您針對報表伺服器 Web 服務定義了多個 URL，入口網站就會使用您所定義的最後一個 URL。 不過，在某些部署中，您可能會想讓入口網站一律透過靜態 URL 連線至 Web 服務。 您可能會想要這樣做的原因如下：如果您針對特定通訊埠或 IP 位址設定了封包篩選，而且想讓報表伺服器的所有連接都通過您所定義的篩選規則。

當您在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 設定工具中設定 URL 時，入口網站就會針對在相同伺服器執行個體中執行的報表伺服器，自動偵測並使用任何全新和更新的 URL。 如果您的部署要求您針對所有報表伺服器要求使用單一靜態 URL，就可以在 RSReportServer.config 檔中指定該 URL。

#### <a name="to-configure-a-static-report-server-url"></a>設定靜態報表伺服器 URL

1. 在文字編輯器中開啟 **RsReportServer.config** 檔。 根據預設，其位於 \Program Files\Microsoft SQL Server\MSRS12.\<*instancename*>\Reporting Services\ReportServer。  

2. 尋找 **ReportServerURL**。

3. 將它取代成報表伺服器執行個體的 URL。

4. 儲存您的變更，然後關閉檔案。

如需組態檔的詳細資訊，請參閱[修改 Reporting Services 組態檔 &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md) 和 [RsReportServer.config 組態檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)。

## <a name="customize-styles-or-application-title"></a>自訂樣式或應用程式標題

您可以建立自訂品牌套件來變更入口網站所使用的色彩。 如需詳細資訊，請參閱[建立入口網站品牌形象](../branding-the-web-portal.md)

#### <a name="to-modify-application-title"></a>修改應用程式標題

1. 使用被指派報表伺服器之 [系統管理員] 權限的帳戶來登入。

2. 開啟 Internet Explorer。

3. 輸入入口網站 URL。 根據預設，它是 http://\<**您的伺服器名稱**>/reports，但是如果您將 Reporting Services 安裝成具名執行個體，預設 URL 就是 http://\<**您的伺服器名稱**>/reports\<**_執行個體名稱**>。

4. 選取 [站台設定] 。

5. 在 [一般] 索引標籤的 [名稱] 中，將 **SQL Server Reporting Services** 取代成不同的名稱。

6. 選取 [套用]。

## <a name="next-steps"></a>後續步驟

[入口網站](../../reporting-services/web-portal-ssrs-native-mode.md)  
[Reporting Services 的瀏覽器支援](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)
[設定 URL](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
[驗證 Reporting Services 安裝](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)   
[開啟或關閉 Reporting Services 功能](../../reporting-services/report-server/turn-reporting-services-features-on-or-off.md)   
[管理 Reporting Services 原生模式報表伺服器](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)   
[RsReportServer.config 組態檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[設定原生模式報表伺服器進行本機管理](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)

 更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
