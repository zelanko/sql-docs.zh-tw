---
title: "程式設計指導方針 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2e3aac41bd87f52998edf366d7c3da2326de3f26
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="programming-guidelines"></a>程式設計指導方針
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]程式設計功能[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver 13 和 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] macOS 和 Linux 為基礎中的 ODBC[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]原生用戶端 ([SQL Server Native Client (ODBC)](http://go.microsoft.com/fwlink/?LinkID=134151))。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]原生用戶端以 Windows Data Access Components 中的 ODBC 為基礎 ([ODBC 程式設計人員參考](http://go.microsoft.com/fwlink/?LinkID=45250))。  

ODBC 應用程式可以使用 Multiple Active Result Sets (MARS) 和其他[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]所包括的特定功能`/usr/local/include/msodbcsql.h`之後 unixODBC 標頭 (`sql.h`， `sqlext.h`， `sqltypes.h`，和`sqlucode.h`)。 然後使用相同的符號名稱[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]-您可以在 Windows ODBC 應用程式中的特定項目。  

## <a name="available-features"></a>可用的功能  
下面各節從[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]Native Client ODBC 的文件 ([SQL Server Native Client (ODBC)](http://go.microsoft.com/fwlink/?LinkID=134151)) 時使用 macOS 和 Linux 上的 ODBC 驅動程式都是有效：  

-   [與 SQL Server (ODBC) 通訊](http://msdn.microsoft.com/library/ms131692.aspx)  
-   [連接和查詢逾時支援](http://msdn.microsoft.com/library/ms130822.aspx)  
-   [資料指標](http://msdn.microsoft.com/library/ms130794(SQL.110).aspx)  
-   [日期/時間改善 (ODBC)](http://msdn.microsoft.com/library/bb677319.aspx)  
-   [執行查詢 (ODBC)](http://msdn.microsoft.com/library/ms131677.aspx)  
-   [處理錯誤和訊息](http://msdn.microsoft.com/library/ms131289.aspx)  
-   [Kerberos 驗證](http://msdn.microsoft.com/library/cc280459.aspx)  
-   [大型 CLR 使用者定義型別 (ODBC)](http://msdn.microsoft.com/library/bb677316.aspx)  
-   [執行交易 (ODBC) （分散式交易除外）](http://msdn.microsoft.com/library/ms131706.aspx)  
-   [處理結果 (ODBC)](http://msdn.microsoft.com/library/ms130812.aspx)  
-   [執行預存程序](http://msdn.microsoft.com/library/ms131440.aspx)
-   [疏鬆資料行支援 (ODBC)](http://msdn.microsoft.com/library/cc280357.aspx)
-   [SSL 加密](http://msdn.microsoft.com/library/ms131691.aspx)
-   [資料表值的參數](https://docs.microsoft.com/en-us/sql/relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc)
-   [Utf-8 和 utf-16 命令和資料 api](http://msdn.microsoft.com/library/ff878241.aspx)
-   [使用目錄函數](http://msdn.microsoft.com/library/ms131490.aspx)  

## <a name="unsupported-features"></a>不支援的功能

在這一版的 ODBC 驅動程式正常運作 macOS 和 Linux 上尚未驗證下列功能：

-   容錯移轉叢集連線
-   [透明網路 IP 解析](https://docs.microsoft.com/en-us/sql/connect/odbc/linux/using-transparent-network-ip-resolution)
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

編碼的用戶端可以是下列其中一項：
  -  UTF-8
  -  ISO 8859-1
  -  ISO 8859-2
  -  ISO 8859-3
  -  ISO 8859-4
  -  ISO 8859-5
  -  ISO 8859-6
  -  ISO 8859-7
  -  ISO 8859-8
  -  ISO 8859-9
  -  ISO-8859-13
  -  ISO 8859-15
  
SQLCHAR 資料必須是其中一個支援的字元集。 SQLWCHAR 資料必須是 UTF-16LE (Little Endian)。  

如果 SQLDescribeParameter 未指定伺服器上的 SQL 類型，驅動程式將會使用 SQLBindParameter 的 *ParameterType* 參數中所指定的 SQL 類型。 如果 SQLBindParameter 中指定了窄字元 SQL 類型，例如 SQL_VARCHAR，驅動程式會將轉換提供的資料從用戶端字碼頁為預設值[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]字碼頁。 (預設值[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]字碼頁通常是 1252年。)如果不支援用戶端字碼頁，它就會設定為 utf-8。 在此情況下，驅動程式再將 utf-8 資料轉換成預設字碼頁。 不過，資料可能會遺失。 如果字碼頁 1252 無法顯示某個字元，驅動程式會將該字元轉換成問號 ('?')。 若要避免這種資料遺失，請在 SQLBindParameter 中指定 Unicode SQL 字元類型，例如 SQL_NVARCHAR。 在此情況下，驅動程式將轉換提供的 Unicode 資料，在 utf-8 編碼為 utf-16，而不會遺失資料。

沒有文字編碼轉換差異 Windows 與 Linux 及 macOS 上的 iconv 程式庫的數個版本之間。 字碼頁 1255 （希伯來文） 編碼的文字資料有一個字碼元素 0xca ()，在轉換時的行為方式。 將這個字元轉換成 Windows 上為 Unicode，會產生 0x05BA 的 utf-16 字碼指標。 轉換成 Unicode macOS 和 Linux 上使用 libiconv 版本早於 1.15 會產生 0x00CA 的 utf-16 字碼指標。

當 UTF-8 多位元組字元或 UTF-16 替代項目在 SQLPutData 緩衝區間分散時，將會造成資料損毀。 對於最後不是部分字元編碼的串流 SQLPutData，請使用緩衝區。  

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

