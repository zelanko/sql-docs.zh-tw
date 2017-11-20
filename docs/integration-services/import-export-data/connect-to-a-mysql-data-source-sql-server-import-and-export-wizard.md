---
title: "連接到 MySQL 資料來源 （SQL Server 匯入和匯出精靈） |Microsoft 文件"
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3d7c5a38-18d3-4cc9-a241-04422cb250d3
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3df56fcda5b39c2895de83feac4f302686b1adf3
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-a-mysql-data-source-sql-server-import-and-export-wizard"></a>連接到 MySQL 資料來源 （SQL Server 匯入和匯出精靈）
本主題說明如何連接到**MySQL**資料來源從**選擇資料來源**或**選擇目的地**SQL Server 匯入和匯出精靈 頁面。 有數個資料提供者可讓您連接到 MySQL。

> [!IMPORTANT]
> 詳細的需求和連接到 MySQL 資料庫的必要條件等已超出 Microsoft 本文的範圍。 本文假設您已經安裝 MySQL 用戶端軟體，而且，您可以已成功連接到目標 MySQL 資料庫。 如需詳細資訊，請參閱您的 MySQL 資料庫管理員或 MySQL 文件。

## <a name="get-the-mysql-connectors"></a>取得 MySQL 連接器
下載提供者和驅動程式從本主題中所述[MySQL 連接器](https://dev.mysql.com/downloads/connector/)頁面。

## <a name="connect-to-mysql-with-the-net-framework-data-provider-for-mysql"></a>連接到 MySQL 使用.Net Framework Data Provider for MySQL
選取後**.NET Framework Data Provider for MySQL**上**選擇資料來源**或**選擇目的地**頁面在精靈的頁面會顯示群組的提供者的選項清單。 其中有許多惡意的名稱和不熟悉的設定。 幸運的是，您只需要提供一些資訊片段。 您可以忽略其他設定的預設值。

> [!NOTE]
> MySQL 為您的來源或目的地連接選項，此資料提供者都是相同的。 也就是您所看到的選項會同時針對相同**選擇資料來源**和**選擇目的地**精靈頁面。

|所需的資訊|.Net framework Data Provider for MySQL 屬性|
|---|---|
|伺服器名稱|**Server**|
|資料庫名稱|**資料庫**|
|驗證 （登入） 資訊|**使用者識別碼**和**密碼**|

您不需要輸入中的連接字串**ConnectionString**清單的欄位。 輸入 MySQL 伺服器名稱的個別值之後 (**伺服器**)，並登入資訊，此精靈將組合從個別的屬性和其值的連接字串。 

![使用.NET 提供者，1 / 2 連接到 MySQL](../../integration-services/import-export-data/media/connect-to-mysql-with-the-net-provider-1-of-2.png)

![使用.NET 提供者，2 2 連線到 MySQL](../../integration-services/import-export-data/media/connect-to-mysql-with-the-net-provider-2-of-2.png)

## <a name="connect-to-mysql-with-the-mysql-odbc-driver"></a>使用 MySQL ODBC 驅動程式連接到 MySQL
ODBC 驅動程式未列在下拉式清單中的資料來源。 若要連接的 ODBC 驅動程式，一開始選取**.NET Framework Data Provider for ODBC**做為資料來源上**選擇資料來源**或**選擇目的地**頁面。 此提供者做為包裝函式，ODBC 驅動程式。

以下是您選取.NET Framework Data Provider for ODBC 之後，立即會看到泛用螢幕。

![連接到使用之前的 ODBC SQL](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-mysql-odbc-driver"></a>選項來指定 （MySQL ODBC 驅動程式）

> [!NOTE]
> MySQL 為您的來源或目的地，此資料提供者和 ODBC 驅動程式的連接選項都相同。 也就是您所看到的選項會同時針對相同**選擇資料來源**和**選擇目的地**精靈頁面。

若要連接到 MySQL 的 MySQL ODBC 驅動程式，組合連接字串，其中包含下列設定，以及它們的值。 完整的連線字串的格式緊接在後面設定的清單。

> [!TIP]
> 取得說明組裝正確的連接字串。 或者，而不是提供的連接字串，提供現有的資料來源名稱 （資料來源名稱），或另外新建一個。 如需這些選項的詳細資訊，請參閱[連接到 ODBC 資料來源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。

**驅動程式**  
ODBC 驅動程式的名稱。

**Server**  
MySQL 伺服器的名稱。 

**資料庫**  
MySQL database 的名稱。

**UID**和**PWD**   
使用者識別碼和密碼來連接。

### <a name="connection-string-format"></a>連接字串格式
以下是一般連接字串的格式。

    ```
    Driver={MySQL ODBC 5.3 Unicode Driver};Server=<server>;Database=<database>;UID=<user id>;PWD=<password>
    ```

### <a name="enter-the-connection-string"></a>輸入連接字串
輸入中的連接字串**ConnectionString**欄位，或輸入中的 DSN 名稱**Dsn**欄位上**選擇資料來源**或**選擇目的地**頁面。 您輸入的連接字串之後，精靈會剖析字串，並會顯示個別的屬性及其值清單中。

下列範例會使用此連接字串。

    ```
    Driver={MySQL ODBC 5.3 Unicode Driver};Server=127.0.0.1;Database=world;UID=root;PWD=********
    ```

以下是您輸入的連接字串之後，請參閱螢幕。

![連接到 MySQL 使用 ODBC](../../integration-services/import-export-data/media/connect-to-mysql-with-odbc.png)

## <a name="other-data-providers-and-more-info"></a>其他資料提供者和其他資訊
如需如何連接到 MySQL 此處未列出的資料提供者資訊，請參閱[MySQL 連接字串](https://www.connectionstrings.com/mysql/)。 此第三方網站也會包含資料提供者和描述在此頁面上的連接參數的詳細資訊。

## <a name="see-also"></a>另請參閱
[選擇資料來源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[選擇目的地](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


