---
title: "選擇資料來源 （SQL Server 匯入和匯出精靈） |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.chooseadatasource.f1
ms.assetid: ebf28a62-dfc1-4b39-9db5-df1919e5fccb
caps.latest.revision: 124
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 80d35cb294fd900611c73ca37bba2a66baef0767
ms.contentlocale: zh-tw
ms.lasthandoff: 08/28/2017

---
# <a name="choose-a-data-source-sql-server-import-and-export-wizard"></a>選擇資料來源 (SQL Server 匯入和匯出精靈)
  在 [歡迎使用] 頁面出現之後，[ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈] 會顯示 [選擇資料來源] 。 在此頁面上，您可以提供資料來源及其連接方式的相關資訊。
  
如需您可以使用之資料來源的資訊，請參閱 [我可以使用哪些資料來源和目的地？](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)

## <a name="screen-shot-of-the-choose-a-data-source-page"></a>[選擇資料來源] 頁面的螢幕擷取畫面 
下列螢幕擷取畫面顯示精靈的 [選擇資料來源]  頁面中的第一個部分。 網頁的其餘有數目可變的選項，這取決於您在此處選擇的資料來源。

![選擇來源](../../integration-services/import-export-data/media/choose-source.png)

## <a name="choose-a-data-source"></a>選擇資料來源
 **資料來源**  
選取可連接到來源的資料提供者來指定資料來源。

-   **您需要的資料提供者會從其名稱通常看出**，因為提供者的名稱通常會包含資料來源的名稱，例如*一般檔案*來源、 Microsoft *Excel*，Microsoft*存取*，.Net Framework Data Provider for *SqlServer*，.Net Framework Data Provider for *Oracle*。

-   **如果您的 ODBC 驅動程式資料來源**，選取 .Net Framework Data Provider for ODBC。 然後輸入驅動程式特有的資訊。 ODBC 驅動程式未列在下拉式清單中的資料來源。 .Net Framework Data Provider for ODBC 做為包裝函式，ODBC 驅動程式。 如需詳細資訊，請參閱[連接到 ODBC 資料來源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。

-   **您的資料來源可能有一個以上的提供者可用。** 通常，您可以選取適用於來源的任何提供者。 例如，若要連線到 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您可以使用.NET Framework Data Provider for SQL Server 或 SQL Server ODBC 驅動程式。 （其他提供者也依然會在清單中的但已不再支援）。 

## <a name="my-data-source-isnt-in-the-list"></a>我的資料來源不在清單中
-   **您可能要下載的資料提供者**來自 Microsoft 或第三方。 中可用的資料提供者清單**資料來源**清單包含您電腦上安裝的提供者。 如需您可以使用之資料來源的資訊，請參閱 [我可以使用哪些資料來源和目的地？](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)

-   **您是否有 ODBC 驅動程式的資料來源？** ODBC 驅動程式未列在下拉式清單中的資料來源。 如果您的資料來源的 ODBC 驅動程式，選取 .Net Framework Data Provider for ODBC。 然後輸入驅動程式特有的資訊。 .Net Framework Data Provider for ODBC 做為包裝函式，ODBC 驅動程式。 如需詳細資訊，請參閱[連接到 ODBC 資料來源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。

-   **64 位元和 32 位元提供者。** 如果您執行 64 位元精靈，您就不會看到資料來源只有 32 位元提供者已安裝，反之亦然。

> [!NOTE]
> 若要使用 64 位元版本的 SQL Server 匯入和匯出精靈，您必須安裝 SQL Server。 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 是 32 位元應用程式，並只安裝 32 位元檔案，包括 32 位元版本的精靈。

## <a name="after-you-choose-a-data-source"></a>選擇資料來源之後
選擇資料來源，其餘的之後**選擇資料來源**頁面有數目可變的選項，這取決於您選擇的資料提供者。

若要連接至常用的資料來源，請參閱下列頁面。
-   [連接到 SQL Server](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [連接到 Oracle](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [連接到一般檔案 （文字檔）](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [連接到 Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [連接到 Access](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [使用 ODBC 連接](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [連接到 Azure Blob 儲存體](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [連接到 PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [連接到 MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)

如需如何連接到未在此處列出的資料來源資訊，請參閱[連接字串參考](https://www.connectionstrings.com/)。 此第三方網站包含範例連接字串和資料提供者的詳細資訊以及它們需要的連接資訊。

## <a name="whats-next"></a>下一步  
 在您提供資料來源及其連接方式的相關資訊之後，下一個頁面為 [選擇目的地] 。 在此頁面上，您可以提供資料目的地及其連接方式的相關資訊。 如需詳細資訊，請參閱 [選擇目的地](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)。
 
## <a name="see-also"></a>另請參閱
[透過匯入和匯出精靈的簡單範例開始使用](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)



