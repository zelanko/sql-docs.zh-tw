---
title: 程式設計指導方針 (ODBC Driver for SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 01/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fd77c85b089c0167306aeaad5c6d65a313e77624
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2018
ms.locfileid: "38983434"
---
# <a name="programming-guidelines"></a>程式設計指導方針

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

macOS 和 Linux 上 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 的程式設計功能以 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client 中 ([SQL Server Native Client (ODBC)](http://go.microsoft.com/fwlink/?LinkID=134151)) 的 ODBC 為基礎。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client 以 Windows Data Access Components ([ODBC 程式設計人員的參考](http://go.microsoft.com/fwlink/?LinkID=45250)) 中的 ODBC 為基礎。  

ODBC 應用程式可以使用多個作用中結果集 (MARS) 和其他[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]特定的功能，加`/usr/local/include/msodbcsql.h`之後 unixODBC 標頭 (`sql.h`， `sqlext.h`， `sqltypes.h`，和`sqlucode.h`)。 接著，請針對您要在 Windows ODBC 應用程式中使用的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 專屬項目，使用相同的符號名稱。

## <a name="available-features"></a>可用的功能  
在 macOS 和 Linux 上使用 ODBC 驅動程序時，您可參考 ODBC 之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client 文件 ([SQL Server Native Client (ODBC)](http://go.microsoft.com/fwlink/?LinkID=134151)) 內的下列章節：  

-   [與 SQL Server 進行通訊 (ODBC)](http://msdn.microsoft.com/library/ms131692.aspx)  
-   [連線和查詢逾時支援](http://msdn.microsoft.com/library/ms130822.aspx)  
-   [資料指標](http://msdn.microsoft.com/library/ms130794(SQL.110).aspx)  
-   [日期/時間改善 (ODBC)](http://msdn.microsoft.com/library/bb677319.aspx)  
-   [執行查詢 (ODBC)](http://msdn.microsoft.com/library/ms131677.aspx)  
-   [處理錯誤與訊息](http://msdn.microsoft.com/library/ms131289.aspx)  
-   [Kerberos 驗證](http://msdn.microsoft.com/library/cc280459.aspx)  
-   [大型 CLR 使用者定義型別 (ODBC)](http://msdn.microsoft.com/library/bb677316.aspx)  
-   [執行交易 (ODBC) (分散式交易除外)](http://msdn.microsoft.com/library/ms131706.aspx)  
-   [處理結果 (ODBC)](http://msdn.microsoft.com/library/ms130812.aspx)  
-   [執行預存程序](http://msdn.microsoft.com/library/ms131440.aspx)
-   [疏鬆資料行支援 (ODBC)](http://msdn.microsoft.com/library/cc280357.aspx)
-   [SSL 加密](http://msdn.microsoft.com/library/ms131691.aspx)
-   [資料表值參數](https://docs.microsoft.com/sql/relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc)
-   [命令和資料 API 的 UTF-8 和 UTF-16](http://msdn.microsoft.com/library/ff878241.aspx)
-   [使用目錄函式](http://msdn.microsoft.com/library/ms131490.aspx)  

## <a name="unsupported-features"></a>不支援的功能

在這一版的 ODBC 驅動程式中正確運作在 macOS 和 Linux 上尚未驗證下列功能：

-   容錯移轉叢集連線
-   [透明網路 IP 解析](https://docs.microsoft.com/sql/connect/odbc/linux/using-transparent-network-ip-resolution)（之前，ODBC Driver 17)
-   [進階的驅動程式追蹤](https://blogs.msdn.microsoft.com/mattn/2012/05/15/enabling-advanced-driver-tracing-for-the-sql-native-client-odbc-drivers/)

macOS 和 Linux 上此版本的 ODBC 驅動程式不提供下列功能： 

-   分散式交易 (不支援 SQL_ATTR_ENLIST_IN_DTC 屬性)  
-   資料庫鏡像  
-   FILESTREAM  
-   分析 ODBC 驅動程式效能 (相關討論請見 [SQLSetConnectAttr](http://go.microsoft.com/fwlink/?LinkId=234099))，以及下列和效能相關的連線屬性：  
    -   SQL_COPT_SS_PERF_DATA  
    -   SQL_COPT_SS_PERF_DATA_LOG  
    -   SQL_COPT_SS_PERF_DATA_LOG_NOW  
    -   SQL_COPT_SS_PERF_QUERY  
    -   SQL_COPT_SS_PERF_QUERY_INTERVAL  
    -   SQL_COPT_SS_PERF_QUERY_LOG  
-   SQLBrowseConnect  
-   C 間隔類型，如 SQL_C_INTERVAL_YEAR_TO_MONTH (相關文件請參閱[資料類型識別碼和描述項](http://msdn.microsoft.com/library/ms716351(VS.85).aspx))
-   SQLSetConnectAttr 函式之 SQL_ATTR_ODBC_CURSORS 屬性的 SQL_CUR_USE_ODBC 值。

## <a name="character-set-support"></a>字元集支援

如需 ODBC Driver 13 和 13.1，SQLCHAR 資料必須是 utf-8。 支援其他編碼方式。

ODBC Driver 17，支援其中一種下列字元的集合/編碼的 SQLCHAR 資料：

|[屬性]|Description|
|-|-|
|UTF-8|Unicode|
|CP437|MS-DOS Latin 美國|
|CP850|MS-DOS 拉丁文 1|
|CP874|拉丁文/泰文|
|CP932|日文，Shift-JIS|
|CP936|簡體中文，GBK|
|CP949|韓文，EUC-KR|
|CP950|繁體中文，Big5|
|CP1251|古斯拉夫文|
|CP1253|希臘文|
|CP1256|阿拉伯文|
|CP1257|波羅的語系|
|CP1258|越南文|
|ISO-8859-1 / CP1252|拉丁文 1|
|ISO-8859-2 / CP1250|拉丁文-2|
|ISO-8859-3|拉丁文 3|
|ISO-8859-4|拉丁文-4|
|ISO-8859-5|拉丁文/斯拉夫文|
|ISO-8859-6|拉丁文/阿拉伯文|
|ISO-8859-7|拉丁文/希臘文|
|ISO-8859-8 / CP1255|Hebrew|
|ISO-8859-9 / CP1254|土耳其文|
|ISO-8859-13|拉丁文-7|
|ISO 8859-15|拉丁文 9|

連接時，驅動程式會偵測目前的地區設定的程序中載入。 如果使用上述的編碼方式的其中一個，驅動程式會使用該編碼 SQLCHAR （窄字元） 的資料;否則，它會預設為 utf-8。 因為所有處理程序，依預設，在"C"地區設定中啟動 （且因此導致 utf-8 預設驅動程式），如果應用程式需要使用上述的編碼方式的其中一個，它應該使用**setlocale**之前適當地設定的地區設定的函式連線;藉由明確地指定所需的地區設定，或使用空字串，例如`setlocale(LC_ALL, "")`使用環境的地區設定。

因此，在一般 Linux 或 Mac 環境中，編碼為 utf-8，ODBC Driver 17 升級從 13 或 13.1 的使用者不會發現任何差異。 不過，應用程式，使用非 utf-8 編碼方式在上述清單中透過`setlocale()`需要使用該資料之間的驅動程式，而不是 utf-8 編碼。

SQLWCHAR 資料必須是 UTF-16LE (Little Endian)。

在窄字元 SQL 類型，例如 SQL_VARCHAR 已指定，繫結與 SQLBindParameter 等的輸入的參數，驅動程式會將所提供的資料轉換為預設值 （通常為字碼頁 1252年） 編碼的用戶端從[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]編碼方式。 當做輸出參數，驅動程式會從與要編碼的用戶端的資料相關聯的定序資訊中指定的編碼方式轉換。 不過，可能會遺失資料---無法顯示目標編碼中的 來源編碼字元會將轉換成問號 ('？ ')。

若要避免這種資料遺失，繫結輸入的參數時，指定 Unicode SQL 字元類型，例如 SQL_NVARCHAR。 在此情況下，驅動程式會從用戶端的編碼為 utf-16，可以代表所有的 Unicode 字元轉換。 此外，目標資料行或參數在伺服器上的也必須是 Unicode 類型 (**nchar**， **nvarchar**， **ntext**) 或其中一個使用定序/編碼方式，可以代表原始來源資料的所有的字元。 避免資料遺失與輸出參數，指定 Unicode SQL 型別和 Unicode C 類型 (SQL_C_WCHAR)，造成驅動程式傳回為 utf-16; 的資料或窄的 C 類型，並確保用戶端的編碼方式可表示來源資料 （這是永遠使用 utf-8。） 的所有字元

如需有關定序和編碼方式的詳細資訊，請參閱 < [Collation and Unicode Support](../../../relational-databases/collations/collation-and-unicode-support.md)。

有一些 Windows 與 Linux 和 macOS 上的 iconv 程式庫的數個版本之間的編碼轉換差異。 文字資料的字碼頁 1255年 （希伯來文） 有一個字碼 (元素 0xCA) 在轉換成 Unicode 時的行為不相同。 在 Windows 中，此字元會將 0x05BA 的 utf-16 字碼指標。 MacOS 與 Linux 上使用早於 1.15 libiconv 版本，它會將 0x00CA。 在 Linux 上使用不支援 Big5/CP950 2003 修訂的 iconv 程式庫 (名為`BIG5-2003`)，加上該修訂的字元不會正確地轉換。 在字碼頁 932 （日文，Shift JIS），不是原本定義編碼標準中的字元解碼的結果也不同。 比方說，0x80 的位元組將轉換成 u+0080，在 Windows 上，但可能會變得 U + 30FB Linux 和 macOS，視 iconv 版本而定。

在 ODBC 驅動程式 13 和 13.1 中，當 UTF-8 多位元組字元或 UTF-16 代理分在各個 SQLPutData 緩衝區時，會導致資料損毀。 對於最後不是部分字元編碼的串流 SQLPutData，請使用緩衝區。 使用 ODBC Driver 17 已移除這項限制。

## <a name="additional-notes"></a>其他注意事項  

1.  您可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 驗證和 **host,port** 建立專用管理員連接 (DAC)。 Sysadmin 角色的成員首先必須探索 DAC 通訊埠。 請參閱[適用於資料庫管理員的診斷連線](https://docs.microsoft.com/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators#dac-port)來探索如何。 例如，如果 DAC 連接埠是 33000，您可透過下列方式以 `sqlcmd` 與其連線：  

    ```
    sqlcmd –U <user> -P <pwd> -S <host>,33000
    ```

    > [!NOTE]  
    > DAC 連線必須使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 驗證。  
    
2.  如果陳述式屬性是透過 SQLSetConnectAttr 來傳遞的，則 UnixODBC 驅動程式對於所有的陳述式屬性都會傳回「無效的屬性/選項識別碼」。 在 Windows 上，當 SQLSetConnectAttr 收到陳述式屬性值時，會導致驅動程式在屬於連線控制代碼子系的所有作用中陳述式上設定值。  

## <a name="see-also"></a>另請參閱  
[常見問題集](../../../connect/odbc/linux-mac/frequently-asked-questions-faq-for-odbc-linux.md)

[此驅動程式版本的已知問題](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)

[版本資訊](../../../connect/odbc/linux-mac/release-notes.md)
