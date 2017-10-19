---
title: "安裝 SQL Server Reporting Services |Microsoft 文件"
ms.date: 10/10/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 52c2f8fae79884b025e067b7d628cd3154ba93f4
ms.openlocfilehash: 5ce83ff18d6908441a3eaaf05599068ec5876308
ms.contentlocale: zh-tw
ms.lasthandoff: 10/10/2017

---
# <a name="install-sql-server-reporting-services"></a>安裝 SQL Server Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

SQL Server Reporting Services 安裝牽涉到儲存報表項目、 轉譯報表，以及處理訂閱和其他報表服務的伺服器元件。  了解如何安裝 Power BI 報表伺服器。

若要下載 SQL Server 2017 Reporting Services，請移至[Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=55252)。

> [!NOTE]
> 尋找 Power BI 報表伺服器嗎？ 請參閱[安裝 Power BI 報表伺服器](https://powerbi.microsoft.com/documentation/reportserver-install-report-server/)。

## <a name="before-you-begin"></a>開始之前

安裝 Reporting Services 之前，請先檢閱[安裝 SQL Server 的硬體和軟體需求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)。

## <a name="install-your-report-server"></a>安裝報表伺服器

安裝報表伺服器是直接的。 有幾個步驟僅安裝檔案。

> [!NOTE]
> 您不需要安裝當時可用的 SQL Server Database Engine 伺服器。 您必須在安裝之後設定 Reporting Services 的其中一個。

1. 尋找 SQLServerReportingServices.exe 的位置，並啟動安裝程式。

2. 選取**安裝 Reporting Services**。

    ![安裝 Reporting Services](media/install-reporting-services/report-server-install.png)

3. 選擇版本，以安裝，然後選取 **下一步**。

    ![選擇版本](media/install-reporting-services/report-server-install-edition.png)

    您可以選擇 Evaluation 或 Developer 版本中的，從下拉式清單。

    ![Evaluation 或 developer edition](media/install-reporting-services/report-server-install-edition-select.png)

    否則，您可以輸入產品金鑰。

4. 閱讀並接受授權條款和條件，然後選取**下一步**。

5. 您需要有可用來儲存報表伺服器資料庫的 Database Engine。 選取**下一步**安裝報表伺服器。

    ![不需要安裝的資料庫](media/install-reporting-services/report-server-install-db-engine.png)

6. 指定報表伺服器的安裝位置。 選取**安裝**才能繼續。

    ![指定安裝路徑](media/install-reporting-services/report-server-install-file-path.png)

    > [!NOTE]
    > 預設路徑是 C:\Program Files\Microsoft SQL Server 報告的服務。

7. 成功安裝之後，選取**設定報表伺服器**啟動 Reporting Services 組態管理員。

    ![設定報表伺服器](media/install-reporting-services/report-server-install-configure.png)

## <a name="configuration-your-report-server"></a>設定報表伺服器

選取後**設定報表伺服器**在安裝程式中，您會看到與**報表伺服器組態管理員**。 如需詳細資訊，請參閱[報表伺服器組態管理員](reporting-services-configuration-manager-native-mode.md)。

您需要[建立報表伺服器資料庫](ssrs-report-server-create-a-report-server-database.md)完成 Reporting Services 的初始組態。 SQL Server 資料庫伺服器才能完成此步驟。

### <a name="creating-a-database-on-a-different-server"></a>另一部伺服器上建立資料庫

如果您要在一部電腦上的資料庫伺服器上建立報表伺服器資料庫，您需要將報表伺服器的服務帳戶變更為可辨識的資料庫伺服器上的認證。

根據預設，報表伺服器會使用虛擬服務帳戶。 如果您嘗試在另一部伺服器上建立資料庫，您可能會收到下列錯誤套用連接權限的步驟。

`System.Data.SqlClient.SqlException (0x80131904): Windows NT user or group '(null)' not found. Check the name again.`

若要解決錯誤，您可以變更服務帳戶以 Network Service 或網域帳戶。 服務帳戶變更為網路服務，適用於報表伺服器的機器帳戶的內容中的權限。

如需詳細資訊，請參閱[設定報表伺服器服務帳戶](configure-the-report-server-service-account-ssrs-configuration-manager.md)。

## <a name="windows-service"></a>Windows 服務

Windows 服務會建立為安裝的一部分。 它會顯示為**SQL Server Reporting Services**。 服務名稱是**SQLServerReportingServices**。

## <a name="default-url-reservations"></a>預設 URL 保留項目

URL 保留項目是由前置詞、主機名稱、通訊埠和虛擬目錄所組成：

|部分|描述|
|----------|-----------------|
|前置詞|預設前置詞是 HTTP。 如果您先前安裝的安全通訊端層 (SSL) 憑證，安裝程式會嘗試建立使用 HTTPS 前置詞的 URL 保留項目。|
|主機名稱|預設主機名稱是強式萬用字元 (+)， 它會指定報表伺服器接受解析為電腦的任何主機名稱的指定連接埠上的任何 HTTP 要求包括`http://<computername>/reportserver`， `http://localhost/reportserver`，或`http://<IPAddress>/reportserver.`|
|通訊埠|預設連接埠是 80。 如果您使用通訊埠 80 以外的任何連接埠，您必須明確地將它加入至 URL 時瀏覽器視窗中開啟 web 入口網站。|
|虛擬目錄|根據預設，ReportServer 可針對報表伺服器 Web 服務和報表格式入口網站來建立虛擬目錄。 如果是報表伺服器 Web 服務，預設虛擬目錄會是 **reportserver**。 入口網站中，預設虛擬目錄是**報表**。|

完整 URL 字串可能出現的範例如下：

- `http://+:80/reportserver`提供報表伺服器的存取權。

- `http://+:80/reports`提供存取入口網站。

## <a name="firewall"></a>防火牆

如果您要從遠端電腦存取報表伺服器，您想要確定您已設定的任何防火牆規則，如果有防火牆存在。

您要開啟您已設定您的 Web 服務 URL 和入口網站 URL 的 TCP 連接埠。 根據預設，這些被設定在 TCP 連接埠 80。

## <a name="additional-configuration"></a>其他組態

- 若要設定與 Power BI 服務的整合，因此您可以釘選到 Power BI 儀表板的報表項目，請參閱[與 Power BI 服務整合](power-bi-report-server-integration-configuration-manager.md)。

- 若要設定訂閱處理的電子郵件，請參閱[電子郵件設定](e-mail-settings-reporting-services-native-mode-configuration-manager.md)和[電子郵件傳遞的報表伺服器中](../subscriptions/e-mail-delivery-in-reporting-services.md)。

- 若要設定入口網站，以便您可以檢視和管理報表的遠端電腦上存取它，請參閱[設定供報表伺服器存取的防火牆](../report-server/configure-a-firewall-for-report-server-access.md)和[設定報表伺服器進行遠端管理](../report-server/configure-a-report-server-for-remote-administration.md).

## <a name="related-information"></a>相關資訊

如需如何安裝 SQL Server 2016 Reporting Services 原生模式的資訊，請參閱[安裝 Reporting Services 原生模式報表伺服器](install-reporting-services-native-mode-report-server.md)。 如需如何在 SharePoint 整合模式中安裝 SQL Server 2016 Reporting Services 資訊，請參閱[以 SharePoint 模式中安裝第一部報表伺服器](install-the-first-report-server-in-sharepoint-mode.md)。

## <a name="next-steps"></a>後續的步驟

您安裝報表伺服器，開始建立報表並部署到報表伺服器。 如需如何開始使用報表產生器資訊，請參閱[安裝報表產生器](../../reporting-services/install-windows/install-report-builder.md)。

使用 SQL Server Data Tools，來建立報表[下載 SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=616714)。

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
