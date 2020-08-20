---
description: 在 ODBC 驅動程式中開發連線集區覺察
title: 在 ODBC 驅動程式中開發連接集區感知 |Microsoft Docs
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
ms.openlocfilehash: 519a2b64f6a5330b8c8fde458323c6c900941025
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476270"
---
# <a name="developing-connection-pool-awareness-in-an-odbc-driver"></a>在 ODBC 驅動程式中開發連線集區覺察
本主題討論開發 ODBC 驅動程式的詳細資料，其中包含驅動程式如何提供連接共用服務的相關資訊。  
  
## <a name="enabling-driver-aware-connection-pooling"></a>啟用驅動程式感知連接共用  
 驅動程式必須執行下列 ODBC 服務提供者介面 (SPI) 函數：  
  
-   SQLSetConnectAttrForDbcInfo  
  
-   SQLSetConnectInfo  
  
-   SQLSetDriverConnectInfo  
  
-   SQLGetPoolID  
  
-   SQLRateConnection  
  
-   SQLPoolConnect  
  
-   SQLCleanupConnectionPoolID  
  
 如需詳細資訊，請參閱 [ODBC 服務提供者介面 (SPI) 參考](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md) 。  
  
 驅動程式也必須執行下列現有的功能，才能啟用驅動程式感知共用：  
  
