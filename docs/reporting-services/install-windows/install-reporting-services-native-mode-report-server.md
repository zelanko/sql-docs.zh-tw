---
description: 安裝 Reporting Services 2016 原生模式報表伺服器
title: 安裝 Reporting Services 2016 原生模式報表伺服器 | Microsoft Docs
ms.date: 12/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- default configuration [Reporting Services]
- report servers [Reporting Services], default configurations
- installation options [Reporting Services]
ms.assetid: 8f25e6dc-b753-400e-9e9a-50f4f35bf6c4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b741c74a2cc614ecab4e866f9bcfe26618133aa4
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891898"
---
# <a name="install-reporting-services-2016-native-mode-report-server"></a>安裝 Reporting Services 2016 原生模式報表伺服器

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

了解如何安裝原生模式的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。 這可讓您存取能管理報表和其他項目的 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 。

> [!NOTE]
> 尋找 Power BI 報表伺服器嗎？ 請參閱[安裝 Power BI 報表伺服器](https://powerbi.microsoft.com/documentation/reportserver-install-report-server/)。

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式報表伺服器是預設 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 伺服器模式，而且可以從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝精靈或命令列進行安裝。 在安裝精靈中，您也可以選擇安裝檔案並使用預設設定來設定伺服器或僅安裝檔案。 本主題檢閱 *「原生模式的預設組態」* (Default Configuration for Native Mode)，其中安裝程式會安裝及設定報表伺服器執行個體。 安裝程式完成之後，報表伺服器會執行並備妥用於基本報表檢視和報表管理。

需要額外設定訂用帳戶處理的其他功能 (例如 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 整合和電子郵件傳遞)。

## <a name="what-is-the-default-configuration"></a><a name="bkmk_whatisdefaultconfiguration"></a> 什麼是預設組態？

當您選取原生模式的預設組態選項時，安裝程式會安裝下列 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能：

- 用於檢視與管理報表和權限的報表伺服器服務 (包含報表伺服器 Web 服務、背景處理應用程式及 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] )。

