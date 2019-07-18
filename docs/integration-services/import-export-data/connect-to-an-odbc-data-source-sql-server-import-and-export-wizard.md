---
title: 連線至 ODBC 資料來源 (SQL Server 匯入和匯出精靈) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e6318776-a188-48a7-995d-9eafd7148ff2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 22fd8a3e1518c535e61321255fda9c2a3f279ab1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65723942"
---
# <a name="connect-to-an-odbc-data-source-sql-server-import-and-export-wizard"></a>連線至 ODBC 資料來源 (SQL Server 匯入和匯出精靈)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


本主題示範如何透過 [SQL Server 匯入和匯出精靈] 的 [選擇資料來源] 或 [選擇目的地] 頁面，連線至 **ODBC** 資料來源。

您可能必須從 Microsoft 或協力廠商下載所需的 ODBC 驅動程式。

也可能需要查閱您必須提供的必要連接資訊。 [The Connection Strings Reference](https://www.connectionstrings.com/) (連接字串參考) 這個協力廠商網站包含範例連接字串、資料提供者的詳細資訊以及其所需的連接資訊。

## <a name="make-sure-the-driver-you-want-is-installed"></a>請確定已安裝您想要的驅動程式
1.  在控制台中搜尋或瀏覽至 [ODBC 資料來源 (64 位元)] 小程式。 如果您只有 32 位元驅動程式，或者了解您必須使用 32 位元驅動程式，請改為搜尋或瀏覽至 [ODBC 資料來源 (32 位元)]。
2.  啟動小程式。 即會開啟 [ODBC 資料來源管理員] 視窗。
3.  在 [驅動程式] 索引標籤上，您可以找到電腦上安裝的所有 ODBC 驅動程式的清單。 (部分驅動程式的名稱可能會以多種語言列出。)

    以下是已安裝之 64 位元驅動程式清單的範例。

    ![已安裝的 64 位元 ODBC 驅動程式](../../integration-services/import-export-data/media/installed-64-bit-odbc-drivers.png)

> [!TIP]
> 如果您知道驅動程式已安裝，但沒有在 64 位元小程式中看到它，請改為查看 32 位元小程式。 這也會告訴您是否需要執行 64 位元或 32 位元的 [SQL Server 匯入和匯出精靈]。
>
> 若要使用 64 位元版本的 [SQL Server 匯入和匯出精靈]，您必須安裝 SQL Server。 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 是 32 位元應用程式，而且只會安裝 32 位元檔案 (包含 32 位元版本的精靈)。
    
## <a name="step-1---select-the-data-source"></a>步驟 1 - 選取資料來源
電腦上安裝的 ODBC 驅動程式並未列在下拉式資料來源清單中。 若要使用 ODBC 驅動程式連線，請先在精靈的 [選擇資料來源] 或 [選擇目的地] 頁面上，將 [.NET Framework Data Provider for ODBC] 選取為資料來源。 此提供者作用為 ODBC 驅動程式的包裝函式。

以下是您選取 .NET Framework Data Provider for ODBC 之後立即看到的一般畫面。

![之前使用 ODBC 連線至 SQL](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

## <a name="step-2---provide-the-connection-info"></a>步驟 2 - 提供連接資訊
下一個步驟是針對 ODBC 驅動程式與資料來源提供連接資訊。 您有兩個選項。
1.  提供已經存在，或是在控制台中使用 [ODBC 資料來源管理員]小程式建立的 **DSN** (資料來源名稱)。 DSN 是連線至 ODBC 資料來源所需的已儲存設定集合。

    如果您已經知道 DSN 名稱，或了解現在要如何建立新的 DSN，則可以略過此頁面的其餘部分。 在 [選擇資料來源] 或 [選擇目的地] 頁面上的 [Dsn] 欄位中輸入 DSN 名稱，然後繼續精靈的下一個步驟。

    [提供 DSN](#odbc_dsn)
    
2.  提供您可以線上查閱，或在電腦上使用 [ODBC 資料來源管理員] 小程式建立並測試的**連接字串**。

    如果您已經有連接字串，或了解如何建立它，則可以略過此頁面的其餘部分。 在 [選擇資料來源] 或 [選擇目的地] 頁面上的 [ConnectionString] 欄位中輸入連接字串，然後繼續精靈的下一步驟。

    [提供連接字串](#odbc_connstring)

如果您提供連接字串，[選擇資料來源] 或 [選擇目的地] 頁面會顯示精靈連線至資料來源將使用的所有連接資訊，例如伺服器和資料庫名稱以及驗證方法。 如果您提供 DSN，就不會顯示這項資訊。

## <a name="odbc_dsn"></a> 選項 1 - 提供 DSN
如果您想要提供含有 DSN (資料來源名稱) 的連接資訊，請使用 [ODBC 資料來源管理員]小程式來尋找現有 DSN 的名稱，或建立新的 DSN。
1.  在控制台中搜尋或瀏覽至 [ODBC 資料來源 (64 位元)] 小程式。 如果您只有 32 位元驅動程式，或者必須使用 32 位元驅動程式，請改為搜尋或瀏覽至 [ODBC 資料來源 (32 位元)]。
2.  啟動小程式。 即會開啟 [ODBC 資料來源管理員] 視窗。 以下是小程式的外觀。

    ![ODBC 管理員控制台小程式](../../integration-services/import-export-data/media/odbc-administrator-control-panel-applet.png)
    
3.  如果您想要針對資料來源**使用現有的 DSN**，則可以使用任何您在 [使用者 DSN]、[系統 DSN] 或 [檔案 DSN] 索引標籤上看到的 DSN。檢查此名稱，然後返回精靈並在 [選擇資料來源] 或 [選擇目的地] 頁面上的 [Dsn] 欄位中輸入它。 略過此頁面的其餘部分，並繼續精靈的下一個步驟。
4.  如果您想要**建立新的 DSN**，請決定您想要讓它只有您可以看見 (使用者 DSN)、包括 Windows 服務的所有電腦使用者都可以看見 (系統 DSN)，還是儲存在檔案中 (檔案 DSN)。 這個範例會建立新的系統 DSN。
5. 在 [系統 DSN] 索引標籤中，按一下 [新增]。

    ![新增 ODBC 系統 DSN](../../integration-services/import-export-data/media/add-a-new-odbc-system-dsn.png)
    
6.  在 [建立新的資料來源] 對話方塊中，選取資料來源的驅動程式，然後按一下 [完成]。

    ![為新的系統 DSN 挑選驅動程式](../../integration-services/import-export-data/media/pick-driver-for-new-system-dsn.png)
    
7. 驅動程式現在會顯示一個或多個驅動程式專用的畫面，您可以在其中輸入連線至資料來源所需的資訊。 (若是 SQL Server 驅動程式，比方說，有四個頁面的自訂設定。)完成之後，新的系統 DSN 會顯示在清單中。

    ![清單中的新系統 DSN](../../integration-services/import-export-data/media/new-system-dsn-in-list.png)
    
8.  返回精靈，然後在 [選擇資料來源] 或 [選擇目的地] 頁面上的 [Dsn] 欄位中輸入 DSN 名稱。 繼續精靈的下一個步驟。

## <a name="odbc_connstring"></a> 選項 2 - 提供連接字串
如果您想要提供含有連接字串的連接資訊，本主題的其餘部分可協助您取得所需的連接字串。

此範例將使用下列連接字串，以連線至 Microsoft SQL Server。

    ```
    Driver={ODBC Driver 13 for SQL Server};server=localhost;database=WideWorldImporters;trusted_connection=Yes;
    ```

在 [選擇資料來源] 或 [選擇目的地] 頁面上的 [ConnectionString] 欄位中輸入連接字串。 輸入連接字串之後，精靈會剖析字串，並在清單中顯示個別屬性和屬性值。

以下是您在輸入連接字串之後看到的畫面。

![之後使用 ODBC 連線至 SQL](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

> [!NOTE]
> 不論您設定的是來源還是目的地，此ODBC 驅動程式的連線選項都會相同。 也就是，您在精靈的 [選擇資料來源] 和 [選擇目的地] 頁面上看到的選項會相同。

## <a name="get-the-connection-string-online"></a>線上取得連接字串
若要線上尋找 ODBC 驅動程式的連接字串，請參閱 [The Connection Strings Reference](https://www.connectionstrings.com/)(連接字串參考)。 這個協力廠商網站包含範例連接字串、資料提供者的詳細資訊以及其所需的連接資訊。

## <a name="get-the-connection-string-with-an-app"></a>使用應用程式取得連接字串
若要在您自己的電腦上建置並測試 ODBC 驅動程式的連接字串，您可以使用控制台中的 [ODBC 資料來源管理員] 小程式。 建立連線的檔案 DSN，然後從檔案 DSN 中複製出設定以組合連接字串。 這需要數個步驟，但可協助確認您具有有效的連接字串。

1.  在控制台中搜尋或瀏覽至 [ODBC 資料來源 (64 位元)] 小程式。 如果您只有 32 位元驅動程式，或者必須使用 32 位元驅動程式，請改為搜尋或瀏覽至 [ODBC 資料來源 (32 位元)]。
2.  啟動小程式。 即會開啟 [ODBC 資料來源管理員] 視窗。
3.  現在移至小程式的 [檔案 DSN] 索引標籤。 按一下 **[加入]**。

    在此範例中，請建立檔案 DSN，而非使用者 DSN 或系統 DSN，因為檔案 DSN 會以連接字串所需的特定格式儲存名稱/值對。

    ![新增 ODBC 檔案 DSN](../../integration-services/import-export-data/media/add-a-new-odbc-file-dsn.png)

4.  在 [建立新的資料來源] 對話方塊中，於清單中選取您的驅動程式，然後按 [下一步]。 這個範例將會建立一個 DSN，其中包含我們連線至 Microsoft SQL Server 所需的連接字串引數。

    ![建立新的 ODBC 資料來源](../../integration-services/import-export-data/media/create-new-odbc-data-source.png)
    
5.  選取位置並輸入新的檔案 DSN 的檔案名稱，然後按 [下一步]。 請記住您儲存檔案的位置，以便您可以在後續步驟中找到並開啟該檔案。

    ![儲存新的檔案 DSN](../../integration-services/import-export-data/media/save-new-file-dsn.png)

6.  檢閱您選項的摘要，然後按一下 [完成]。

7.  按一下 [完成] 之後，您選取的驅動程式會顯示一個或多個專屬畫面，以收集其連線所需的資訊。 一般來說，這項資訊包括伺服器、登入資訊和伺服器架構資料來源的資料庫，以及檔案、格式和檔案式資料來源的版本。

8. 設定資料來源並按一下 [完成] 之後，您通常會看到選項的摘要，而且可以選擇進行測試。

    ![測試新的檔案 DSN](../../integration-services/import-export-data/media/test-new-file-dsn.png)

9. 測試您的資料來源並關閉對話方塊之後，請在檔案系統中找出您儲存它的檔案 DSN。 如果您沒有變更副檔名，預設的副檔名為 .DSN。

10. 使用 [記事本] 或其他文字編輯器開啟已儲存的檔案。 以下是我們的 SQL Server 範例的內容。

    ```   
    [ODBC]  
    DRIVER=ODBC Driver 13 for SQL Server  
    TrustServerCertificate=No  
    DATABASE=WideWorldImporters    
    WSID=<local computer name>  
    APP=MicrosoftÂ® WindowsÂ® Operating System  
    Trusted_Connection=Yes  
    SERVER=localhost   
    ```
        
11. 複製必要值並將其貼到名稱/值對以分號分隔的連接字串中。

    從範例檔案 DSN 中組合必要值之後，就會有下列連接字串。
    
        ```
        DRIVER=ODBC Driver 13 for SQL Server;SERVER=localhost;DATABASE=WideWorldImporters;Trusted_Connection=Yes
        ```

    建立有效的連接字串時，通常不需要 [ODBC 資料來源管理員] 所建立之 DSN 的所有設定。  
    -   您一定要指定 ODBC 驅動程式。
    -   若是 SQL Server 等伺服器架構資料來源，您通常需要伺服器、資料庫和登入資訊。 因此在此範例 DSN 中，您不需要 TrustServerCertificate、WSID 或 APP。
    -   若是檔案式資料來源，您至少需要檔案名稱和位置。
    
12. 將此連接字串貼入精靈的 [選擇資料來源] 或 [選擇目的地] 頁面上的 [ConnectionString] 欄位。 精靈即會剖析字串，現在您已準備好繼續進行！

    ![之後使用 ODBC 連線至 SQL](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

## <a name="see-also"></a>另請參閱
[選擇資料來源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[選擇目的地](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


