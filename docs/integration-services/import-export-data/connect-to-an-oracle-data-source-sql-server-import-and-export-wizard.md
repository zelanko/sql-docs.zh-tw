---
title: "連接到 Oracle 資料來源 （SQL Server 匯入和匯出精靈） |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
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
ms.assetid: b0bd1f5a-34dd-4be3-9ac8-f9f87727781b
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e589e7f7a0262d258342bf887ec84c57d57dc978
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-an-oracle-data-source-sql-server-import-and-export-wizard"></a>連接到 Oracle 資料來源 （SQL Server 匯入和匯出精靈）
本主題說明如何連接到**Oracle**資料來源從**選擇資料來源**或**選擇目的地**SQL Server 匯入和匯出精靈 頁面。 有數個可讓您連接到 Oracle 資料提供者。

> [!IMPORTANT]
> 詳細的需求和必要條件連接到 Oracle 資料庫等已超出 Microsoft 本文的範圍。 本文假設您已安裝 Oracle 用戶端軟體，而且，您可以已成功連接到目標 Oracle 資料庫。 如需詳細資訊，請參閱 Oracle 資料庫管理員或 Oracle 文件集。

## <a name="connect-to-oracle-with-the-net-framework-data-provider-for-oracle"></a>連接到 Oracle 的.Net Framework Data Provider for Oracle
選取後**.NET Framework Data Provider for Oracle**上**選擇資料來源**或**選擇目的地**頁面在精靈的頁面會顯示群組的提供者的選項清單。 其中有許多惡意的名稱和不熟悉的設定。 幸運的是，您只需要提供兩個或三項資訊。 您可以忽略其他設定的預設值。

> [!NOTE]
> Oracle 為您的來源或目的地連接選項，此資料提供者都是相同的。 也就是您所看到的選項會同時針對相同**選擇資料來源**和**選擇目的地**精靈頁面。

|所需的資訊|.Net framework Data Provider for Oracle 屬性|
|---|---|
|伺服器名稱|**資料來源**|
|驗證 （登入） 資訊|**使用者識別碼**和**密碼**; 或者，**整合式安全性**|

您不需要輸入中的連接字串**ConnectionString**清單的欄位。 Oracle 伺服器名稱輸入個別的值之後 (**資料來源**)，並登入資訊，此精靈將組合從個別的屬性和其值的連接字串。 

![使用.NET 提供者連接到 Oracle](../../integration-services/import-export-data/media/connect-to-oracle-with-net-provider.jpg)

## <a name="connect-to-oracle-with-the-microsoft-odbc-driver-for-oracle"></a>Oracle 連接到 Oracle 的 Microsoft ODBC 驅動程式
ODBC 驅動程式未列在下拉式清單中的資料來源。 若要連接的 ODBC 驅動程式，一開始選取**.NET Framework Data Provider for ODBC**做為資料來源上**選擇資料來源**或**選擇目的地**頁面。 此提供者做為包裝函式，ODBC 驅動程式。

以下是您選取.NET Framework Data Provider for ODBC 之後，立即會看到泛用螢幕。

![連接到 Oracle 使用 ODBC 之前](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-odbc-driver-for-oracle"></a>選項來指定 （oracle 的 ODBC 驅動程式）

> [!NOTE]
> Oracle 為您的來源或目的地，此資料提供者和 ODBC 驅動程式的連接選項都相同。 也就是您所看到的選項會同時針對相同**選擇資料來源**和**選擇目的地**精靈頁面。

若要連接到 Oracle Oracle 的 ODBC 驅動程式，組合連接字串，其中包含下列設定，以及它們的值。 完整的連線字串的格式緊接在後面設定的清單。

> [!TIP]
> 取得說明組裝正確的連接字串。 或者，而不是提供的連接字串，提供現有的資料來源名稱 （資料來源名稱），或另外新建一個。 如需這些選項的詳細資訊，請參閱[連接到 ODBC 資料來源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。

**驅動程式**  
ODBC 驅動程式名稱**Oracle 的 Microsoft ODBC**。

**Server**  
在 Oracle 伺服器名稱。 

**Uid**和**Pwd**   
使用者識別碼和密碼來連接。

### <a name="connection-string-format"></a>連接字串格式
以下是一般連接字串的格式。

    ```
    Driver={Microsoft ODBC for Oracle};Server=myServerAddress;Uid=myUsername;Pwd=myPassword;
    ```

### <a name="enter-the-connection-string"></a>輸入連接字串
輸入中的連接字串**ConnectionString**欄位，或輸入中的 DSN 名稱**Dsn**欄位上**選擇資料來源**或**選擇目的地**頁面。 您輸入的連接字串之後，精靈會剖析字串，並會顯示個別的屬性及其值清單中。

以下是您輸入的連接字串之後，請參閱螢幕。

![連接到 Oracle 使用 ODBC](../../integration-services/import-export-data/media/connect-to-oracle-with-odbc.jpg)

## <a name="whats-my-oracle-server-name"></a>我的 Oracle 伺服器名稱是什麼？
執行下列查詢來取得 Oracle 伺服器名稱的其中一個。

`SELECT host_name FROM v$instance`

或

`SELECT sys_context('USERENV','SERVER_HOST') FROM dual`

## <a name="other-data-providers-and-more-info"></a>其他資料提供者和其他資訊
如需如何連接到 Oracle 與此處未列出的資料提供者資訊，請參閱[Oracle 連接字串](https://www.connectionstrings.com/oracle/)。 此第三方網站也會包含資料提供者和描述在此頁面上的連接參數的詳細資訊。

## <a name="see-also"></a>另請參閱
[選擇資料來源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[選擇目的地](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


