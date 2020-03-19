---
title: Linux 和 macOS 上的 ODBC 驅動程式已知問題
ms.date: 03/05/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- known issues
author: rothja
ms.author: jroth
ms.openlocfilehash: 9746456a4a38f2a19e485d1e17786073b97b243e
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79286432"
---
# <a name="known-issues-for-the-odbc-driver-on-linux-and-macos"></a>Linux 和 macOS 上的 ODBC 驅動程式已知問題

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

本文包含 Microsoft ODBC Driver for SQL Server on Linux and macOS 13、13.1 和 17 版的已知問題清單。 其中也包含針對連線能力問題進行疑難排解的步驟。

## <a name="known-issues"></a>已知問題

其他問題會公佈於 [Microsoft ODBC 驅動程式團隊部落格](https://blogs.msdn.com/b/sqlnativeclient/)上。  

- 由於系統程式庫的限制，Alpine Linux 支援較少的字元編碼和地區設定。 例如，en_US.UTF-8 無法使用。 如需詳細資訊，請參閱 [musl libc - functional differences from glibc](https://wiki.musl-libc.org/functional-differences-from-glibc.html) (musl libc - 與 glibc 的功能差異)。

- Windows、Linux 和 macOS 可能會以不同的方式轉換來自專用區 (PUA) 或使用者定義字元 (EUDC) 的字元。 透過 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 在伺服器上執行的轉換，會使用 Windows 轉換程式庫。 驅動程式中的轉換會使用 Windows、Linux 或 macOS 轉換程式庫。 執行這些轉換時，這兩個程式庫可能會產生不同的結果。 如需詳細資訊，請參閱[終端使用者定義字元和專用區字元](/windows/desktop/Intl/end-user-defined-characters)。

- 如果用戶端編碼是 UTF-8，則驅動程式管理員不一定會正確地從 UTF-8 格式轉換為 UTF-16。 目前，字串中若有一或多個字元不是有效的 UTF-8 字元，即會發生資料損毀。 ASCII 字元會正確地對應。 在呼叫 ODBC API 的 SQLCHAR 版本 (例如 SQLDriverConnectA) 時，驅動程式管理員會嘗試這項轉換。 在呼叫 ODBC API 的 SQLWCHAR 版本 (例如 SQLDriverConnectW) 時，驅動程式管理員將不會嘗試這項轉換。  

- **SQLBindParameter** 的 *ColumnSize* 參數會參考 SQL 類型中的字元數，而 *BufferLength* 是應用程式緩衝區中的位元組數目。 不過，如果 SQL 資料類型是 `varchar(n)` 或 `char(n)`、應用程式繫結如 SQL_C_CHAR 或 SQL_C_VARCHAR 等參數，且用戶端的字元編碼為 UTF-8，則驅動程式可能會顯示「字串資料，右側截斷」的錯誤，即使 *ColumnSize* 的值與伺服器上的資料類型大小相符亦然。 因為字元編碼之間的轉換可能會變更資料長度，所以發生此錯誤。 例如，右單引號字元 (U+2019) 以 CP-1252 編碼時會成為單位元組 0x92，但以 UTF-8 編碼時會成為 3 個位元組的序列 0xe2 0x80 0x99。

例如，如果您的編碼為 UTF-8，並同時為 out 參數 **SQLBindParameter** 中的 *Columnsize* 和 *ColumnSize* 指定 1，然後嘗試擷取伺服器上儲存在 `char(1)` 資料行的前一個字元 (使用 CP-1252)，則驅動程式會嘗試將它轉換成 3 個位元組的 UTF-8 編碼方式，但無法將結果放入 1 個位元組的緩衝區內。 換個方向，它在執行用戶端與伺服器上不同字碼頁之間的轉換前，會先比較 **SQLBindParameter** 中的 *ColumnSize* 與 *BufferLength*。 由於 *ColumnSize* 1 小於 *BufferLength* 3 (舉例來說)，因此驅動程式會產生錯誤。 若要避免這個錯誤，請確認資料在轉換後的長度可放入指定的緩衝區或資料行內。 請注意，就 `varchar(n)` 類型而言，*ColumnSize* 不可大於 8000。

## <a id="connectivity"></a> 針對連線問題進行疑難排解  

如果您無法使用 ODBC 驅動程式連線到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，請使用下列資訊來識別問題。  
  
最常見的連接問題是安裝了兩個 UnixODBC 驅動程式管理員複本。 請在 /usr 中搜尋 libodbc\*.so\*。 如果您看見多個檔案版本，表示您 (可能) 安裝了多個驅動程式管理員。 您的應用程式可能使用了錯誤的版本。
  
藉由編輯 `/etc/odbcinst.ini` 檔案以包含下列區段和這些項目來啟用連接記錄檔：

```
[ODBC]
Trace = Yes
TraceFile = (path to log file, or /dev/stdout to output directly to the terminal)
```  
  
如果連接再次失敗，且未出現記錄檔，表示您的電腦上 (可能) 有兩個驅動程式管理員複本。 否則，記錄輸出應如下所示：  
  
```
[ODBC][28783][1321576347.077780][SQLDriverConnectW.c][290]  
        Entry:  
            Connection = 0x17c858e0  
            Window Hdl = (nil)  
            Str In = [DRIVER={ODBC Driver 13 for SQL Server};SERVER={contoso.com};Trusted_Connection={YES};WSID={mydb.contoso.com};AP...][length = 139 (SQL_NTS)]  
            Str Out = (nil)  
            Str Out Max = 0  
            Str Out Ptr = (nil)  
            Completion = 0  
        UNICODE Using encoding ASCII 'UTF8' and UNICODE 'UTF16LE'  
```  
  
如果 ASCII 字元編碼不是 UTF-8，例如： 
  
```
UNICODE Using encoding ASCII 'ISO8859-1' and UNICODE 'UCS-2LE'  
```  
  
安裝了多個驅動程式管理員，且應用程式使用了錯誤的管理員，或是驅動程式管理員未正確建置。  
  
如需解決連接失敗的詳細資訊，請參閱：  

- [疑難排解 SQL 連接性問題的步驟](https://docs.microsoft.com/archive/blogs/sql_protocols/steps-to-troubleshoot-sql-connectivity-issues)  
  
- [SQL Server 2005 連接問題的疑難排解 - 第 1 部分](https://techcommunity.microsoft.com/t5/sql-server/sql-server-2005-connectivity-issue-troubleshoot-part-i/ba-p/383034)  
  
- [使用連接信號緩衝區在 SQL Server 2008 中進行連接的疑難排解](https://techcommunity.microsoft.com/t5/sql-server/connectivity-troubleshooting-in-sql-server-2008-with-the/ba-p/383393)  
  
- [SQL Server 驗證疑難排解員](https://docs.microsoft.com/archive/blogs/sqlsecurity/sql-server-authentication-troubleshooter)  

## <a name="next-steps"></a>後續步驟

如需 ODBC 驅動程式安裝指示，請參閱下列文章：

- [安裝 Linux 上的 Microsoft ODBC Driver for SQL Server](installing-the-microsoft-odbc-driver-for-sql-server.md)
- [安裝 macOS 上的 Microsoft ODBC Driver for SQL Server](install-microsoft-odbc-driver-sql-server-macos.md)

如需詳細資訊，請參閱[程式設計指導方針](programming-guidelines.md)和[版本資訊](release-notes-odbc-sql-server-linux-mac.md)。  
