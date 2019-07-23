---
title: 資料來源嚮導畫面 4 (ODBC Driver for SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 177888dd1034bb1edcb870db38b00bbc418cb261
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989462"
---
# <a name="data-source-wizard-screen-4"></a>資料來源精靈畫面 4

指定 SQL Server 訊息所使用的語言、字元集轉譯，以及 ODBC Driver for SQL Server 是否應該使用區域設定。 您也可以控制長期執行查詢及驅動程式統計資料設定的記錄。

## <a name="options"></a>選項。

### <a name="change-the-language-of-sql-server-system-messages-to"></a>變更 SQL Server 系統訊息的語言為

SQL Server 的每一個執行個體都可具有多組系統訊息，每一組都可使用不同的語言 (例如，英文、西班牙文、法文等)。 如果資料來源是針對具有多組系統訊息的伺服器而定義，則您可以指定您要用於系統訊息的語言。 在清單中，按一下語言。 如果在 SQL Server 上只安裝了一種語言，則此選項無法使用。

### <a name="use-strong-encryption-for-data"></a>使用高度加密資料

選取時，透過使用此 DSN 建立的連接所傳遞的資料將會加密。 預設會加密登入，即使清除該核取方塊亦然。

### <a name="trust-server-certificate"></a>信任伺服器憑證

只有在已啟用 [**對資料使用強式加密**] 時, 才適用此選項。 選取此選項時, 將不會驗證服務器的憑證是否具有伺服器的正確主機名稱, 並由受信任的憑證授權單位單位發行。 

### <a name="perform-translation-for-character-data"></a>為字元資料執行轉譯

選取此核取方塊時，ODBC Driver for SQL Server 會使用 Unicode 來轉換在用戶端電腦與 SQL Server 之間傳送的 ANSI 字串。 ODBC 驅動程式有時會在用戶端電腦上的 SQL Server 字碼頁與 Unicode 之間轉換。 若要執行此作業，SQL Server 所使用字碼頁必須是用戶端電腦上可用的其中一個字碼頁。

若清除此核取方塊，ANSI 字元字串中的延伸字元在用戶端應用程式與伺服器之間傳送時就不會進行任何轉譯。 如果用戶端電腦正在使用與 SQL Server 字碼頁不同的 ANSI 字碼頁 (ACP)，則 ANSI 字元字串中的擴充字元可能會被錯誤解譯。 如果用戶端電腦正在使用的 ACP 字碼頁與 SQL Server 所使用字碼頁相同，則擴充字元會被正確解譯。

### <a name="use-regional-settings-when-outputting-currency-numbers-dates-and-times"></a>當輸出流通貨幣、數字、日期和時間時，請使用地區設定

指定驅動程式使用用戶端電腦的區域設定，以格式化字元輸出字串中的貨幣、數字、日期及時間。 針對透過資料來源連接之使用者的 Windows 登入帳戶，驅動程式會使用預設區域設定。 請針對僅顯示資料的應用程式 (而非處理資料的應用程式) 選取此選項。

### <a name="save-long-running-queries-to-the-log-file"></a>將長時間執行的查詢儲存到記錄檔

指定驅動程式記錄查詢時間長於 [長查詢時間] 值的任何查詢。  長期執行查詢會記錄在指定的檔案中。 若要指定記錄檔，請在方塊中鍵入完整路徑和檔案名稱，或按一下 [瀏覽]，透過巡覽現有檔案目錄來選取記錄檔。 

### <a name="long-query-time-milliseconds"></a>長時間查詢的時間 (毫秒)

指定長期執行查詢記錄的臨界值 (以毫秒為單位)。 執行時間長於此毫秒數的任何查詢都會被記錄。

### <a name="log-odbc-driver-statistics-to-the-log-file"></a>記錄 ODBC 驅動程式統計資料至記錄檔

指定要記錄統計資料。 將統計資料記錄至指定檔案。 若要指定記錄檔，請在方塊中鍵入完整路徑和檔案名稱，或按一下 [瀏覽]，透過巡覽現有檔案目錄來選取記錄檔。 

統計資料記錄是以 Tab 分隔的檔案，可以在 Microsoft Excel 或其他任何支援以 Tab 分隔檔案的應用程式中進行分析。

### <a name="connect-retry-count"></a>連接重試計數

指定重試嘗試連接失敗的次數。

### <a name="connect-retry-interval-seconds"></a>連接重試間隔 (秒)

指定每個連接重試嘗試之間的秒數。 如需有關此作業和**連接重試計數**選項的詳細資訊, 請參閱[Windows ODBC 驅動程式中的連接恢復](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)功能。

### <a name="back"></a>上一頁

按一下此按鈕, 返回嚮導的上一頁。

### <a name="finish"></a>[完成]

如果在此畫面上指定的資訊已完成, 您可以按一下 **[完成]** 。 DSN 是使用在 wizard 的這個畫面上所指定的所有屬性來建立, 而且您有機會測試新建立的 DSN。

## <a name="next-steps"></a>後續步驟

[資料來源精靈畫面 3](../../../connect/odbc/windows/dsn-wizard-3.md)
