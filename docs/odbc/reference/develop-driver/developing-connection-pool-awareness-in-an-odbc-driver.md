---
title: 在 ODBC 驅動程式中開發連接池感知 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c63d5cae-24fc-4fee-89a9-ad0367cddc3e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f77fea1d8439ac9ce7374b7dd47db5665686cfbc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283428"
---
# <a name="developing-connection-pool-awareness-in-an-odbc-driver"></a>在 ODBC 驅動程式中開發連線集區覺察
本主題討論開發ODBC驅動程式的詳細資訊,該驅動程式包含有關驅動程式應如何提供連接池服務的資訊。  
  
## <a name="enabling-driver-aware-connection-pooling"></a>開啟驅動程式感知連接池  
 驅動程式必須實現以下 ODBC 服務提供者介面 (SPI) 功能:  
  
-   SQLSetConnectattrFordbcinfo  
  
-   SQLSetConnectInfo  
  
-   SQLSet 驅動程式連線資訊  
  
-   SQLGetPoolID  
  
-   SQLRate 連線  
  
-   SQLPool 連接  
  
-   SQL 清理連線池 ID  
  
 有關詳細資訊[,請參閱 ODBC 服務提供者介面 (SPI) 參考](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)。  
  
 驅動程式還必須實現以下現有函數,以便啟用驅動程式感知池:  
  
