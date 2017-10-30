---
title: "選擇目的地 （SQL Server 匯入和匯出精靈） |Microsoft 文件"
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
- sql13.dts.impexpwizard.chooseadestination.f1
ms.assetid: 1898be15-3e69-42d3-8ecb-3733c9f6c8e3
caps.latest.revision: 104
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 4ff3c7c8413bd6b535e1c5f95e2a7b06b397c053
ms.contentlocale: zh-tw
ms.lasthandoff: 08/28/2017

---
# <a name="choose-a-destination-sql-server-import-and-export-wizard"></a>選擇目的地 (SQL Server 匯入和匯出精靈)
 在您提供有關資料來源及其連接方式的資訊之後，[ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈] 會顯示 [選擇目的地] 。 在此頁面上，您可以提供資料目的地及其連接方式的相關資訊。
  
如需您可以使用之資料目的地的資訊，請參閱 [我可以使用哪些資料來源和目的地？](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)。 

## <a name="screen-shot-of-the-destination-page"></a>[目的地] 頁面的螢幕擷取畫面
下列螢幕擷取畫面顯示精靈的 [選擇目的地]  頁面中的第一個部分。 網頁的其餘的選項，這取決於您在此處選擇的目的地變數數目。

![選擇目的地](../../integration-services/import-export-data/media/choose-destination.png)

## <a name="choose-a-destination"></a>選擇目的地
 **目的地**  
 選取可將資料匯入目的地的資料提供者來指定目的地。
 
-   **您需要的資料提供者會從其名稱通常看出**，因為提供者的名稱通常會包含目的地的名稱，例如*一般檔案*目的地、 Microsoft *Excel*，Microsoft*存取*，.Net Framework Data Provider for *SqlServer*，.Net Framework Data Provider for *Oracle*。

-   **如果您的目的地中的 ODBC 驅動程式**，選取 .Net Framework Data Provider for ODBC。 然後輸入驅動程式特有的資訊。 ODBC 驅動程式未列在下拉式清單中的目的地。 .Net Framework Data Provider for ODBC 做為包裝函式，ODBC 驅動程式。 如需詳細資訊，請參閱[連接到 ODBC 資料來源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。

-   **您的目的地可能有一個以上的提供者可用。** 通常，您可以選取適用於目的地的任何提供者。 例如，若要連線到 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您可以使用.NET Framework Data Provider for SQL Server 或 SQL Server ODBC 驅動程式。 （其他提供者也依然會在清單中的但已不再支援）。 

## <a name="my-destination-isnt-in-the-list"></a>我的目的地不在清單中
-   **您可能要下載的資料提供者**來自 Microsoft 或第三方。 中可用的資料提供者清單**目的地**清單包含您電腦上安裝的提供者。 如需您可以使用目的地資訊，請參閱[何種資料來源和目的地可以使用？](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)

-   **您是否有 ODBC 驅動程式為您的目的地？** ODBC 驅動程式未列在下拉式清單中的目的地。 如果您的目的地的 ODBC 驅動程式，選取 .Net Framework Data Provider for ODBC。 然後輸入驅動程式特有的資訊。 .Net Framework Data Provider for ODBC 做為包裝函式，ODBC 驅動程式。 如需詳細資訊，請參閱[連接到 ODBC 資料來源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。

-   **64 位元和 32 位元提供者。** 如果您執行 64 位元精靈，您就不會看到目的地僅 32 位元提供者已安裝，反之亦然。

> [!NOTE]
> 若要使用 64 位元版本的 SQL Server 匯入和匯出精靈，您必須安裝 SQL Server。 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 是 32 位元應用程式，並只安裝 32 位元檔案，包括 32 位元版本的精靈。

## <a name="after-you-choose-a-destination"></a>選擇目的地之後
選擇目的地，而其餘的之後**選擇目的地**頁面有數目可變的選項，這取決於您選擇的資料提供者。

若要連接到常用的目的地，請參閱下列頁面。
-   [連接到 SQL Server](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [連接到 Oracle](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [連接到一般檔案 （文字檔）](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [連接到 Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [連接到 Access](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [使用 ODBC 連接](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [連接到 Azure Blob 儲存體](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [連接到 PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [連接到 MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)

如需如何連接到未在此處列出的目的地資訊，請參閱[連接字串參考](https://www.connectionstrings.com/)。 此第三方網站包含範例連接字串和資料提供者的詳細資訊以及它們需要的連接資訊。

## <a name="whats-next"></a>下一步  
 在您提供有關資料目的地及其連接方式的資訊之後，下一個頁面是 [指定資料表複製或查詢] 。 在此頁面上，您可以指定要複製整個資料表或只複製特定資料列。 如需詳細資訊，請參閱 [指定資料表複製或查詢](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md)。  

## <a name="see-also"></a>另請參閱
[透過匯入和匯出精靈的簡單範例開始使用](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)



