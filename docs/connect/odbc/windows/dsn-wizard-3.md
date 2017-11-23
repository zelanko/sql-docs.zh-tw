---
title: "資料來源精靈畫面 3 （適用於 SQL Server ODBC 驅動程式） |Microsoft 文件"
ms.custom: 
ms.date: 09/27/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a8803b1a18ce1a0987c9ebfcbd718345cfc3ef60
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="data-source-wizard-screen-3"></a>資料來源精靈畫面 3

指定預設資料庫、驅動程式所使用的各種 ANSI 選項及鏡像伺服器的名稱。

## <a name="options"></a>選項。

### <a name="change-the-default-database-to"></a>變更預設資料庫為

指定預設資料庫的名稱，以用於使用此資料來源所建立的任何連接。 清除此方塊時，連接會使用為該伺服器之登入 ID 所定義的預設資料庫。 選取此方塊時，方塊中所命名的資料庫會覆寫為該登入識別碼定義的預設資料庫。 如果**附加資料庫檔名**方塊具有主要檔案的名稱，主要檔案所說明的資料庫附加資料庫，使用指定的資料庫名稱為**預設資料庫變更至**方塊。

使用登入 ID 的預設資料庫比在 ODBC 資料來源中指定預設資料庫更有效。

### <a name="mirror-server"></a>鏡像伺服器

指定要鏡像處理之資料庫的容錯移轉夥伴名稱。 如果資料庫名稱不會顯示在**變更預設資料庫為** 方塊中或顯示的名稱是預設資料庫、**鏡像伺服器**會變成灰色。

(選擇性) 您可以指定鏡像伺服器的伺服器主體名稱 (SPN)。 鏡像伺服器的 SPN 會用於用戶端與伺服器之間的相互驗證。

### <a name="attach-database-filename"></a>附加資料庫檔名

為可附加的資料庫指定主要檔案的名稱。 此資料庫會附加並且當做資料來源的預設資料庫使用。 指定主要檔案的完整路徑及檔名。 中指定的資料庫名稱**變更預設資料庫為**方塊用做為附加的資料庫名稱。

### <a name="use-ansi-quoted-identifiers"></a>使用 ANSI 引號識別項

指定 QUOTED_IDENTIFIERS 會設定上的 ODBC driver for SQL Server 連線時。 選取此核取方塊時，SQL Server 會強制執行有關引號的 ANSI 規則。 雙引號僅可用於識別項，如資料行及資料表名稱。 字元字串必須以單引號括住：

```
SELECT "LastName"
FROM "Person.Contact"
WHERE "LastName" = 'O''Brien'
```

如果清除此核取方塊，則當使用引號識別項的應用程式 (如 Microsoft Excel 隨附的 Microsoft Query 公用程式) 利用引號識別項產生 SQL 陳述式時，就會發生錯誤。

### <a name="use-ansi-nulls-paddings-and-warnings"></a>使用 ANSI 空值、 留白和警告

指定 ANSI_NULLS、 ANSI_WARNINGS 及 ANSI_PADDINGS 選項會設定在 ODBC Driver for SQL Server 連接時。

當啟用 ANSI_NULLS 時，伺服器會強制執行關於 NULL 資料行比較的 ANSI 規則。 必須針對所有 NULL 比較使用 ANSI 語法 "IS NULL" 或 "IS NOT NULL"。 Transact-SQL 語法 "= NULL" 不受支援。

Ansi_warnings，SQL Server 會發出警告訊息，針對違反 ANSI 規則但未違反 TRANSACT-SQL 規則的條件。 此類錯誤包括執行 INSERT 或 UPDATE 陳述式時截斷資料，或在執行彙總函式期間產生 NULL 值。 

Ansi_padding 時，結尾的空格**varchar**值和結尾的零**varbinary**值不會自動修剪。

### <a name="application-intent"></a>應用程式意圖

宣告連接到伺服器時的應用程式工作負載類型。 可能的值為**ReadOnly**和**ReadWrite**。

### <a name="multi-subnet-failover"></a>多重子網路容錯移轉

如果您的應用程式連接至高可用性、 災害復原 （AlwaysOn 可用性群組） 可用性群組 (AG) 的不同子網路，請啟用**多重子網路容錯移轉。** 設定 ODBC Driver for SQL Server 來提供更快速偵測與 （目前） 使用中伺服器的連接。

### <a name="transparent-network-ip-resolution"></a>透明網路 IP 解析。

改變行為**多重子網路容錯移轉**以便進行容錯移轉期間更快的重新連線。 請參閱[使用透明網路 IP 解析](../../../connect/odbc/using-transparent-network-ip-resolution.md)如需詳細資訊。

### <a name="column-encryption"></a>資料行加密。

啟用自動解密和加密與加密資料行的資料傳輸[永遠加密](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)功能可在 SQL Server 2016 及更新版本。

### <a name="next"></a>下一個

繼續進行精靈的下一個畫面。

### <a name="back"></a>上一頁

傳回上一個精靈的螢幕。

## <a name="next-steps"></a>後續的步驟

[資料來源精靈螢幕 2](../../../connect/odbc/windows/dsn-wizard-2.md)

[資料來源精靈畫面 4](../../../connect/odbc/windows/dsn-wizard-4.md)
