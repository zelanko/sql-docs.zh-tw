---
title: 選擇目的地 (SQL Server 匯入和匯出精靈) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: import-export-data
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.chooseadestination.f1
ms.assetid: 1898be15-3e69-42d3-8ecb-3733c9f6c8e3
caps.latest.revision: 104
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0eeaff03133cdfa2d9077e21905c3984571f87b3
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="choose-a-destination-sql-server-import-and-export-wizard"></a>選擇目的地 (SQL Server 匯入和匯出精靈)
 在您提供有關資料來源及其連接方式的資訊之後，[ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈] 會顯示 [選擇目的地] 。 在此頁面上，您可以提供資料目的地及其連接方式的相關資訊。
  
如需您可以使用之資料目的地的資訊，請參閱 [我可以使用哪些資料來源和目的地？](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)。 

## <a name="screen-shot-of-the-destination-page"></a>[目的地] 頁面的螢幕擷取畫面
下列螢幕擷取畫面顯示精靈的 [選擇目的地]  頁面中的第一個部分。 頁面的其餘部分具有不同數目的選項，而這取決於您在此處選擇的目的地。

![選擇目的地](../../integration-services/import-export-data/media/choose-destination.png)

## <a name="choose-a-destination"></a>選擇目的地
 **目的地**  
 選取可將資料匯入目的地的資料提供者來指定目的地。
 
-   **一般來說，您可以從資料提供者的名稱來辨識您需要的資料提供者**，因為提供者的名稱通常會包含目的地的名稱，例如「一般檔案」目的地、Microsoft *Excel*、Microsoft *Access*、.Net Framework Data Provider for *SqlServer*、.Net Framework Data Provider for *Oracle*。

-   **如果您有適用於目的地的 ODBC 驅動程式**，請選取 .NET Framework Data Provider for ODBC。 然後輸入驅動程式的特定資訊。 ODBC 驅動程式未列在目的地的下拉式清單中。 .Net Framework Data Provider for ODBC 用作為 ODBC 驅動程式的包裝函式。 如需詳細資訊，請參閱[連線至 ODBC 資料來源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。

-   **您的目的地可能有一個以上的提供者可用。** 通常，您可以選取適用於目的地的任何提供者。 例如，若要連線至 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您可以使用 .NET Framework Data Provider for SQL Server 或 SQL Server ODBC 驅動程式。 (清單中依然還會有其他提供者，但已不再支援。) 

## <a name="my-destination-isnt-in-the-list"></a>我的目的地不在清單中
-   您可能必須從 Microsoft 或協力廠商**下載資料提供者**。 [目的地] 清單中可用的資料提供者清單，僅包括您在電腦上安裝的提供者。 如需您可以使用之目的地的資訊，請參閱[我可以使用哪些資料來源和目的地？](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)

-   **您是否有適用於目的地的 ODBC 驅動程式？** ODBC 驅動程式未列在目的地的下拉式清單中。 如果您有適用於目的地的 ODBC 驅動程式，請選取 .NET Framework Data Provider for ODBC。 然後輸入驅動程式特有的資訊。 .Net Framework Data Provider for ODBC 用作為 ODBC 驅動程式的包裝函式。 如需詳細資訊，請參閱[連線至 ODBC 資料來源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。

-   **64 位元和 32 位元提供者。** 如果您是執行 64 位元精靈，就不會看到只安裝 32 位元提供者的目的地，反之亦然。

> [!NOTE]
> 若要使用 64 位元版本的 [SQL Server 匯入和匯出精靈]，您必須安裝 SQL Server。 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 是 32 位元應用程式，而且只會安裝 32 位元檔案 (包含 32 位元版本的精靈)。

## <a name="after-you-choose-a-destination"></a>選擇目的地之後
選擇目的地之後，[選擇目的地] 頁面的其餘部分會有不同數目的選項，視您選擇的資料提供者而定。

若要連線至常用的目的地，請參閱下列其中一個頁面。
-   [連線到 SQL Server](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [連接到 Oracle](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [連線至一般檔案 (文字檔)](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [連線至 Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [連線至 Access](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [使用 ODBC 連線](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [連線至 Azure Blob 儲存體](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [連線至 PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [連線至 MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)

若要了解如何連線至此處未列出之目的地的資訊，請參閱[連接字串參考](https://www.connectionstrings.com/)。 此第三方網站包含範例連接字串，以及資料提供者及其所需連線資訊的更多資訊。

## <a name="whats-next"></a>下一步  
 在您提供有關資料目的地及其連接方式的資訊之後，下一個頁面是 [指定資料表複製或查詢] 。 在此頁面上，您可以指定要複製整個資料表或只複製特定資料列。 如需詳細資訊，請參閱 [指定資料表複製或查詢](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md)。  

## <a name="see-also"></a>另請參閱
[透過匯入和匯出精靈的簡單範例開始使用](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)


