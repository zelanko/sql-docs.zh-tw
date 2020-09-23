---
description: 資料來源精靈畫面 3 (ODBC Driver for SQL Server)
title: 資料來源精靈畫面 3 (ODBC Driver for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 48b65f57ac4a47a372ff82db4bc92f5ee631ea36
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462193"
---
# <a name="data-source-wizard-screen-3"></a>資料來源精靈畫面 3

指定預設資料庫、驅動程式所使用的各種 ANSI 選項及鏡像伺服器的名稱。

## <a name="options"></a>選項

### <a name="change-the-default-database-to"></a>變更預設資料庫為

指定預設資料庫的名稱，以用於使用此資料來源所建立的任何連接。 清除此方塊時，連接會使用為該伺服器之登入 ID 所定義的預設資料庫。 選取此方塊時，方塊中所命名的資料庫會覆寫為該登入識別碼定義的預設資料庫。 如果 [附加資料庫檔案名稱] 方塊具有主要檔案的名稱，則主要檔案所描述之資料庫會附加為使用 [變更預設資料庫為] 方塊中所指定資料庫名稱的資料庫。********

使用登入 ID 的預設資料庫比在 ODBC 資料來源中指定預設資料庫更有效。

### <a name="mirror-server"></a>鏡像伺服器

指定要鏡像處理之資料庫的容錯移轉夥伴名稱。 如果資料庫名稱未顯示在 [變更預設資料庫為] 方塊中，或顯示的名稱為預設資料庫，則 [鏡像伺服器] 會變成灰色。********

(選擇性) 您可以指定鏡像伺服器的伺服器主體名稱 (SPN)。 鏡像伺服器的 SPN 會用於用戶端與伺服器之間的相互驗證。

### <a name="attach-database-filename"></a>附加資料庫檔案名稱

為可附加的資料庫指定主要檔案的名稱。 此資料庫會附加並且當做資料來源的預設資料庫使用。 指定主要檔案的完整路徑及檔名。 [變更預設資料庫為] 方塊中所指定資料庫名稱會作為附加資料庫的名稱使用。****

### <a name="use-ansi-quoted-identifiers"></a>使用 ANSI 引號識別項

指定在 ODBC Driver for SQL Server 連接時，啟用 QUOTED_IDENTIFIERS。 選取此核取方塊時，SQL Server 會強制執行有關引號的 ANSI 規則。 雙引號僅可用於識別項，如資料行及資料表名稱。 字元字串必須以單引號括住：

```
SELECT "LastName"
FROM "Person.Contact"
WHERE "LastName" = 'O''Brien'
```

如果清除此核取方塊，則當使用引號識別項的應用程式 (如 Microsoft Excel 隨附的 Microsoft Query 公用程式) 利用引號識別項產生 SQL 陳述式時，就會發生錯誤。

### <a name="use-ansi-nulls-paddings-and-warnings"></a>使用 ANSI 空值、填補和警告

指定在 ODBC Driver for SQL Server 連接時，啟用 ANSI_NULLS、ANSI_WARNINGS 及 ANSI_PADDINGS 選項。

當啟用 ANSI_NULLS 時，伺服器會強制執行關於 NULL 資料行比較的 ANSI 規則。 必須針對所有 NULL 比較使用 ANSI 語法 "IS NULL" 或 "IS NOT NULL"。 Transact-SQL 語法 "= NULL" 不受支援。

當啟用 ANSI_WARNINGS 時，SQL Server 會針對違反 ANSI 規則但未違反 Transact-SQL 規則的情況，發出警告訊息。 此類錯誤包括執行 INSERT 或 UPDATE 陳述式時截斷資料，或在執行彙總函式期間產生 NULL 值。 

當啟用 ANSI_PADDING 時，就不會自動修剪 **varchar** 值結尾的空格，以及 **varbinary** 值結尾的零。

### <a name="application-intent"></a>應用程式意圖

宣告連接到伺服器時的應用程式工作負載類型。 可能的值為 **ReadOnly** 和 **ReadWrite**。

### <a name="multi-subnet-failover"></a>多重子網路容錯移轉

如果您的應用程式要連線到不同子網路上的高可用性、災害復原 (AlwaysOn 可用性群組) 可用性群組 (AG)，則會啟用 [多重子網路容錯移轉]****。 會設定 ODBC Driver for SQL Server，以提供對 (目前) 使用中伺服器更快速的偵測與連接。

### <a name="transparent-network-ip-resolution"></a>透明網路 IP 解析。

改變 [多重子網路容錯移轉]**** 的行為，以允許在容錯移轉期間更快速地重新連線。 如需詳細資訊，請參閱[使用透明網路 IP 解析](../../../connect/odbc/using-transparent-network-ip-resolution.md)。

### <a name="column-encryption"></a>資料行加密。

可讓您對使用 SQL Server 2016 和更新版本中提供的 [Always Encrypted](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) 功能加密的資料行，自動解密和加密在其中傳輸的資料。

### <a name="use-fmtonly-metadata-discovery"></a>使用 FMTONLY 中繼資料探索：

連線到 SQL Server 2012 或更新版本時，請使用舊版的 SET FMTONLY 中繼資料探索方法。 只有在使用 [sp_describe_first_result_set](../../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) 支援的查詢 (例如，包含暫存資料表的查詢) 時，才啟用此選項。 

### <a name="next"></a>下一個

繼續前往精靈的下一個畫面。

### <a name="back"></a>上一步

返回精靈的上一個畫面。

## <a name="next-steps"></a>後續步驟

[資料來源精靈畫面 2](../../../connect/odbc/windows/dsn-wizard-2.md)

[資料來源精靈畫面 4](../../../connect/odbc/windows/dsn-wizard-4.md)
