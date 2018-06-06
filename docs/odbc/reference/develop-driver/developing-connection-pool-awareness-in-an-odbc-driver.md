---
title: 開發連接集區中的 ODBC 驅動程式的認知 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c63d5cae-24fc-4fee-89a9-ad0367cddc3e
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 795fa0d91e706b2c78bd12f492413ca10a04d35b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="developing-connection-pool-awareness-in-an-odbc-driver"></a>開發中的 ODBC 驅動程式的連接集區感知
本主題討論開發的 ODBC 驅動程式會包含驅動程式應如何提供連線共用服務的相關資訊的詳細資料。  
  
## <a name="enabling-driver-aware-connection-pooling"></a>啟用可感知驅動程式的連接集區  
 驅動程式必須實作下列 ODBC 服務提供者介面 (SPI) 函式：  
  
-   SQLSetConnectAttrForDbcInfo  
  
-   SQLSetConnectInfo  
  
-   SQLSetDriverConnectInfo  
  
-   SQLGetPoolID  
  
-   SQLRateConnection  
  
-   SQLPoolConnect  
  
-   SQLCleanupConnectionPoolID  
  
 請參閱[ODBC 服務提供者介面 (SPI) 參考](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)如需詳細資訊。  
  
 驅動程式也必須實作下列現有的函式，以便可以啟用可感知驅動程式共用：  
  
