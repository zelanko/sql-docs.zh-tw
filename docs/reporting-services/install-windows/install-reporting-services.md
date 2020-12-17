---
description: 安裝 SQL Server Reporting Services
title: 安裝 SQL Server Reporting Services | Microsoft Docs
ms.date: 12/11/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>= sql-server-2016'
ms.openlocfilehash: 35924e9e1f5a72533ef1b30d983b99493858274d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484230"
---
# <a name="install-sql-server-reporting-services"></a>安裝 SQL Server Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

SQL Server Reporting Services 安裝所涉及的伺服器元件包括儲存報表項目、轉譯報表，以及處理訂閱和其他報表服務。 

::: moniker range=">=sql-server-ver15"
從 Microsoft 下載中心下載 [SQL Server 2019 Reporting Services](https://www.microsoft.com/download/details.aspx?id=100122)。

::: moniker-end

::: moniker range="=sql-server-2017"
從 Microsoft 下載中心下載 [SQL Server 2017 Reporting Services](https://www.microsoft.com/download/details.aspx?id=55252)。

::: moniker-end

> [!NOTE]
> 尋找 Power BI 報表伺服器嗎？ 請參閱[安裝 Power BI 報表伺服器](https://powerbi.microsoft.com/documentation/reportserver-install-report-server/)。
> 
> 要從 SQL Server 2016 或舊版 Reporting Services 升級或移轉？ 請參閱[升級和移轉 Reporting Services](upgrade-and-migrate-reporting-services.md)。

## <a name="before-you-begin"></a>開始之前

安裝 Reporting Services 之前，請先檢閱[安裝 SQL Server 的硬體與軟體需求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)。

## <a name="install-your-report-server"></a>安裝報表伺服器

安裝報表伺服器的過程簡潔明瞭。 安裝檔案只要幾個步驟。

> [!NOTE]
> 安裝時不需要使用 SQL Server 資料庫引擎伺服器。 安裝之後需要一部來設定 Reporting Services。

1. 找到 SQLServerReportingServices.exe 的位置，並啟動安裝程式。

2. 選取 [安裝 Reporting Services]  。

3. 選擇安裝版本，然後選取 [下一步]  。

    在免費版本中，從下拉式清單中選擇 Evaluation 或 Developer。

    ![Evaluation 或 Developer 版本](media/install-reporting-services/report-server-install-edition-select.png)

    否則，請輸入產品金鑰。 [尋找 SQL Server Reporting Services 的產品金鑰](find-reporting-services-product-key-ssrs.md)。

4. 閱讀並同意授權條款，然後選取 [下一步]  。

5. 您需要有資料庫引擎以儲存報表伺服器資料庫。 選取 [下一步]  只安裝報表伺服器。

6. 指定報表伺服器的安裝位置。 選取 [安裝]  繼續進行。

    > [!NOTE]
    > 預設路徑為 C:\Program Files\Microsoft SQL Server Reporting Services。

7. 成功安裝之後，請選取 [設定報表伺服器] 以啟動報表伺服器組態管理員。

## <a name="configure-your-report-server"></a>設定報表伺服器

在安裝程式中選取 [設定報表伺服器]  後，您會看到 **報表伺服器設定管理員**。 如需詳細資訊，請參閱[報表伺服器設定管理員](reporting-services-configuration-manager-native-mode.md)。

您需要[建立報表伺服器資料庫](ssrs-report-server-create-a-report-server-database.md)以完成 Reporting Services 的初始設定。 SQL Server Database 伺服器需要完成此步驟。

### <a name="creating-a-database-on-a-different-server"></a>在其他伺服器上建立資料庫

如果您要在其他電腦的資料庫伺服器上建立報表伺服器資料庫，您需要將報表伺服器的服務帳戶變更成資料庫伺服器可辨識的認證。

報表伺服器預設使用虛擬服務帳戶。 如果嘗試在其他伺服器上建立資料庫，您可能會在「套用連線權限」步驟收到下列錯誤。

`System.Data.SqlClient.SqlException (0x80131904): Windows NT user or group '(null)' not found. Check the name again.`

若要解決錯誤，您可以將服務帳戶變更成網路服務或網域帳戶。 將服務帳戶變更為網路服務，會套用報表伺服器電腦帳戶內容中的權限。

如需詳細資訊，請參閱[設定報表伺服器服務帳戶](configure-the-report-server-service-account-ssrs-configuration-manager.md)。

## <a name="windows-service"></a>Windows 服務

安裝時會建立 Windows 服務。 它會顯示為 **SQL Server Reporting Services**。 服務名稱是 **SQLServerReportingServices**。

## <a name="default-url-reservations"></a>預設 URL 保留項目

URL 保留項目是由前置詞、主機名稱、通訊埠和虛擬目錄所組成：

|部分|描述|
|----------|-----------------|
|前置詞|預設前置詞是 HTTP。 如果您之前已安裝傳輸層安全性 (TLS) (先前稱為安全通訊端層 (SSL)) 憑證，安裝程式會嘗試建立使用 HTTPS 前置詞的 URL 保留項目。|
|主機名稱|預設主機名稱是強式萬用字元 (+)， 它會指定報表伺服器接受解析為電腦任何主機名稱之指定連接埠上的任何 HTTP 要求，包括 `https://<computername>/reportserver`、`https://localhost/reportserver` 或 `https://<IPAddress>/reportserver.`|
|連接埠|預設連接埠是 80。 如果您使用連接埠 80 以外的任何連接埠，當您在瀏覽器視窗中開啟入口網站時，就必須明確將此連接埠新增至 URL 中。|
|虛擬目錄|根據預設，系統會建立虛擬目錄，報表伺服器 Web 服務使用 ReportServer 格式，入口網站使用 Reports 格式。 如果是報表伺服器 Web 服務，預設虛擬目錄會是 **reportserver**。 入口網站的預設虛擬目錄為 **reports**。|

完整 URL 字串可能出現的範例如下：

- `https://+:80/reportserver`，提供報表伺服器的存取權。

- `https://+:80/reports`，提供入口網站的存取權。

## <a name="firewall"></a>防火牆

如果您要從遠端電腦存取報表伺服器，如果有防火牆存在，您想要確定您已設定所有防火牆規則。

您需要開啟已為 Web 服務 URL 和入口網站 URL 設定的 TCP 連接埠。 根據預設，這些是設定在 TCP 連接埠 80。

## <a name="additional-configuration"></a>其他設定

- 若要設定與 Power BI 服務的整合，以便可將報表項目釘選到 Power BI 儀表板，請參閱[與 Power BI 服務整合](power-bi-report-server-integration-configuration-manager.md)。

- 若要設定處理訂用帳戶的電子郵件，請參閱[電子郵件設定](e-mail-settings-reporting-services-native-mode-configuration-manager.md)和[報表伺服器的電子郵件傳遞](../subscriptions/e-mail-delivery-in-reporting-services.md)。

- 若要設定入口網站，以在遠端電腦上存取它來檢視和管理報表，請參閱[設定供報表伺服器存取的防火牆](../report-server/configure-a-firewall-for-report-server-access.md)和[設定報表伺服器來進行遠端管理](../report-server/configure-a-report-server-for-remote-administration.md)。

## <a name="related-information"></a>相關資訊

如需如何安裝 SQL Server Reporting Services 原生模式的資訊，請參閱[安裝 Reporting Services 原生模式報表伺服器](install-reporting-services-native-mode-report-server.md)。 

::: moniker range="=sql-server-2016"

如需如何在 SharePoint 整合模式中安裝 SQL Server 2016 Reporting Services (和更早版本) 的資訊，請參閱[在 SharePoint 模式中安裝第一部報表伺服器](install-the-first-report-server-in-sharepoint-mode.md)。

::: moniker-end

## <a name="next-steps"></a>後續步驟

安裝好報表伺服器後，開始建立報表並將它們部署到報表伺服器。 如需如何開始何用報表產生器的資訊，請參閱[安裝報表產生器](../../reporting-services/install-windows/install-report-builder.md)。

若要建立使用 SQL Server Data Tools 的報表，請[下載 SQL Server Data Tools](https://go.microsoft.com/fwlink/?LinkID=616714)。

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
