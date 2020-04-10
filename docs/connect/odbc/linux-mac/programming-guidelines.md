---
title: 程式設計指導方針 (ODBC Driver for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/12/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: v-makouz
ms.author: v-daenge
ms.openlocfilehash: 9299e42d4e9defb5695716771a60ea2855729ee7
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80912374"
---
# <a name="programming-guidelines"></a>程式設計指導方針

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

macOS 和 Linux 上 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的程式設計功能以 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 中 ([SQL Server Native Client (ODBC)](https://go.microsoft.com/fwlink/?LinkID=134151)) 的 ODBC 為基礎。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 以 Windows Data Access Components ([ODBC 程式設計人員的參考](https://go.microsoft.com/fwlink/?LinkID=45250)) 中的 ODBC 為基礎。  

ODBC 應用程式可在納入 unixODBC 標頭 ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]、`/usr/local/include/msodbcsql.h`、`sql.h` 和 `sqlext.h`) 之後納入 `sqltypes.h`，藉以使用 Multiple Active Result Sets (MARS) 和其他 `sqlucode.h` 特定功能。 接著，請針對您要在 Windows ODBC 應用程式中使用的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 專屬項目，使用相同的符號名稱。

## <a name="available-features"></a>可用的功能  
在 macOS 和 Linux 上使用 ODBC 驅動程序時，您可參考 ODBC 之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 文件 ([SQL Server Native Client (ODBC)](https://go.microsoft.com/fwlink/?LinkID=134151)) 內的下列章節：  

-   [與 SQL Server 進行通訊 (ODBC)](https://msdn.microsoft.com/library/ms131692.aspx)  
-   [連線和查詢逾時支援](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
-   [資料指標](../../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
-   [日期/時間改善 (ODBC)](https://msdn.microsoft.com/library/bb677319.aspx)  
-   [執行查詢 (ODBC)](https://msdn.microsoft.com/library/ms131677.aspx)  
-   [處理錯誤與訊息](../../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
-   [Kerberos 驗證](../../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)  
-   [大型 CLR 使用者定義型別 (ODBC)](https://msdn.microsoft.com/library/bb677316.aspx)  
-   [執行交易 (ODBC) (分散式交易除外)](https://msdn.microsoft.com/library/ms131706.aspx)  
-   [處理結果 (ODBC)](https://msdn.microsoft.com/library/ms130812.aspx)  
-   [執行預存程序](../../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)
-   [疏鬆資料行支援 (ODBC)](https://msdn.microsoft.com/library/cc280357.aspx)
-   [SSL 加密](../../../relational-databases/native-client/features/using-encryption-without-validation.md)
-   [資料表值參數](https://docs.microsoft.com/sql/relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc)
-   [命令和資料 API 的 UTF-8 和 UTF-16](https://msdn.microsoft.com/library/ff878241.aspx)
-   [使用目錄函式](../../../relational-databases/native-client/odbc/using-catalog-functions.md)  

## <a name="unsupported-features"></a>不支援的功能

下列功能並未經確認可在 macOS 和 Linux 上此版本的 ODBC 驅動程式正確運作：

-   容錯移轉叢集連接
-   [透明網路 IP 解析](https://docs.microsoft.com/sql/connect/odbc/linux/using-transparent-network-ip-resolution) (在 ODBC Driver 17 以前)
-   [進階驅動程式追蹤](https://blogs.msdn.microsoft.com/mattn/2012/05/15/enabling-advanced-driver-tracing-for-the-sql-native-client-odbc-drivers/)

macOS 和 Linux 上此版本的 ODBC 驅動程式不提供下列功能： 

-   分散式交易 (不支援 SQL_ATTR_ENLIST_IN_DTC 屬性)  
-   資料庫鏡像  
-   FILESTREAM  
-   分析 ODBC 驅動程式效能 (相關討論請見 [SQLSetConnectAttr](https://go.microsoft.com/fwlink/?LinkId=234099))，以及下列和效能相關的連線屬性：  
    -   SQL_COPT_SS_PERF_DATA  
    -   SQL_COPT_SS_PERF_DATA_LOG  
    -   SQL_COPT_SS_PERF_DATA_LOG_NOW  
    -   SQL_COPT_SS_PERF_QUERY  
    -   SQL_COPT_SS_PERF_QUERY_INTERVAL  
    -   SQL_COPT_SS_PERF_QUERY_LOG  
-   SQLBrowseConnect (17.2 版之前)
-   C 間隔類型，如 SQL_C_INTERVAL_YEAR_TO_MONTH (相關文件請參閱[資料類型識別碼和描述項](https://msdn.microsoft.com/library/ms716351(VS.85).aspx))
-   SQLSetConnectAttr 函式之 SQL_ATTR_ODBC_CURSORS 屬性的 SQL_CUR_USE_ODBC 值。

## <a name="character-set-support"></a>字元集支援

若為 ODBC Driver 13 和 13.1，SQLCHAR 資料必須是 UTF-8。 不支援其他任何編碼。

若為 ODBC Driver 17，支援其中一種下列字元集/編碼的 SQLCHAR 資料：

> [!NOTE]  
> 由於 `iconv` 和 `musl` 之間的 `glibc` 差異，因此，Alpine Linux 不支援這其中許多地區設定。
>
> 如需詳細資訊，請參閱[與 glibc 的功能差異](https://wiki.musl-libc.org/functional-differences-from-glibc.html) \(英文\)。

|名稱|描述|
|-|-|
|UTF-8|Unicode|
|CP437|MS-DOS Latin US|
|CP850|MS-DOS Latin 1|
|CP874|Latin/Thai|
|CP932|日文，Shift-JIS|
|CP936|簡體中文，GBK|
|CP949|韓文，EUC-KR|
|CP950|繁體中文，Big5|
|CP1251|古斯拉夫文|
|CP1253|希臘文|
|CP1256|阿拉伯文|
|CP1257|波羅的語系|
|CP1258|越南文|
|ISO-8859-1 / CP1252|Latin-1|
|ISO-8859-2 / CP1250|Latin-2|
|ISO-8859-3|Latin-3|
|ISO-8859-4|Latin-4|
|ISO-8859-5|Latin/Cyrillic|
|ISO-8859-6|Latin/Arabic|
|ISO-8859-7|Latin/Greek|
|ISO-8859-8 / CP1255|Hebrew|
|ISO-8859-9 / CP1254|土耳其文|
|ISO-8859-13|Latin-7|
|ISO-8859-15|Latin-9|

連接時，驅動程式會偵測載入它的目前處理序地區設定。 如果使用上述編碼方式之一，驅動程式會針對 SQLCHAR (窄字元) 資料使用該編碼，否則它會預設為 UTF-8。 因為所有處理序預設都以 "C" 地區設定啟動 (因此導致驅動程式預設為 UTF-8)，如果應用程式需要使用上述編碼方式之一，它應該使用 **setlocale** 函式先適當地設定地區設定，然後才進行連線；藉由明確地指定所需的地區設定，或使用空字串，例如 `setlocale(LC_ALL, "")`，以使用環境的地區設定。

因此，在編碼為 UTF-8 的一般 Linux 或 Mac 環境中，從 13 或 13.1 升級而來的 ODBC Driver 17 使用者不會發現任何差異。 不過，透過 `setlocale()` 使用上述清單中非 UTF-8 編碼的應用程式，需要針對與驅動程式之間資料使用該編碼，而不是 UTF-8。

SQLWCHAR 資料必須是 UTF-16LE (Little Endian)。

使用 SQLBindParameter 繫結輸入參數時，如果指定了窄字元 SQL 類型，例如 SQL_VARCHAR，驅動程式會將所提供的資料從用戶端編碼轉換為預設 (通常為字碼頁 1252) [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 編碼。 針對輸出參數，驅動程式會從資料相關聯定序資訊中指定的編碼轉換為用戶端編碼。 不過，資料可能會遺失 --- 無法用目標編碼顯示的來源編碼字元，會轉換成問號 ('?')。

繫結輸入參數時，若要避免這種資料遺失，請指定 Unicode SQL 字元類型，例如 SQL_NVARCHAR。 在此情況下，驅動程式會從用戶端編碼轉換為 UTF-16，這可以呈現所有 Unicode 字元。 此外，伺服器上的目標資料行或參數也必須是 Unicode 類型 (**nchar**、**nvarchar**、**ntext**) 或具有定序/編碼的類型，可呈現原始來源資料的所有字元。 如需避免輸出參數的資料遺失，請指定 Unicode SQL 類型，以及 Unicode C 類型 (SQL_C_WCHAR)，讓驅動程式傳回 UTF-16 資料，或是窄 C 類型，並確保用戶端編碼可以呈現來源資料的所有字元 (UTF-8 一律可做到這點)。

如需定序和編碼的詳細資訊，請參閱[定序和 Unicode 支援](../../../relational-databases/collations/collation-and-unicode-support.md)。

Windows 與 Linux 和 macOS 上的數個 iconv 程式庫版本之間有一些編碼轉換差異。 字碼頁 1255 (希伯來文) 的文字資料中有一個字碼元素 (0xCA) 在轉換為 Unicode 時行為不相同。 在 Windows 中，此字元會轉換為 0x05BA 的 UTF-16 字碼元素。 在 libiconv 版本早於 1.15 的 macOS 和 Linux 上，它會轉換為 0x00CA。 在 iconv 程式庫不支援 Big5/CP950 2003 修訂 (名為`BIG5-2003`) 的 Linux 上，使用該修訂新增的字元不會正確地轉換。 在字碼頁 932 (日文，Shift-JIS)，字元如原本未定義於編碼標準中，解碼的結果也會不同。 比方說，位元組 0x80 在 Windows 上會轉換為 U+0080，但在 Linux 和 macOS 上可能會變成 U+30FB，視 iconv 版本而定。

在 ODBC 驅動程式 13 和 13.1 中，當 UTF-8 多位元組字元或 UTF-16 代理分在各個 SQLPutData 緩衝區時，會導致資料損毀。 對於最後不是部分字元編碼的串流 SQLPutData，請使用緩衝區。 ODBC Driver 17 已移除這項限制。

## <a name="openssl"></a><a name="bkmk-openssl"></a>OpenSSL
從 17.4 版開始，驅動程式會以動態方式載入 OpenSSL，使其可在具有 1.0 或 1.1 版的系統上執行，而不需個別的驅動程式檔案。 若有多個版本的 OpenSSL 存在，驅動程式將嘗試載入最新版本。 驅動程式目前支援 OpenSSL 1.0.x 和 1.1.x。

> [!NOTE]  
> 如果使用驅動程式 (或其中一個元件) 的應用程式會連結到或動態載入不同版本的 OpenSSL，可能就會發生衝突。 如果系統上有數個版本的 OpenSSL 存在，而且應用程式會加以使用，則強烈建議您特別小心地確認應用程式和驅動程式所載入的版本不相符，因為錯誤可能會損毀記憶體，因此不一定會以明顯或一致的方式表現出來。

## <a name="alpine-linux"></a><a name="bkmk-alpine"></a>Alpine Linux
撰寫本文時，MUSL 中的預設堆疊大小是 128K，這對於基本的 ODBC 驅動程式功能就已足夠，但根據應用程式的用途，超過此限制並不困難，尤其是從多個執行緒呼叫驅動程式時。 建議使用 `-Wl,-z,stack-size=<VALUE IN BYTES>` 來編譯 Alpine Linux 上的 ODBC 應用程式，以增加堆疊大小。 大部分 GLIBC 系統上的預設堆疊大小為 2MB (僅供參考)。

## <a name="additional-notes"></a>其他注意事項  

1.  您可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證和 **host,port** 建立專用管理員連接 (DAC)。 Sysadmin 角色的成員首先必須探索 DAC 通訊埠。 如需做法，請參閱[資料庫管理員的診斷連接](https://docs.microsoft.com/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators#dac-port)。 例如，如果 DAC 連接埠是 33000，您可透過下列方式以 `sqlcmd` 與其連線：  

    ```
    sqlcmd -U <user> -P <pwd> -S <host>,33000
    ```

    > [!NOTE]  
    > DAC 連線必須使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證。  
    
2.  如果陳述式屬性是透過 SQLSetConnectAttr 來傳遞的，則 UnixODBC 驅動程式對於所有的陳述式屬性都會傳回「無效的屬性/選項識別碼」。 在 Windows 上，當 SQLSetConnectAttr 收到陳述式屬性值時，會導致驅動程式在屬於連線控制代碼子系的所有作用中陳述式上設定值。  

3.  搭配高度多執行緒的應用程式使用驅動程式時，unixODBC 的控制代碼驗證可能會變成效能瓶頸。 在這種情況下，您可以使用 `--enable-fastvalidate` 選項來編譯 unixODBC，以獲得大幅提高的效能。 不過，請注意，這可能導致將無效控制代碼傳遞給 ODBC API 的應用程式損毀，而不會傳回 `SQL_INVALID_HANDLE` 錯誤。

## <a name="see-also"></a>另請參閱  
[常見問題集](../../../connect/odbc/linux-mac/frequently-asked-questions-faq-for-odbc-linux.md)

[此驅動程式版本的已知問題](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)

[版本資訊](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)