|函數|新增的功能|  
|--------------|-------------------------|  
|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)<br /><br /> [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)<br /><br /> [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|支援新的控制代碼類型： SQL_HANDLE_DBC_INFO_TOKEN （請參閱下方說明）。|  
|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|支援新的設定專用的連接屬性： SQL_ATTR_DBC_INFO_TOKEN 重設連接 （請參閱下方說明）。|  
  
> [!NOTE]  
>  已被取代的函式例如**SQLError**和**SQLSetConnectOption**不支援可感知驅動程式的連接共用。  
  
## <a name="the-pool-id"></a>集區識別碼  
 集區識別碼是指標長度驅動程式特定識別碼來代表特定群組的連線可以交替使用。 提供一組連接資訊，驅動程式應該要能夠快速推算相對應的集區識別碼。  
  
 例如，集區識別碼應編碼的伺服器名稱和認證資訊。 不過，因為驅動程式可能可以重複使用的連接，然後將資料庫變更為更少的時間比建立新的連接，不是需要資料庫名稱。  
  
 驅動程式應該定義一組索引鍵屬性，將會構成集區識別碼。 這些索引鍵屬性的值可來自於連接屬性、 連接字串和資料來源名稱。 萬一在這些來源中有任何衝突，現有的驅動程式特定的解決原則應該用於回溯相容性。  
  
 驅動程式管理員會使用不同的集區的不同的集區識別碼。 在相同的集區中的所有連線都都可重複使用。 驅動程式管理員將會永遠不會重複使用的連接，並提供不同的集區識別碼。  
  
 因此驅動程式應將指派的連接具有相同的值，其定義的索引鍵屬性中的每個群組的唯一集區識別碼。 如果驅動程式會在索引鍵屬性的值不同的兩個連線使用相同的集區識別碼，驅動程式管理員將仍將它們放入相同的集區 （驅動程式管理員完全不知道驅動程式特有的索引鍵屬性）。 這表示驅動程式將需要報告至驅動程式管理員與一組不同的索引鍵屬性的連接不是可重複使用內部[SQLRateConnection 函式](../../../odbc/reference/syntax/sqlrateconnection-function.md)。 這可能會降低效能，建議您不要。  
  
 驅動程式管理員不會重複使用連接，即使所有連接資訊都符合配置從另一個驅動程式的環境。 驅動程式管理員會使用不同的集區不同的環境中，即使連接具有相同的集區識別碼。 因此，集區識別碼是本機到驅動程式環境。  
  
 取得集區識別碼的驅動程式的函式是[SQLGetPoolID 函式](../../../odbc/reference/syntax/sqlgetpoolid-function.md)。  
  
## <a name="the-connection-rating"></a>連線等級  
 相較於建立新連線，您可以藉由重設某些連接資訊 （例如資料庫），在共用連接取得較佳的效能。 因此，您可能不想要在您的索引鍵屬性集的資料庫名稱。 否則，您可以有不同的集區的每個資料庫，這可能不是很好的中介層應用程式中，客戶使用各種不同的連接字串的位置。  
  
 每當您重複使用具有一些屬性不相符的連接，您應該重設不相符的屬性，根據新的應用程式要求，使傳回的連接是與應用程式要求相同 （請參閱屬性 SQL_ATTR 的討論在 _DBC_INFO_TOKEN [SQLSetConnectAttr 函數](http://go.microsoft.com/fwlink/?LinkId=59368))。 不過，重設這些屬性可能會降低效能。 例如，重設資料庫需要伺服器的網路呼叫。 因此，如果有的話，重複使用完全相符的連接。  
  
 驅動程式中的評等函式可以評估新的連線要求與現有的連接。 例如，可以判斷驅動程式的評等函式：  
  
-   如果現有的連線完全比對與要求。  
  
-   如果只有某些不重要不符，例如連接逾時，不需要與重設伺服器的通訊。  
  
-   如果有一些不相符的屬性，需要與重設伺服器的通訊，但仍會產生較佳的效能比建立新的連接。  
  
-   如果不相符的發生是非常耗費的時間來重設的屬性 （驅動程式的開發人員可能會考慮將此屬性加入至屬性集的索引鍵，用來產生的集區識別碼）。  
  
 可能的其中 0，則表示不要重複使用而 100 表示完全相符的分數，介於 0 到 100 之間。 [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)是分級連線的函式。  
  
## <a name="new-odbc-handle---sqlhandledbcinfotoken"></a>新 ODBC 控制代碼-SQL_HANDLE_DBC_INFO_TOKEN  
 若要支援共用的可感知驅動程式的連接，驅動程式必須連接資訊來計算集區的識別碼。 驅動程式也必須要比較與連線集區中的新連線要求的連接資訊。  每當沒有連接集區中的可以重複使用，驅動程式就必須建立新的連線，因此需要連接資訊。  
  
 由於連接資訊可以來自多個來源 （連接字串、 連接屬性和資料來源名稱），驅動程式可能必須剖析連接字串和解析這些來源中每個以上的函式呼叫之間的衝突。  
  
 因此，導入了新的 ODBC 控制代碼： SQL_HANDLE_DBC_INFO_TOKEN。 SQL_HANDLE_DBC_INFO_TOKEN，與驅動程式並不需要剖析連接字串與超過一次解決衝突的連接資訊。 由於這是一種驅動程式專屬資料結構時，驅動程式可以儲存連接資訊等資料或集區識別碼。  
  
 這個控制代碼只當做驅動程式管理員與驅動程式之間的介面。 應用程式無法直接配置這個控制代碼。  
  
 這個控制代碼的父控制代碼是型別 SQL_HANDLE_ENV，表示驅動程式可以取得從 HENV 控制代碼的環境資訊的連接資訊解析期間。  
  
 每當收到新的連線要求，驅動程式管理員將用於儲存連接資訊之後就能確認驅動程式支援連接集區感知, 配置 SQL_HANDLE_DBC_INFO_TOKEN 類型的控制代碼。 當完成使用此控制代碼 (不過有些會傳回前傳回代碼從 SQL_STILL_EXECUTING 以外[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)或[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md))，驅動程式管理員會釋放控制代碼。 因此，此控制代碼 SQLAllocHandle 呼叫之後，建立及終結 SQLFreeHandle 呼叫之後。 驅動程式管理員 保證的控制代碼將會釋放，然後再釋放其相關聯的 HENV (當[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)或[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)會傳回錯誤)。  
  
 驅動程式應該修改下列的函式以接受新的控制代碼類型 SQL_HANDLE_DBC_INFO_TOKEN:  
  
1.  [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
2.  [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
3.  [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
4.  [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
 驅動程式管理員可保證，多個執行緒不會使用相同的 SQL_HANDLE_DBC_INFO_TOKEN 控制代碼同時。 因此，此控制代碼的同步處理模型可以是非常簡單的驅動程式內。 配置及釋放 SQL_HANDLE_DBC_INFO_TOKEN 之前，驅動程式管理員會等到環境鎖定。  
  
 驅動程式管理員**SQLAllocHandle**和**SQLFreeHandle**不接受這個新的控制代碼類型。  
  
 SQL_HANDLE_DBC_INFO_TOKEN 可能包含機密資訊，例如認證。 因此，驅動程式應安全地清除記憶體緩衝區 (使用[SecureZeroMemory](http://msdn.microsoft.com/library/windows/desktop/aa366877\(v=vs.85\).aspx))，其中包含敏感資訊釋放與這個控制代碼之前**SQLFreeHandle**。 每當應用程式的環境控制代碼關閉時，將會關閉所有相關聯的連接集區。  
  
## <a name="driver-manager-connection-pool-rating-algorithm"></a>評等演算法的驅動程式管理員連接集區  
 本章節討論驅動程式管理員連接共用的評等演算法。 驅動程式開發人員可以實作相同的演算法，用於回溯相容性。 此演算法可能無法最佳提案。 您應該精簡此演算法會根據您的實作 （否則沒有理由来實作這項功能）。  
  
 驅動程式管理員會傳回整數的評等從 0 到 100 之間的每一個連接從集區。 0 表示不能重複使用連接和 100 時，表示為完整比對。 假設 hRequest 名為連線要求，並從集區的現有連接會稱為 hCandidate。 如果任何一個下列條件為 false，則無法重複使用共用的連接 hCandidate hRequest （驅動程式管理員會指派 0 的評等） 的。  
  
-   hCandidate 與 hRequest 來自 UNICODE 應用程式開發介面 （例如 SQLDriverConnectW) 或 ANSI 應用程式開發介面 （例如 SQLDriverConnectA)。 （UNICODE 驅動程式，則可指定 ANSI 應用程式開發介面和 UNICODE 應用程式開發介面 （請參閱 「 連接 」 屬性 SQL_ATTR_ANSI_APP） 的行為不同。）  
  
-   相同的函式; 建立 hCandidate 和 hRequestSQLDriverConnect 或 SQLConnect。  
  
-   使用 SQLDriverConnect 時，用來開啟 hCandidate 的連接字串應該 hRequest，相同。  
  
-   伺服器名稱 （或資料來源名稱），使用者名稱，以及用來開啟 hCandidate 密碼應該用來開啟 hRequest 使用 SQLConnect 時相同。  
  
-   目前執行緒的安全性識別碼 (SID) 應該是相同的 SID 用於開啟 hCandidate。  
  
-   登錄和取消登錄相當費時的驅動程式 (SQL_DTC_TRANSITION_COST 中的討論內容，請參閱 < [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md))、 重複使用*hRequest*不需要額外的登記或 unenlistment。  
  
 下表顯示不同的案例的分數指派。  
  
|連接屬性管理的集區的連接和要求之間的比較|沒有編列 / unenlistment|需要額外的登記 / Unenlistment|  
|---------------------------------------------------------------------------------------|-----------------------------------|----------------------------------------------|  
|是不同的類別目錄 (SQL_ATTR_CURRENT_CATALOG)|60|50|  
|有些連接屬性不同，但目錄會是相同|90|70|  
|完全相符的所有連接屬性|100|80|  
  
## <a name="sequence-diagram"></a>順序圖表  
 此順序圖表顯示本主題中所述的基本集區機制。 它只會顯示使用[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)但[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)案例是類似。  
  
 ![順序圖表](../../../odbc/reference/develop-driver/media/odbc_seq_dia.gif "odbc_seq_dia")  
  
## <a name="state-diagram"></a>狀態圖表  
 這個狀態圖表會顯示此連接資訊 token 物件，本主題中所述。 圖表只會顯示[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)但[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)案例是類似。 因為驅動程式管理員可能需要在任何時間處理錯誤，可以呼叫驅動程式管理員[SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)任何狀態。  
  
 ![狀態圖表](../../../odbc/reference/develop-driver/media/odbc_state_diagram.gif "odbc_state_diagram")  
  
## <a name="see-also"></a>另請參閱  
 [可感知驅動程式的連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 服務提供者介面 (SPI) 參考](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)