|函式|新增功能|  
|--------------|-------------------------|  
|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)<br /><br /> [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)<br /><br /> [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|支援新的句柄類型:SQL_HANDLE_DBC_INFO_TOKEN(請參閱下面的說明)。|  
|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|支援新的僅集連接屬性:SQL_ATTR_DBC_INFO_TOKEN重置連接(請參閱下面的說明)。|  
  
> [!NOTE]  
>  棄用功能(如**SQLError**和**SQLSetConnectOption)** 不支援用於驅動程式感知連接池。  
  
## <a name="the-pool-id"></a>池識別碼  
 池 ID 是一個指標長度的特定於驅動程式的 ID,用於表示可互換使用的特定連接組。 給定一組連接資訊,驅動程序應該能夠快速推斷出相應的池 ID。  
  
 例如,池 ID 應對伺服器名稱和憑據資訊進行編碼。 但是,不需要資料庫名稱,因為驅動程式可能能夠重用連接,然後在比建立新連接更短的時間內更改資料庫。  
  
 驅動程式應定義一組關鍵屬性,這些屬性將包含池 ID。 這些關鍵屬性的值可以來自連接屬性、連接字串和 DSN。 如果這些源中有任何衝突,則應使用現有的特定於驅動程式的解析策略來進行向後相容性。  
  
 驅動程式管理器將使用不同的池用於不同的池。 同一池中的所有連接都是可重用的。 驅動程式管理員永遠不會重用具有其他池 ID 的連接。  
  
 因此,驅動程式應為其定義的關鍵屬性中具有相同值的每個連接組分配唯一的池 ID。 如果驅動程式對鍵屬性中具有不同值的兩個連接使用相同的池 ID,驅動程式管理器仍將將它們放入同一池(驅動程式管理器對特定於驅動程式的鍵屬性一無所知)。 這意味著驅動程式將需要向驅動程式管理員報告,與一組其他鍵屬性的連接在[SQLRateConnection 函數](../../../odbc/reference/syntax/sqlrateconnection-function.md)中不可重用。 這可能會降低性能,不建議這樣做。  
  
 驅動程式管理器不會重用從其他驅動程式環境分配的連接,即使所有連接資訊都匹配。 驅動程式管理員將針對不同的環境使用不同的池,即使連接具有相同的池 ID 也是如此。 因此,池 ID 是其驅動程序環境的本地。  
  
 從驅動程式取得池 ID 的函數是[SQLGetPoolID 函數](../../../odbc/reference/syntax/sqlgetpoolid-function.md)。  
  
## <a name="the-connection-rating"></a>連線評級  
 與建立新連接相比,您可以通過在池連接中重置某些連接資訊(如 DATABASE)來獲得更好的性能。 因此,您可能不希望資料庫名稱位於一組關鍵屬性中。 否則,您可以為每個資料庫建立一個單獨的池,這在中端應用程式中可能並不好,因為客戶使用不同的不同連接字串。  
  
 每當重用具有某些屬性不匹配的連接時,應基於新的應用程式請求重置不匹配的屬性,以便返回的連接與應用程式請求相同(請參閱[SQLSetConnect Attr 函數](https://go.microsoft.com/fwlink/?LinkId=59368)中SQL_ATTR_DBC_INFO_TOKEN的屬性討論)。 但是,重置這些屬性可能會降低性能。 例如,重置資料庫需要對伺服器進行網路調用。 因此,請重用完全匹配的連接(如果有)。  
  
 驅動程式中的評級功能可以評估具有新連接請求的現有連接。 例如,驅動程式的評級功能可以確定:  
  
-   如果現有連接與請求完美匹配。  
  
-   如果只有一些微不足道的不匹配(如連接超時),則不需要與伺服器通信來重置。  
  
-   如果有一些不匹配的屬性需要與伺服器通信來重置,但仍會比建立新連接更性能。  
  
-   如果發生不匹配的屬性非常耗時的重置(驅動程式的開發人員可以考慮將此屬性添加到用於生成池 ID 的金鑰屬性集中)。  
  
 分數介於 0 和 100 之間是可能的,其中 0 表示不重用,100 表示完全匹配。 [SQLRate 連接](../../../odbc/reference/syntax/sqlrateconnection-function.md)是用於對連接進行評級的函數。  
  
## <a name="new-odbc-handle---sql_handle_dbc_info_token"></a>新的 ODBC 句柄 - SQL_HANDLE_DBC_INFO_TOKEN  
 為了支援驅動程式感知連接池,驅動程式需要連接資訊來計算池 ID。 驅動程式還需要連接資訊來比較新的連接請求和池中的連接。  只要池中沒有任何連接可以重用,驅動程式就必須建立新的連接,因此需要連接資訊。  
  
 由於連接資訊可能來自多個源(連接字串、連接屬性和DSN),驅動程式可能需要分析連接字串並解決上述每個函數調用中這些源之間的衝突。  
  
 因此,引入了一個新的 ODBC 句柄:SQL_HANDLE_DBC_INFO_TOKEN。 使用SQL_HANDLE_DBC_INFO_TOKEN,驅動程式不需要多次解析連接字串並解決連接資訊中的衝突。 由於這是特定於驅動程序的數據結構,驅動程式可以儲存連接資訊或池 ID 等數據。  
  
 此句柄僅用作驅動程式管理器和驅動程式之間的介面。 應用程式不能直接分配此句柄。  
  
 此句柄的父句柄的類型為SQL_HANDLE_ENV,這意味著驅動程式可以在連接資訊解析期間從 HENV 句柄獲取環境資訊。  
  
 每當它收到新的連接請求時,驅動程式管理員將分配一個類型SQL_HANDLE_DBC_INFO_TOKEN的句柄,用於存儲連接資訊,因為它確認驅動程式支援連接池感知。 使用完該句柄后(但在從[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)或[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)返回SQL_STILL_EXECUTING以外的一些返回代碼之前),驅動程式管理器將釋放該句柄。 因此,句柄是在 SQLAllocHandle 調用之後創建的,並在 SQLFreeHandle 調用後銷毀。 驅動程式管理員保證在釋放其關聯的 HENV 之前([當 SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)或[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)傳回錯誤時),將釋放句柄。  
  
 驅動程式應修改以下函數以接受新的句柄類型SQL_HANDLE_DBC_INFO_TOKEN:  
  
1.  [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
2.  [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
3.  [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
4.  [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
 驅動程式管理員保證多個線程不會同時使用相同的SQL_HANDLE_DBC_INFO_TOKEN句柄。 因此,此句柄的同步模型在驅動程序內部可能非常簡單。 在分配和釋放SQL_HANDLE_DBC_INFO_TOKEN之前,驅動程式管理器不會獲取環境鎖。  
  
 驅動程式管理員的**SQLAllocHandle**和**SQLFreeHandle**不會接受此新的句柄類型。  
  
 SQL_HANDLE_DBC_INFO_TOKEN可能包含機密資訊,如憑據。 因此,驅動程式應在使用**SQLFreeHandle**釋放此句柄之前安全地清除包含敏感資訊的記憶體緩衝區(使用[Secure ZeroMemory)。](https://msdn.microsoft.com/library/windows/desktop/aa366877\(v=vs.85\).aspx) 每當關閉應用程式的環境句柄時,將關閉所有關聯的連接池。  
  
## <a name="driver-manager-connection-pool-rating-algorithm"></a>驅動程式管理員連接池評級演演算法  
 本節討論驅動程式管理器連接池的評級演演演算法。 驅動程式開發人員可以實現相同的演演演算法,以實現向後相容性。 此演演演算法可能不是最佳演演演算法。 您應該基於實現來優化此演演演算法(否則,沒有理由實現此功能)。  
  
 驅動程式管理員將從池中的每個連接返回從 0 到 100 的積分評級。 0 表示連接無法重複使用,100 表示完美匹配。 假設連接請求名為 hRequest,並且池中的現有連接命名為 h候選。 如果以下任一條件為 false,則池連接 h候選項不能重新用於 hRequest(驅動程式管理員將分配評級為 0)。  
  
-   h候選和 hRequest 都來自 UNICODE API(如 SQLDriverConnectW)或 ANSI API(如 SQLDriverConnectA)。 (給定 ANSI API 和 UNICODE API(請參閱連接屬性SQL_ATTR_ANSI_APP),UNICODE 驅動程式可以行為不同。  
  
-   h候選和 hRequest 由同一函數創建;SQLDriver 連接或 SQLConnect。  
  
-   使用 SQLDriverConnect 時,用於打開 hAa 的連接字串應與 hRequest 相同。  
  
-   用於打開 hAt 的伺服器名稱(或 DSN)、使用者名稱和密碼應與使用 SQLConnect 時用於打開 hRequest 的密碼相同。  
  
-   當前線程的安全識別碼 (SID) 應與用於打開 h候選項的 SID 相同。  
  
-   對於登記和取消登記費用高昂的驅動程式(請參閱[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)中有關SQL_DTC_TRANSITION_COST的討論),重用*hRequest*不需要額外的登記或取消登記。  
  
 下表顯示了不同方案的分數分配。  
  
|池連線與要求之間的連線屬性比較|無登記/未登記|要求額外登記/取消登記|  
|---------------------------------------------------------------------------------------|-----------------------------------|----------------------------------------------|  
|目錄(SQL_ATTR_CURRENT_CATALOG)不同|60|50|  
|某些連線屬性不同,但目錄相同|90|70|  
|所有連線屬性完美配|100|80|  
  
## <a name="sequence-diagram"></a>順序圖表  
 此序列圖顯示了本主題中描述的基本池機制。 它只顯示[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)的使用,但[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)大小寫類似。  
  
 ![順序圖表](../../../odbc/reference/develop-driver/media/odbc_seq_dia.gif "odbc_seq_dia")  
  
## <a name="state-diagram"></a>狀態圖表  
 此狀態圖顯示連接資訊令牌物件,本主題中介紹。 該關係圖僅顯示[SQLDriverConnect,](../../../odbc/reference/syntax/sqldriverconnect-function.md)但[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)大小寫類似。 由於驅動程式管理員可能需要隨時處理錯誤,因此驅動程式管理器可以調用[SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)查看任何狀態。  
  
 ![狀態圖表](../../../odbc/reference/develop-driver/media/odbc_state_diagram.gif "odbc_state_diagram")  
  
## <a name="see-also"></a>另請參閱  
 [驅動程式感知連接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 服務提供者介面 (SPI) 參考](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)
