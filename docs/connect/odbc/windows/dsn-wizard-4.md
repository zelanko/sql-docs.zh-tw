---
title: "資料來源精靈畫面 4 (ODBC Driver for SQL Server) |Microsoft 文件"
ms.custom: 
ms.date: 09/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: d3ba6607f717299bdeb60b649a8c6a1838ab0d17
ms.contentlocale: zh-tw
ms.lasthandoff: 10/06/2017

---
# <a name="data-source-wizard-screen-4"></a>資料來源精靈畫面 4

指定要用於 SQL Server 訊息的語言、 字元集轉譯，以及 ODBC driver for SQL Server 是否應使用的地區設定。 您也可以控制長期執行查詢及驅動程式統計資料設定的記錄。

## <a name="options"></a>選項。

### <a name="change-the-language-of-sql-server-system-messages-to"></a>變更 SQL Server 系統訊息的語言為

每個 SQL Server 執行個體可以具有多組系統訊息，每一組不同的語言 （例如，英文、 西班牙文、 法文等）。 如果資料來源是針對具有多組系統訊息的伺服器而定義，則您可以指定您要用於系統訊息的語言。 在清單中，按一下語言。 如果只有一種語言安裝 SQL Server 上，則無法使用此選項。

### <a name="use-strong-encryption-for-data"></a>使用高度加密資料

選取時，透過使用此 DSN 建立的連接所傳遞的資料將會加密。 預設會加密登入，即使清除該核取方塊亦然。

### <a name="trust-server-certificate"></a>信任伺服器憑證

時，此選項時才適用**使用高度加密資料**已啟用。 選取時，伺服器的憑證會驗證伺服器的正確的主機名稱，然後再由受信任的憑證授權單位發出。 

### <a name="perform-translation-for-character-data"></a>為字元資料執行轉譯

選取此核取方塊時，ODBC driver for SQL Server 會將使用 Unicode 用戶端電腦與 SQL Server 之間傳送的 ANSI 字串轉換。 ODBC 驅動程式有時的 SQL Server 字碼頁和 Unicode 之間轉換，用戶端電腦上。 這需要 SQL Server 所使用的字碼頁是其中一種用戶端電腦上可用的字碼頁。

若清除此核取方塊，ANSI 字元字串中的延伸字元在用戶端應用程式與伺服器之間傳送時就不會進行任何轉譯。 如果用戶端電腦會使用 ANSI 字碼頁 (ACP) SQL Server 字碼頁不同，可能會被誤解 ANSI 字元字串中的擴充的字元。 如果用戶端電腦正在使用相同的字碼頁，SQL Server 使用的 acp，擴充的字元會正確解譯。

### <a name="use-regional-settings-when-outputting-currency-numbers-dates-and-times"></a>當輸出流通貨幣、數字、日期和時間時，請使用地區設定

指定驅動程式使用用戶端電腦的區域設定，以格式化字元輸出字串中的貨幣、數字、日期及時間。 針對透過資料來源連接之使用者的 Windows 登入帳戶，驅動程式會使用預設區域設定。 請針對僅顯示資料的應用程式 (而非處理資料的應用程式) 選取此選項。

### <a name="save-long-running-queries-to-the-log-file"></a>將長時間執行的查詢儲存到記錄檔

指定驅動程式記錄所花費的時間比任何查詢**長時間查詢的時間**值。 長期執行查詢會記錄在指定的檔案中。 若要指定記錄檔，請在方塊中，輸入完整路徑和檔案名稱，或按一下**瀏覽**來瀏覽現有檔案目錄來選取記錄檔。

### <a name="long-query-time-milliseconds"></a>長時間查詢的時間 (毫秒)

指定長期執行查詢記錄的臨界值 (以毫秒為單位)。 執行時間長於此毫秒數的任何查詢都會被記錄。

### <a name="log-odbc-driver-statistics-to-the-log-file"></a>記錄 ODBC 驅動程式統計資料至記錄檔

指定要記錄統計資料。 將統計資料記錄至指定檔案。 若要指定記錄檔，請在方塊中輸入完整路徑和檔案名稱，或按一下**瀏覽**來瀏覽現有檔案目錄來選取記錄檔。

統計資料記錄是以 Tab 分隔的檔案，可以在 Microsoft Excel 或其他任何支援以 Tab 分隔檔案的應用程式中進行分析。

### <a name="connect-retry-count"></a>連接重試計數

指定重試一次連線嘗試失敗次數。

### <a name="connect-retry-interval-seconds"></a>連接重試間隔 （秒）

指定每個連接重試嘗試之間的秒的數。 如需有關這個操作和**連接重試計數**選項，請參閱[Connection Resiliency in the Windows ODBC Driver](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)。

### <a name="back"></a>上一頁

按一下此按鈕以返回精靈的上一頁。

### <a name="finish"></a>完成

如果在這個畫面上指定的資訊已完成，您可以按一下**完成**。 DSN 會使用這和在精靈的其他螢幕上指定的所有屬性所建立，您會獲得一個機會來測試新建立的資料來源名稱。

## <a name="next-steps"></a>後續的步驟

[資料來源精靈畫面 3](../../../connect/odbc/windows/dsn-wizard-3.md)

