---
title: 連線至 MySQL 資料來源 (SQL Server 匯入和匯出精靈) | Microsoft Docs
ms.custom: ''
ms.date: 06/20/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3d7c5a38-18d3-4cc9-a241-04422cb250d3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9fc1128ff50a6b5f6fbb459dca23f518cbcd4f26
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2019
ms.locfileid: "71285687"
---
# <a name="connect-to-a-mysql-data-source-sql-server-import-and-export-wizard"></a>連線至 MySQL 資料來源 (SQL Server 匯入和匯出精靈)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


本主題示範如何透過 [SQL Server 匯入和匯出精靈] 的 [選擇資料來源]  或 [選擇目的地]  頁面，連線至 **MySQL** 資料來源。 您可以使用數個資料提供者來連線至 MySQL。

> [!IMPORTANT]
> 這一篇 Microsoft 文章範圍未涵蓋連線至 MySQL 資料庫的詳細需求和必要條件。 本文假設您已安裝 MySQL 用戶端軟體，並已成功連線至目標 MySQL 資料庫。 如需詳細資訊，請參閱 MySQL 資料庫管理員或 MySQL 文件。

## <a name="get-the-mysql-connectors"></a>取得 MySQL 連接器
從 [MySQL 連接器](https://dev.mysql.com/downloads/connector/)頁面下載本主題中所述的提供者和驅動程式。

## <a name="connect-to-mysql-with-the-net-framework-data-provider-for-mysql"></a>使用 .NET Framework Data Provider for MySQL 連線至 MySQL
當您在精靈的 [選擇資料來源]  或 [選擇目的地]  頁面上選取 [.NET Framework Data Provider for MySQL]  之後，頁面會顯示提供者的分組選項清單。 其中有許多是不易記的名稱和不熟悉的設定。 不過別擔心，因為您只需要提供一些資訊即可。 您可以忽略其他設定的預設值。

> [!NOTE]
> 不論 MySQL 是您的來源還是目的地，此資料提供者的連線選項都會相同。 也就是，您在精靈的 [選擇資料來源]  和 [選擇目的地]  頁面上看到的選項會相同。

|必要資訊|.Net Framework Data Provider for MySQL 屬性|
|---|---|
|伺服器名稱|**Server**|
|資料庫名稱|**[資料庫備份]**|
|驗證 (登入) 資訊|[使用者識別碼]  和 [密碼] |

您不需要在清單的 [ConnectionString]  欄位中輸入連接字串。 當您為 MySQL 伺服器名稱 ([伺服器]  ) 和登入資訊輸入個別的值之後，精靈即會從個別的屬性和屬性值來組合連接字串。 

![使用 .NET 提供者連線至 MySQL，1 / 2](../../integration-services/import-export-data/media/connect-to-mysql-with-the-net-provider-1-of-2.png)

![使用 .NET 提供者連線至 MySQL，2 / 2](../../integration-services/import-export-data/media/connect-to-mysql-with-the-net-provider-2-of-2.png)

## <a name="connect-to-mysql-with-the-mysql-odbc-driver"></a>使用 MySQL ODBC 驅動程式連線至 MySQL
ODBC 驅動程式未列在資料來源的下拉式清單中。 若要使用 ODBC 驅動程式連線，請先在 [選擇資料來源]  或 [選擇目的地]  頁面上，將 [.NET Framework Data Provider for ODBC]  選取為資料來源。 此提供者作用為 ODBC 驅動程式的包裝函式。

以下是您選取 .NET Framework Data Provider for ODBC 之後立即看到的一般畫面。

![之前使用 ODBC 連線至 SQL](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-mysql-odbc-driver"></a>要指定的選項 (MySQL ODBC 驅動程式)

> [!NOTE]
> 不論 MySQL 是您的來源還是目的地，此資料提供者和 ODBC 驅動程式的連線選項都會相同。 也就是，您在精靈的 [選擇資料來源]  和 [選擇目的地]  頁面上看到的選項會相同。

若要使用 MySQL ODBC 驅動程式連線至 MySQL，請組合包含下列設定和其值的連接字串。 完整連接字串的格式緊接在設定清單後面。

> [!TIP]
> 取得組合正確連接字串的說明。 或者，您可以提供現有 DSN (資料來源名稱) 或建立新的 DSN，而不提供連接字串。 如需這些選項的詳細資訊，請參閱[連線至 ODBC 資料來源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。

**驅動程式**  
ODBC 驅動程式的名稱。

**Server**  
MySQL 伺服器的名稱。 

**[資料庫備份]**  
MySQL 伺服器的名稱。

**UID** 和 **PWD**   
用來進行連線的使用者識別碼和密碼。

### <a name="connection-string-format"></a>連接字串格式
以下是一般連接字串的格式。

    ```
    Driver={MySQL ODBC 5.3 Unicode Driver};Server=<server>;Database=<database>;UID=<user id>;PWD=<password>
    ```

### <a name="enter-the-connection-string"></a>輸入連接字串
在 [選擇資料來源]  或 [選擇目的地]  頁面上，於 [ConnectionString]  欄位中輸入連接字串，或在 [Dsn]  欄位中輸入 DSN 名稱。 輸入連接字串之後，精靈會剖析字串，並在清單中顯示個別屬性和其值。

下列範例使用此連接字串。

    ```
    Driver={MySQL ODBC 5.3 Unicode Driver};Server=127.0.0.1;Database=world;UID=root;PWD=********
    ```

以下是您在輸入連接字串之後看到的畫面。

![使用 ODBC 連線至 MySQL](../../integration-services/import-export-data/media/connect-to-mysql-with-odbc.png)

## <a name="other-data-providers-and-more-info"></a>其他資料提供者和其他資訊
若要了解如何使用此處未列出的資料提供者連線至 MySQL 的資訊，請參閱 [MySQL connection strings](https://www.connectionstrings.com/mysql/) (MySQL 連接字串)。 此協力廠商網站也會包含此頁面上所述之資料提供者和連線參數的詳細資訊。

## <a name="see-also"></a>另請參閱
[選擇資料來源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[選擇目的地](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