|函式|新增的功能|  
|--------------|-------------------------|  
|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)<br /><br /> [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)<br /><br /> [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|支援新的控制碼類型： SQL_HANDLE_DBC_INFO_TOKEN (請參閱下方的描述) 。|  
|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|支援新的僅限設定連接屬性： SQL_ATTR_DBC_INFO_TOKEN 若要重設連接 (請參閱以下) 的描述。|  
  
> [!NOTE]  
>  已淘汰的功能（例如 **SQLError** 和 **SQLSetConnectOption** ）不支援驅動程式感知的連接共用。  
  
## <a name="the-pool-id"></a>集區識別碼  
 集區識別碼是指標長度驅動程式專屬的識別碼，代表可以交換使用的特定連接群組。 由於有一組連接資訊，驅動程式應該能夠快速推算對應的集區識別碼。  
  
 例如，集區識別碼應該將伺服器名稱和認證資訊編碼。 但是，資料庫名稱不是必要的，因為驅動程式可以重複使用連接，然後以比建立新連接更少的時間來變更資料庫。  
  
 驅動程式應定義一組索引鍵屬性，這些屬性會組成集區識別碼。 這些索引鍵屬性的值可能來自連接屬性、連接字串和 DSN。 如果這些來源中有任何衝突，則應該使用現有的驅動程式專用解析原則來提供回溯相容性。  
  
 驅動程式管理員會針對不同的集區識別碼使用不同的集區。 相同集區中的所有連接都可以重複使用。 驅動程式管理員絕不會重複使用具有不同集區識別碼的連接。  
  
 因此，驅動程式應該為每個連線群組指派唯一的集區識別碼，其定義的索引鍵屬性中的值相同。 如果驅動程式針對其索引鍵屬性中具有不同值的兩個連線使用相同的集區識別碼，驅動程式管理員仍會將它們放入相同的集區， (驅動程式管理員不知道驅動程式特定的金鑰屬性) 。 這表示驅動程式將需要向驅動程式管理員報告，但無法在 [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)函式內重複使用與不同索引鍵屬性集的連接。 這可能會降低效能，因此不建議這麼做。  
  
 驅動程式管理員將不會重複使用從另一個驅動程式環境配置的連接，即使所有連接資訊都相符。 驅動程式管理員會針對不同的環境使用不同的集區，即使連接具有相同的集區識別碼也是一樣。 因此，集區識別碼在其驅動程式環境中是本機的。  
  
 從驅動程式取得集區識別碼的函數是 [SQLGetPoolID](../../../odbc/reference/syntax/sqlgetpoolid-function.md)函式。  
  
## <a name="the-connection-rating"></a>連接分級  
 相較于建立新的連接，您可以藉由重設某些連接 (資訊（例如，在共用連接中的資料庫) ）來取得較佳的效能。 因此，您可能不想讓資料庫名稱在您的索引鍵屬性集內。 否則，您可以為每個資料庫建立不同的集區，這在中介層應用程式中可能不適合，客戶使用不同的連接字串。  
  
 每當您重複使用具有某些屬性不符的連接時，您應該根據新的應用程式要求重設不相符的屬性，讓傳回的連接與應用程式要求相同， (查看 [SQLSetConnectAttr](https://go.microsoft.com/fwlink/?LinkId=59368) 函式) 中 SQL_ATTR_DBC_INFO_TOKEN 屬性的討論。 但是，重設這些屬性可能會降低效能。 例如，重設資料庫需要對伺服器進行網路呼叫。 因此，請重複使用完全相符的連接（如果有的話）。  
  
 驅動程式中的評等函式可以使用新的連線要求來評估現有的連接。 例如，驅動程式的評等功能可以判斷：  
  
-   如果現有的連接與要求完全相符。  
  
-   如果只有一些無意義的不相符，例如連接逾時，則不需要與伺服器通訊來重設。  
  
-   如果有一些不相符的屬性需要與伺服器進行通訊以重設，但仍會導致效能優於建立新的連接。  
  
-   如果在重設 (非常耗時的屬性發生不相符的情況，驅動程式的開發人員可能會考慮將此屬性加入至用來產生集區識別碼) 的索引鍵屬性集。  
  
 介於0和100之間的分數是可行的，其中0表示不重複使用，100表示完全相符。 [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md) 是用來評等連接的函式。  
  
## <a name="new-odbc-handle---sql_handle_dbc_info_token"></a>新的 ODBC 控制碼-SQL_HANDLE_DBC_INFO_TOKEN  
 若要支援驅動程式感知連接共用，驅動程式需要連線資訊來計算集區識別碼。 驅動程式也需要連接資訊，以比較新的連接要求與集區中的連線。  當集區中沒有任何連線可以重複使用時，驅動程式必須建立新的連接，因此需要連接資訊。  
  
 由於連接資訊可能來自多個來源 (連接字串、連接屬性和 DSN) ，因此驅動程式可能需要剖析連接字串，並解決上述每個函式呼叫中這些來源之間的衝突。  
  
 因此，引進了新的 ODBC 控制碼： SQL_HANDLE_DBC_INFO_TOKEN。 使用 SQL_HANDLE_DBC_INFO_TOKEN 時，驅動程式不需要剖析連接字串，也不需要解決連接資訊中的衝突。 由於這是驅動程式特定的資料結構，因此驅動程式可以儲存資料，例如連接資訊或集區識別碼。  
  
 這個控制碼只會用來做為驅動程式管理員與驅動程式之間的介面。 應用程式無法直接配置此控制碼。  
  
 這個控制碼的父控制碼屬於 SQL_HANDLE_ENV 類型，也就是說，驅動程式可以在連接資訊解析期間從 HENV 控制碼取得環境資訊。  
  
 當它收到新的連線要求時，驅動程式管理員會在確認驅動程式支援連線集區感知之後，配置儲存連接資訊的 SQL_HANDLE_DBC_INFO_TOKEN 類型的控制碼。 當您完成使用控制碼 (但除了傳回從 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 或 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)) SQL_STILL_EXECUTING 以外的一些傳回碼之前，驅動程式管理員將釋放控制碼。 因此，在 SQLAllocHandle 呼叫之後會建立控制碼，並在 SQLFreeHandle 呼叫之後損毀。 當 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 或 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 傳回錯誤) 時，驅動程式管理員可保證將會釋放控制碼，然後釋放其相關聯的 HENV (。  
  
 驅動程式應該修改下列函式，以接受新的控制碼類型 SQL_HANDLE_DBC_INFO_TOKEN：  
  
1.  [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
2.  [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
3.  [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
4.  [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
 驅動程式管理員可保證多個執行緒不會同時使用相同的 SQL_HANDLE_DBC_INFO_TOKEN 控制碼。 因此，這個控制碼的同步處理模型在驅動程式內可能很簡單。 在配置和釋放 SQL_HANDLE_DBC_INFO_TOKEN 之前，驅動程式管理員不會進行環境鎖定。  
  
 驅動程式管理員的 **SQLAllocHandle** 和 **SQLFreeHandle** 將不會接受這個新的控制碼類型。  
  
 SQL_HANDLE_DBC_INFO_TOKEN 可能包含機密資訊，例如認證。 因此，在使用**SQLFreeHandle**釋放此控制碼之前，驅動程式應該安全地清除記憶體緩衝區 (使用包含敏感性資訊的[SecureZeroMemory](https://msdn.microsoft.com/library/windows/desktop/aa366877\(v=vs.85\).aspx)) 。 每當應用程式的環境控制碼關閉時，就會關閉所有相關聯的連接集區。  
  
## <a name="driver-manager-connection-pool-rating-algorithm"></a>驅動程式管理員連接集區分級演算法  
 本節討論驅動程式管理員連接共用的評等演算法。 驅動程式開發人員可以執行相同的演算法來提供回溯相容性。 這種演算法可能不是最佳的演算法。 您應以您的實作為基礎來精簡此演算法 (否則，就沒有理由) 執行此功能。  
  
 針對集區中的每個連接，驅動程式管理員會傳回從0到100的整數評等。 0表示無法重複使用連接，100表示完全相符。 假設連接要求的名稱為 hRequest，而集區中的現有連接會命名為 hCandidate。 如果下列任何一個條件為 false，則無法重複使用共用連線 hCandidate 進行 hRequest (驅動程式管理員會指派 0) 的評等。  
  
-   hCandidate 和 hRequest 都是來自 UNICODE API (例如 SQLDriverConnectW) 或 ANSI API (例如 SQLDriverConnectA) 。  (UNICODE 驅動程式可行為不同的指定 ANSI API 和 UNICODE API (請參閱連接屬性 SQL_ATTR_ANSI_APP) 。 )   
  
-   hCandidate 和 hRequest 是由相同的函式所建立;可能是 SQLDriverConnect 或 SQLConnect。  
  
-   使用 SQLDriverConnect 時，用來開啟 hCandidate 的連接字串應該與 hRequest 相同。  
  
-   在使用 SQLConnect 時，用來開啟 hCandidate 的 ServerName (或 DSN) 、使用者名稱和密碼，都應該與用來開啟 hRequest 的使用者名稱和密碼相同。  
  
-   目前線程 (SID) 的安全識別碼必須與用來開啟 hCandidate 的 SID 相同。  
  
-   針對需要登錄和取消登錄的驅動程式， (請參閱 SQL_DTC_TRANSITION_COST 在 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)) 中的討論，重複使用 *hRequest* 不需要額外的登錄或 unenlistment。  
  
 下表顯示不同案例的分數指派。  
  
|共用連接與要求之間的連接屬性比較|無登記/unenlistment|需要額外的登記/Unenlistment|  
|---------------------------------------------------------------------------------------|-----------------------------------|----------------------------------------------|  
| (SQL_ATTR_CURRENT_CATALOG) 的目錄不同|60|50|  
|某些連接屬性不同，但目錄相同|90|70|  
|完全相符的所有連接屬性|100|80|  
  
## <a name="sequence-diagram"></a>順序圖表  
 此順序圖表會顯示本主題中所述的基本共用機制。 它只會顯示使用 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) ，但 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 案例很類似。  
  
 ![順序圖表](../../../odbc/reference/develop-driver/media/odbc_seq_dia.gif "odbc_seq_dia")  
  
## <a name="state-diagram"></a>狀態圖表  
 此狀態圖表會顯示此主題中所述的連接資訊權杖物件。 此圖表只會顯示 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) ，但 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 案例很類似。 因為驅動程式管理員可能需要在任何時間處理錯誤，所以驅動程式管理員可以針對任何狀態呼叫 [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md) 。  
  
 ![狀態圖表](../../../odbc/reference/develop-driver/media/odbc_state_diagram.gif "odbc_state_diagram")  
  
## <a name="see-also"></a>另請參閱  
 [驅動程式感知連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 服務提供者介面 (SPI) 參考](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)