- [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員

- [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 命令列公用程式 rsconfig.exe、rskeymgmt.exe 和 rs.exe。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 與 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 現在是不同的下載。

 安裝程式會針對原生模式報表伺服器安裝設定以下項目：

- 報表伺服器服務的服務帳戶。

- 報表伺服器 Web 服務 URL。

- [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] URL。

- 報表伺服器資料庫。

- 報表伺服器資料庫的服務帳戶存取。

- 報表伺服器資料庫的連線資訊，也稱為資料來源名稱 (DSN)。

 安裝程式不會設定自動執行帳戶、報表伺服器電子郵件、備份加密金鑰或向外延展部署。 您可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員來設定這些屬性。 如需詳細資訊，請參閱[報表伺服器組態管理員 &#40;原生模式&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)。

## <a name="when-to-install-the-default-configuration-for-native-mode"></a><a name="bkmk_whentoinstalldefaultconfig"></a> 何時安裝原生模式的預設組態

預設組態會在作業狀態下安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，好讓您可以在安裝程式完成之後立刻使用報表伺服器。 當您想要儲存步驟時，請指定這個模式，其方式是刪除您原本必須在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具內執行的任何必要組態工作。

安裝預設組態並不保證報表伺服器可在安裝程式完成之後運作。 當此服務啟動時，預設 URL 可能無法註冊。 請務必要測試您的安裝，以確認此服務可如預期般啟動及執行。 請參閱 [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)。

## <a name="requirements"></a><a name="bkmk_requirements"></a> 需求

預設組態選項會使用預設值來設定讓報表伺服器運作所需的核心設定， 它的需求如下：

- 檢閱[安裝 SQL Server 的硬體和軟體需求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)。

- [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 必須一起安裝在相同的執行個體中。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體會主控安裝程式所建立及設定的報表伺服器資料庫。

- 用來執行安裝程式的使用者帳戶必須是本機管理員群組的成員，而且擁有在主控報表伺服器資料庫之 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體上存取和建立資料庫的權限。

- 安裝程式必須能夠使用預設值，以保留可提供存取報表伺服器和 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]的 URL。 這些值為連接埠 80、強式萬用字元及採用 **ReportServer_\<***instance_name***>** 和 **Reports_\<***instance_name***>** 格式的虛擬目錄名稱。

- 安裝程式必須能夠使用預設值，以建立報表伺服器資料庫。 這些值為 **ReportServer** 和 **ReportServerTempDB**。 如果您現有的資料庫是來自之前的安裝，安裝程式將會被封鎖，因為它無法在原生模式的預設組態中設定報表伺服器。 您必須重新命名、移動或刪除這些資料庫，才能解除封鎖安裝程式。

如果您的電腦未能滿足預設安裝的所有需求，就必須在僅限檔案模式中安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，然後在安裝程式完成之後使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員來進行設定。

> [!IMPORTANT]
> 雖然可以在具有唯讀網域控制站 (RODC) 的環境中安裝 Reporting Services，但若要正常運作，Reporting Services 必須能夠存取讀寫網域控制站。 如果 Reporting Services 只能存取 RODC，嘗試管理服務時可能會發生錯誤。

## <a name="default-url-reservations"></a><a name="bkmk_defaultURLreservations"></a> 預設 URL 保留項目

URL 保留項目是由前置詞、主機名稱、通訊埠和虛擬目錄所組成：

|部分|描述|
|----------|-----------------|
|前置詞|預設前置詞是 HTTP。 如果您之前已安裝傳輸層安全性 (TLS) (先前稱為安全通訊端層 (SSL)) 憑證，安裝程式將會嘗試建立使用 HTTPS 前置詞的 URL 保留項目。|
|主機名稱|預設主機名稱是強式萬用字元 (+)， 它會指定報表伺服器接受解析為電腦任何主機名稱之指定連接埠上的任何 HTTP 要求，包括 `https://<computername>/reportserver`、`https://localhost/reportserver` 或 `https://<IPAddress>/reportserver`。|
|連接埠|預設連接埠是 80。 請注意，如果您使用通訊埠 80 以外的任何通訊埠，當您在瀏覽器視窗中開啟 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web 應用程式時，就必須明確將此通訊埠加入 URL 中。|
|虛擬目錄|根據預設，系統會建立虛擬目錄，報表伺服器 Web 服務使用 ReportServer_\<*instance_name*> 格式，[!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] 使用 Reports_\<*instance_name*> 格式。 如果是報表伺服器 Web 服務，預設虛擬目錄會是 **reportserver**。 如果是 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]，則預設虛擬目錄為 **reports**。|

完整 URL 字串可能出現的範例如下：

- `https://+:80/reportserver`，提供報表伺服器的存取權。

- `https://+:80/reports`，提供 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] 的存取權。

## <a name="install-native-mode-with-the-sql-server-installation-wizard"></a><a name="bkmk_installwithwizard"></a> 使用 SQL Server 安裝精靈安裝原生模式

下列清單描述在 [SQL Server 安裝精靈] 中選取的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 特定步驟和選項。 此清單不會描述您在安裝精靈中看見的每一個頁面，而是只有屬於原生模式安裝的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 相關頁面。

1. 執行 SQL Server 安裝精靈 (setup.exe) 並逐步執行下列初步頁面︰

    - 產品金鑰

    - 授權條款

    - 全域規則

    - Microsoft Update

    - 產品更新

    - 安裝安裝程式檔案

    - 安裝規則

2. 在 **[安裝程式角色]** 頁面上，選取 **[SQL Server 功能安裝]** 。

    ![適用於安裝程式角色的 SQL Server 功能安裝](../../reporting-services/install-windows/media/rs-setuprole.png "適用於安裝程式角色的 SQL Server 功能安裝")

3. 在 **[特徵選取]** 頁面上，選取下列選項：

    - (1) [Database Engine Services]  \(除非已安裝資料庫引擎執行個體)。

    - (2) [Reporting Services-原生]  。

    ![特徵選取中的 SSRS 原生模式選取](../../reporting-services/install-windows/media/rs-setupfeatureselection-native-withcircles.png "特徵選取中的 SSRS 原生模式選取")

4. 檢閱通過的 [功能規則]  。

5. 在 [執行個體組態] 頁面上，請記住，如果您選擇設定 [具名執行個體]  ，則在瀏覽至報表管理員和報表伺服器本身時，需要在 URL 中使用執行個體名稱。 如果執行個體名稱為 "THESQLINSTANCE"，則 URL 會如下所示︰

    - `https://[ServerName]/ReportServer_THESQLINSTANCE`

    - `https://[ServerName]/Reports_THESQLINSTANCE`

6. **伺服器組態**：如果您打算使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 訂閱功能，請在 [伺服器組態]  頁面上設定 SQL Server Agent [自動]  啟動類型。 預設值是 [手動]。

7. 在 [資料庫引擎組態]  頁面中新增 SQL Server 系統管理員。

8. 在 **[Reporting Services 組態]** 頁面上選取 **[安裝和設定]** 。

    ![SSRS 原生模式組態](../../reporting-services/install-windows/media/rs-setupconfiguration-native-with-circles.png "SSRS 原生模式組態")

    > [!NOTE]
    > 您必須同時選取要安裝的資料庫功能，才能使用 [安裝和設定]  。

9. 功能組態規則︰驗證通過的規則。 如果規則都通過，則安裝精靈會自動移到 [準備安裝]  。\
[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]特有的是規則會確認報表伺服器目錄和 temp 目錄資料庫尚未存在。

10. 在 [準備安裝]  頁面上，記下稍後要參考的組態檔路徑，以取得伺服器初始 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態的良好摘要，包括已安裝的元件、服務帳戶和系統管理員。

11. SQL Server 安裝精靈完成後，請利用下列基本步驟驗證預設的原生模式安裝。

    - 開啟 [ [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員]，並確認能夠連接到報表伺服器。

    - **以系統管理權限** 開啟瀏覽器，並連接到 [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]，例如 `https://localhost/Reports`。

    - 以系統管理權限開啟瀏覽器，並連接到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器頁面。 例如， `https://localhost/ReportServer`

如需詳細資訊，請參閱下列兩個主題的＜原生＞一節：

[驗證 Reporting Services 安裝](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)

[針對 Reporting Services 安裝進行疑難排解](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)

## <a name="additional-configuration"></a><a name="bkmk_additional_configuration"></a> 其他設定

- 若要設定 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 整合，以將報表項目釘選到 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 儀表板，請參閱 [Power BI 報表伺服器整合](../../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)。

- 若要設定訂閱處理的電子郵件，請參閱[電子郵件設定 - Reporting Services 原生模式](../../reporting-services/install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)和 [Reporting Services 中的電子郵件傳遞](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md)。

- 若要設定入口網站，以在報表電腦上存取它來檢視和管理報表，請參閱[設定供報表伺服器存取的防火牆](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)和[設定報表伺服器來進行遠端管理](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md)。

## <a name="see-also"></a>另請參閱

[針對 Reporting Services 安裝進行疑難排解](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)  
[驗證 Reporting Services 安裝](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)  
[設定報表伺服器服務帳戶](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)  
[設定報表伺服器 URL](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
[設定報表伺服器資料庫連接](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
[僅限檔案安裝 &#40;Reporting Services&#41;](../../reporting-services/install-windows/files-only-installation-reporting-services.md)  
[初始化報表伺服器](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)  
[在原生模式報表伺服器上設定 TLS 連線](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)  
[設定 Windows 服務帳戶與權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
