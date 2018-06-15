---
title: 程式設計指導方針 (ODBC Driver for SQL Server) |Microsoft 文件
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
ms.openlocfilehash: 68a7b720ab2ab9a4280cc6d8a22a37cf0cad0f5d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32853203"
---
# <a name="programming-guidelines"></a>程式設計指導方針

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

程式設計功能[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] macOS 和 Linux 為基礎中的 ODBC[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]原生用戶端 ([SQL Server Native Client (ODBC)](http://go.microsoft.com/fwlink/?LinkID=134151))。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 原生用戶端以 Windows Data Access Components 中的 ODBC 為基礎 ([ODBC 程式設計人員參考](http://go.microsoft.com/fwlink/?LinkID=45250))。  

ODBC 應用程式可以使用 Multiple Active Result Sets (MARS) 和其他[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]所包括的特定功能`/usr/local/include/msodbcsql.h`之後 unixODBC 標頭 (`sql.h`， `sqlext.h`， `sqltypes.h`，和`sqlucode.h`)。 然後使用相同的符號名稱[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]-Windows ODBC 應用程式會使用您的特定項目。

## <a name="available-features"></a>可用的功能  
下面各節從[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]Native Client ODBC 的文件 ([SQL Server Native Client (ODBC)](http://go.microsoft.com/fwlink/?LinkID=134151)) 時使用 macOS 和 Linux 上的 ODBC 驅動程式都是有效：  

-   [與 SQL Server 進行通訊 (ODBC)](http://msdn.microsoft.com/library/ms131692.aspx)  
-   [連接和查詢逾時支援](http://msdn.microsoft.com/library/ms130822.aspx)  
-   [資料指標](http://msdn.microsoft.com/library/ms130794(SQL.110).aspx)  
-   [日期/時間改善 (ODBC)](http://msdn.microsoft.com/library/bb677319.aspx)  
-   [執行查詢 (ODBC)](http://msdn.microsoft.com/library/ms131677.aspx)  
-   [處理錯誤與訊息](http://msdn.microsoft.com/library/ms131289.aspx)  
-   [Kerberos 驗證](http://msdn.microsoft.com/library/cc280459.aspx)  
-   [大型 CLR 使用者定義型別 (ODBC)](http://msdn.microsoft.com/library/bb677316.aspx)  
-   [執行交易 (ODBC) （分散式交易除外）](http://msdn.microsoft.com/library/ms131706.aspx)  
-   [處理結果 (ODBC)](http://msdn.microsoft.com/library/ms130812.aspx)  
-   [執行預存程序](http://msdn.microsoft.com/library/ms131440.aspx)
-   [疏鬆資料行支援 (ODBC)](http://msdn.microsoft.com/library/cc280357.aspx)
-   [SSL 加密](http://msdn.microsoft.com/library/ms131691.aspx)
-   [資料表值的參數](https://docs.microsoft.com/en-us/sql/relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc)
-   [Utf-8 和 utf-16 命令和資料 api](http://msdn.microsoft.com/library/ff878241.aspx)
-   [使用目錄函式](http://msdn.microsoft.com/library/ms131490.aspx)  

## <a name="unsupported-features"></a>不支援的功能

在這一版的 ODBC 驅動程式正常運作 macOS 和 Linux 上尚未驗證下列功能：

-   容錯移轉叢集連線
-   [透明網路 IP 解析](https://docs.microsoft.com/en-us/sql/connect/odbc/linux/using-transparent-network-ip-resolution)（之前 ODBC 驅動程式 17）
-   [進階的驅動程式的追蹤](https://blogs.msdn.microsoft.com/mattn/2012/05/15/enabling-advanced-driver-tracing-for-the-sql-native-client-odbc-drivers/)

不在 macOS 和 Linux 上的 ODBC 驅動程式的此版本中提供下列功能： 

-   分散式交易 （不支援 SQL_ATTR_ENLIST_IN_DTC 屬性）  
-   資料庫鏡像  
-   FILESTREAM  
-   分析 ODBC 驅動程式效能，討論[SQLSetConnectAttr](http://go.microsoft.com/fwlink/?LinkId=234099)，和下列效能相關連接屬性：  
    -   SQL_COPT_SS_PERF_DATA  
    -   SQL_COPT_SS_PERF_DATA_LOG  
    -   SQL_COPT_SS_PERF_DATA_LOG_NOW  
    -   SQL_COPT_SS_PERF_QUERY  
    -   SQL_COPT_SS_PERF_QUERY_INTERVAL  
    -   SQL_COPT_SS_PERF_QUERY_LOG  
-   SQLBrowseConnect  
-   C 間隔類型，例如 SQL_C_INTERVAL_YEAR_TO_MONTH (記載於[資料類型識別碼和描述元](http://msdn.microsoft.com/library/ms716351(VS.85).aspx))
-   SQLSetConnectAttr 函數之 SQL_ATTR_ODBC_CURSORS 屬性的 SQL_CUR_USE_ODBC 值。

## <a name="character-set-support"></a>字元設定支援

如需 ODBC Driver 13 和 13.1，SQLCHAR 資料必須是 utf-8。 不支援任何其他編碼方式。

ODBC 驅動程式 17，支援其中一種下列字元組/編碼 SQLCHAR 資料：

|名稱|Description|
|-|-|
|UTF-8|Unicode|
|CP437|MS-DOS 拉丁美國|
|CP850|MS-DOS 拉丁文 1|
|CP874|拉丁文/泰文|
|CP932|日文 Shift JIS|
|CP936|簡體中文 （gbk）|
|CP949|EUC-KR 韓文|
|CP950|繁體中文 Big5|
|CP1251|古斯拉夫文|
|CP1253|希臘文|
|CP1256|阿拉伯文|
|CP1257|波羅的語系|
|CP1258|越南文|
|ISO-8859-1 / CP1252|拉丁文 1|
|ISO-8859-2 / CP1250|拉丁文 2|
|ISO-8859-3|拉丁文 3|
|ISO-8859-4|拉丁文 4|
|ISO-8859-5|拉丁文/斯拉夫文|
|ISO-8859-6|拉丁文/阿拉伯文|
|ISO-8859-7|拉丁文/希臘文|
|ISO-8859-8 / CP1255|Hebrew|
|ISO-8859-9 / CP1254|土耳其文|
|ISO-8859-13|拉丁文 7|
|ISO-8859-15|拉丁文 9|

連接時，驅動程式會偵測處理程序中載入的目前地區設定。 如果它使用上述的編碼方式的其中一個，驅動程式會使用該編碼 SQLCHAR （窄字元） 的資料。否則，它會預設為 utf-8。 因為所有處理程序啟動"C"地區設定中的預設值 （並因此造成驅動程式新增至預設為 utf-8），如果應用程式需要使用上述的編碼方式的其中一個，則應該使用**setlocale**之前適當地設定的地區設定的函式連線;藉由明確地指定想要的地區設定，或使用空字串，例如`setlocale(LC_ALL, "")`使用地區設定的環境。

因此，一般 Linux 或 Mac 環境所在的編碼方式為 utf-8 中的 ODBC 驅動程式 17 從 13 或升級 13.1 使用者不會發現任何差異。 不過，應用程式，使用非 utf-8 編碼方式在上述清單中透過`setlocale()`需要使用該編碼資料，而不是 utf-8 的驅動程式。

SQLWCHAR 資料必須是 UTF-16LE (Little Endian)。

繫結時輸入的參數與 SQLBindParameter，如果窄字元 SQL 類型，例如指定 SQL_VARCHAR，驅動程式會將所提供的資料轉換為預設值 （通常為字碼頁 1252年） 編碼的用戶端從[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]編碼方式。 輸出參數的驅動程式會從要編碼的用戶端的資料相關聯的定序資訊中指定的編碼方式轉換。 不過，可能會遺失資料---無法顯示在目標編碼中的 來源編碼字元會將轉換成問號 ('？ ')。

若要避免這種資料遺失，繫結輸入的參數時，指定 Unicode SQL 字元類型，例如 SQL_NVARCHAR。 在此情況下，驅動程式會從用戶端編碼為 utf-16，這可能表示所有 Unicode 字元轉換。 此外，目標資料行或在伺服器上的參數也必須可以是 Unicode 類型 (**nchar**， **nvarchar**， **ntext**) 或另一個定序/編碼為，其中可以表示原始來源資料的所有的字元。 為避免資料遺失，使用 output 參數，指定 Unicode SQL 型別，並可以是 Unicode C 類型 (SQL_C_WCHAR)，造成驅動程式來傳回資料當做 utf-16;或半形的 C 類型，並確定編碼用戶端可以代表所有字元的來源資料 （這是永遠使用 utf-8 可能）。

如需有關定序和編碼方式的詳細資訊，請參閱[Collation and Unicode Support](../../../relational-databases/collations/collation-and-unicode-support.md)。

有一些 Windows 與 Linux 及 macOS 上的 iconv 程式庫的數個版本之間的編碼轉換差異。 文字資料的字碼頁 1255年 （希伯來文） 有一個字碼元素 0xca ()，在轉換成 Unicode 時的行為方式。 在 Windows 中，此字元會將 0x05BA 的 utf-16 字碼指標。 在 macOS 和 libiconv 版本早於 1.15 Linux，會將轉換成 0x00CA。 On Linux 不支援 Big5/CP950 2003 修訂的 iconv 程式庫 (名為`BIG5-2003`)，加上該修訂的字元不會正確轉換。 在字碼頁 932 （日文、 Shift JIS），不是原本定義編碼標準的字元解碼的結果也各不相同。 比方說，0x80 的位元組將轉換為 U + 0080 Windows 上，但可能會變成 U + 30FB Linux 及 macOS，視 iconv 版本而定。

在 ODBC Driver 13 和 13.1，當 utf-8 多位元組字元或 utf-16 surrogate SQLPutData 緩衝區間分散，分割會導致資料損毀。 對於最後不是部分字元編碼的串流 SQLPutData，請使用緩衝區。 已移除這項限制與 ODBC 驅動程式 17。

## <a name="additional-notes"></a>其他注意事項  

1.  您可以進行專用的管理員連接 (DAC) 使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]驗證和**主機、 連接埠**。 Sysadmin 角色的成員首先必須探索 DAC 通訊埠。 請參閱[資料庫管理員的診斷連接](https://docs.microsoft.com/en-us/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators#dac-port)來探索如何。 例如，如果 DAC 通訊埠是 33000，則，您無法連接到它與`sqlcmd`，如下所示：  

    ```
    sqlcmd –U <user> -P <pwd> -S <host>,33000
    ```

    > [!NOTE]  
    > DAC 連接必須使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]驗證。  
    
2.  如果陳述式屬性是透過 SQLSetConnectAttr 來傳遞的，則 UnixODBC 驅動程式對於所有的陳述式屬性都會傳回「無效的屬性/選項識別碼」。 在 Windows 中，當 SQLSetConnectAttr 接收陳述式的屬性值會導致驅動程式，也就是連接控制代碼的子系的所有作用中陳述式上設定該值。  

## <a name="see-also"></a>另請參閱  
[常見問題集](../../../connect/odbc/linux-mac/frequently-asked-questions-faq-for-odbc-linux.md)

[此驅動程式版本的已知問題](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)

[版本資訊](../../../connect/odbc/linux-mac/release-notes.md)
