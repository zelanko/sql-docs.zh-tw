---
title: "連接至 ODBC 資料來源 （SQL Server 匯入和匯出精靈） |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e6318776-a188-48a7-995d-9eafd7148ff2
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 0e3ffe2ff1695de69be7149f4be7b42f57b0e991
ms.contentlocale: zh-tw
ms.lasthandoff: 08/28/2017

---
# <a name="connect-to-an-odbc-data-source-sql-server-import-and-export-wizard"></a>連接至 ODBC 資料來源 （SQL Server 匯入和匯出精靈）
本主題說明如何連接到**ODBC**資料來源從**選擇資料來源**或**選擇目的地**SQL Server 匯入和匯出精靈 頁面。

您可能要下載您需要從 Microsoft 或第三方從 ODBC 驅動程式。

您可能要查閱您必須提供必要的連接資訊。 此協力廠商站台-[連接字串參考](https://www.connectionstrings.com/)-包含的範例連接字串和資料提供者的詳細資訊以及它們需要的連接資訊。

## <a name="make-sure-the-driver-you-want-is-installed"></a>請確定您想要安裝的驅動程式
1.  搜尋或瀏覽至**ODBC 資料來源 （64 位元）**控制台小程式。 如果您只有 32 位元驅動程式，或您知道您必須使用 32 位元驅動程式，搜尋或瀏覽至**ODBC 資料來源 （32 位元）**改為。
2.  啟動小程式。 **ODBC 資料來源管理員**視窗隨即開啟。
3.  在**驅動程式**索引標籤上，您可以找到的所有電腦上安裝的 ODBC 驅動程式清單。 （部分驅動程式的名稱可能會列出多種語言）。

    以下是已安裝 64 位元驅動程式清單的範例。

    ![已安裝的 64 位元 ODBC 驅動程式](../../integration-services/import-export-data/media/installed-64-bit-odbc-drivers.png)

> [!TIP]
> 如果您知道您的驅動程式安裝，而且您沒有看到它在 64 位元 小程式，查看在 32 位元 小程式改為。 這也會告訴您是否需要執行的 64 位元或 32 位元 SQL Server 匯入和匯出精靈 」。
>
> 若要使用 64 位元版本的 SQL Server 匯入和匯出精靈，您必須安裝 SQL Server。 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 是 32 位元應用程式，並只安裝 32 位元檔案，包括 32 位元版本的精靈。
    
## <a name="step-1---select-the-data-source"></a>步驟 1-選取的資料來源
安裝在電腦上的 ODBC 驅動程式不被列在下拉式清單中的資料來源。 若要連接的 ODBC 驅動程式，一開始選取**.NET Framework Data Provider for ODBC**做為資料來源上**選擇資料來源**或**選擇目的地**精靈頁面。 此提供者做為包裝函式，ODBC 驅動程式。

以下是您選取.NET Framework Data Provider for ODBC 之後，立即會看到泛用螢幕。

![連接到使用之前的 ODBC SQL](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

## <a name="step-2---provide-the-connection-info"></a>步驟 2-提供的連接資訊
下一個步驟是針對 ODBC 驅動程式與您資料來源提供的連接資訊。 您有兩個選項。
1.  提供**DSN** （資料來源名稱） 已經存在，或建立具有**ODBC 資料來源管理員**控制台小程式。 DSN 會儲存的連接加入 ODBC 資料來源所需的設定集合。

    如果您已經知道 DSN 名稱，或了解如何建立新的資料來源名稱，現在，您可以略過此頁面的其餘部分。 DSN 中輸入名稱**Dsn**欄位**選擇資料來源**或**選擇目的地**頁面上，然後繼續精靈的下一個步驟。

    [提供資料來源名稱](#odbc_dsn)
    
2.  提供**連接字串**，其中您可以查閱上線，或建立並測試您的電腦上**ODBC 資料來源管理員**小程式。

    如果您已經有連接字串，或了解如何建立它，您可以略過此頁面的其餘部分。 輸入中的連接字串**ConnectionString**欄位**選擇資料來源**或**選擇目的地**頁面上，然後繼續精靈的下一個步驟。

    [提供的連接字串](#odbc_connstring)

如果您提供的連接字串，**選擇資料來源**或**選擇目的地**頁面會顯示精靈即將使用連線到您的資料來源，例如伺服器和資料庫名稱和驗證方法的所有連接資訊。 如果您提供的資料來源名稱，這項資訊不會顯示。

## <a name="odbc_dsn"></a>選項 1-提供資料來源名稱
如果您想要提供連接資訊與資料來源名稱 （資料來源名稱），使用**ODBC 資料來源管理員**小程式找不到現有的資料來源名稱 的名稱，或建立新的 DSN。
1.  搜尋或瀏覽至**ODBC 資料來源 （64 位元）**控制台小程式。 如果您只安裝 32 位元驅動程式，或必須使用 32 位元驅動程式，搜尋或瀏覽至**ODBC 資料來源 （32 位元）**改為。
2.  啟動小程式。 **ODBC 資料來源管理員**視窗隨即開啟。 以下是 「 附屬應用程式的外觀。

    ![ODBC 管理員控制台小程式](../../integration-services/import-export-data/media/odbc-administrator-control-panel-applet.png)
    
3.  如果您想要**使用現有的 DSN**資料來源時，您可以使用任何您在看到的 DSN**使用者 DSN**，**系統 DSN**，或**檔案 DSN**  索引標籤。請檢查名稱，然後返回精靈並在輸入**Dsn**欄位**選擇資料來源**或**選擇目的地**頁面。 略過此頁面的其餘部分，並繼續精靈的下一個步驟。
4.  如果您想要**建立新的 DSN**、 決定您想要看是否只會為您 (使用者 DSN) 的電腦的所有使用者看見包括 Windows 服務 （系統 DSN），或儲存於檔案中 (檔案 DSN)。 這個範例會建立新的系統 DSN。
5. 在**系統 DSN**索引標籤上，按一下 **新增**。

    ![加入新的 ODBC 系統 DSN](../../integration-services/import-export-data/media/add-a-new-odbc-system-dsn.png)
    
6.  在**建立新的資料來源**對話方塊中，選取您的資料來源的驅動程式，然後按一下 **完成**。

    ![挑選新的系統 DSN 的驅動程式](../../integration-services/import-export-data/media/pick-driver-for-new-system-dsn.png)
    
7. 驅動程式現在會顯示一個或多個驅動程式專屬螢幕，您可以輸入連接到您的資料來源所需的資訊。 （SQL Server 驅動程式，例如，有四個頁面的自訂設定。）完成之後，新系統 DSN 會顯示在清單中。

    ![清單中的新系統 DSN](../../integration-services/import-export-data/media/new-system-dsn-in-list.png)
    
8.  請返回精靈並輸入中的 DSN 名稱**Dsn**欄位**選擇資料來源**或**選擇目的地**頁面。 繼續精靈的下一個步驟。

## <a name="odbc_connstring"></a>選項 2-提供的連接字串
如果您想要提供您的連接資訊連接字串，本主題的其餘部分可協助您取得您需要的連接字串。

此範例中所要使用下列連接字串中，連接到 Microsoft SQL Server。

    Driver={ODBC Driver 13 for SQL Server};server=localhost;database=WideWorldImporters;trusted_connection=Yes;

輸入中的連接字串**ConnectionString**欄位**選擇資料來源**或**選擇目的地**頁面。 您輸入的連接字串之後，精靈會剖析字串，並會顯示個別的屬性及其值清單中。

以下是您輸入的連接字串之後，請參閱螢幕。

![連接到 SQL 搭配 ODBC 之後](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

> [!NOTE]
> 是否要設定您的來源或目的地的 ODBC 驅動程式的連接選項都是相同的。 也就是您所看到的選項會同時針對相同**選擇資料來源**和**選擇目的地**精靈頁面。

## <a name="get-the-connection-string-online"></a>取得連接字串
若要尋找 ODBC 驅動程式連線的連接字串，請參閱[連接字串參考](https://www.connectionstrings.com/)。 此第三方網站包含範例連接字串和資料提供者的詳細資訊以及它們需要的連接資訊。

## <a name="get-the-connection-string-with-an-app"></a>取得與應用程式的連接字串
若要建置和測試您自己電腦上的 ODBC 驅動程式的連接字串時，您可以使用**ODBC 資料來源管理員**控制台小程式。 建立檔案 DSN 連線，然後複製設定值，超出檔案 DSN 組合連接字串。 這需要數個步驟，但可協助確認您具有有效的連接字串。

1.  搜尋或瀏覽至**ODBC 資料來源 （64 位元）**控制台小程式。 如果您只安裝 32 位元驅動程式，或必須使用 32 位元驅動程式，搜尋或瀏覽至**ODBC 資料來源 （32 位元）**改為。
2.  啟動小程式。 **ODBC 資料來源管理員**視窗隨即開啟。
3.  現在請移至**檔案 DSN**小程式 索引標籤。 按一下 **[加入]**。

    針對此範例中，建立檔案 DSN，而非使用者 DSN 或系統 DSN，因為檔案 DSN 在儲存特定格式所需的連接字串名稱 / 值組。

    ![加入新的 ODBC 檔案 DSN](../../integration-services/import-export-data/media/add-a-new-odbc-file-dsn.png)

4.  在**建立新的資料來源**對話方塊中，在清單中，選取您的驅動程式，，然後按一下**下一步**。 這個範例會建立包含我們要連接到 Microsoft SQL Server 的連接字串引數的 DSN。

    ![建立新的 ODBC 資料來源](../../integration-services/import-export-data/media/create-new-odbc-data-source.png)
    
5.  選取位置並輸入新的檔案資料來源名稱 的檔案名稱，然後按一下**下一步**。 請記住，您才能找到它，以及開啟在後續步驟中儲存檔案。

    ![儲存新檔案 DSN](../../integration-services/import-export-data/media/save-new-file-dsn.png)

6.  檢閱您選項的摘要，然後按一下**完成**。

7.  按一下 之後**完成**，您所選取的驅動程式會顯示一個或多個專屬的螢幕，以蒐集需要連接的資訊。 通常這項資訊包括伺服器、 登入資訊和資料庫伺服器為基礎的資料來源，以及檔案、 格式和以檔案為基礎的資料來源的版本。

8. 設定資料來源，並按一下之後**完成**，通常請參閱您的選擇的摘要並有機會加以測試。

    ![測試新的檔案 DSN](../../integration-services/import-export-data/media/test-new-file-dsn.png)

9. 測試您的資料來源並關閉對話方塊後，會發現在儲存在檔案系統中的 檔案 DSN。 如果您沒有變更副檔名，預設的延伸模組。資料來源名稱。

10. 使用 [記事本] 或其他文字編輯器中開啟已儲存的檔案。 以下是我們的 SQL Server 範例的內容。

        [ODBC]  
        DRIVER=ODBC Driver 13 for SQL Server  
        TrustServerCertificate=No  
        DATABASE=WideWorldImporters    
        WSID=<local computer name>  
        APP=Microsoft® Windows® Operating System  
        Trusted_Connection=Yes  
        SERVER=localhost   
        
11. 複製並貼到連接字串名稱 / 值組會以分號分隔的必要的值。

    您從範例檔案 DSN 組合需要的值之後，您會有下列連接字串。
    
        DRIVER=ODBC Driver 13 for SQL Server;SERVER=localhost;DATABASE=WideWorldImporters;Trusted_Connection=Yes

    您通常不需要建立的 ODBC 資料來源管理員來建立搭配連接字串的 DSN 中的所有設定。  
    -   您一定要指定 ODBC 驅動程式。
    -   SQL Server 等伺服器為基礎資料來源，您通常需要伺服器、 資料庫和登入資訊。 因此在 DSN 範例中，您不需要 TrustServerCertificate、 WSID 或應用程式。
    -   以檔案為基礎的資料來源，您至少需要檔案名稱和位置。
    
12. 貼上到此連接字串**ConnectionString**欄位**選擇資料來源**或**選擇目的地**精靈頁面。 精靈會將字串剖析和您準備好繼續 ！

    ![連接到 SQL 搭配 ODBC 之後](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

## <a name="see-also"></a>另請參閱
[選擇資料來源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[選擇目的地](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)



