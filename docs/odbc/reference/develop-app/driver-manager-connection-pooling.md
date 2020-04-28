---
title: 驅動程式管理員連接共用 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection pooling [ODBC]
- pooled connections [ODBC]
- connecting to driver [ODBC], connection pooling
- connecting to data source [ODBC], connection pooling
ms.assetid: ee95ffdb-5aa1-49a3-beb2-7695b27c3df9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 84ccc0db8f9a54eecc8337ca5efbc7b4c4baa239
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305819"
---
# <a name="driver-manager-connection-pooling"></a>驅動程式管理員連線共用
連線共用可讓應用程式使用不需要重新建立的連線集區連接，以供每次使用。 一旦建立連線並將其放在集區中，應用程式就可以重複使用該連接，而不需要執行完整的連接處理。  
  
 使用集區連接可以大幅提升效能，因為應用程式可以節省建立連接所需的額外負荷。 這對於透過網路連接的仲介層應用程式，或針對重複連線和中斷連接的應用程式（例如網際網路應用程式）而言特別重要。  
  
 除了提升效能之外，連接共用架構也可讓環境和其相關聯的連接在單一進程中由多個元件使用。 這表示相同進程中的獨立元件可以彼此互動，而不會察覺彼此。 多個元件可以重複使用連接集區中的連接。  
  
> [!NOTE]
>  ODBC 應用程式可以使用連接共用，也就是 ODBC 2。*x*行為，只要應用程式可以呼叫*SQLSetEnvAttr*。 使用連接共用時，應用程式不能執行變更資料庫或資料庫內容的 SQL 語句，例如\<變更*資料庫名稱*>，這會變更資料來源所使用的目錄。  


 ODBC 驅動程式必須是完全安全線程，而且連接不能有線程親和性來支援連接共用。 這表示驅動程式能夠隨時處理任何執行緒上的呼叫，而且能夠在一個執行緒上連接、使用另一個執行緒上的連接，以及在第三個執行緒上中斷連線。  
  
 連接集區是由驅動程式管理員維護。 當應用程式呼叫**SQLConnect**或**SQLDriverConnect**時，會從集區繪製連接，並在應用程式呼叫**SQLDisconnect**時傳回至集區。 集區的大小會根據要求的資源配置，以動態方式成長。 它會根據非使用狀態的超時時間來壓縮：如果連接未作用一段時間（未在連線中使用），則會從集區中移除。 集區的大小只受限於伺服器上的記憶體限制和限制。  
  
 驅動程式管理員會根據在**SQLConnect**或**SQLDriverConnect**中傳遞的引數，以及在配置連接之後所設定的連接屬性，決定是否要使用集區中的特定連接。  
  
 當驅動程式管理員共用連線時，它必須能夠判斷連接是否仍在運作中，然後再進行連接。 否則，當發生暫時性的網路失敗時，驅動程式管理員會持續處理應用程式的無作用連接。 ODBC 3.x 中已定義新的連接*屬性： SQL_ATTR_CONNECTION_DEAD*。 這是唯讀的連接屬性，會傳回 SQL_CD_TRUE 或 SQL_CD_FALSE。 值 SQL_CD_TRUE 表示連接已經遺失，而值 SQL_CD_FALSE 表示連接仍在使用中。 （符合舊版 ODBC 的驅動程式也可以支援此屬性。）  
  
 驅動程式必須有效率地執行此選項，否則會影響連接共用的效能。 具體而言，取得此連接屬性的呼叫應該不會造成伺服器往返。 相反地，驅動程式應該只傳回連接的最後已知狀態。 如果最後一次傳送至伺服器失敗，連接就會失效，如果最後一次行程成功，則不會停止。  
  
## <a name="remarks"></a>備註  
 如果連接已遺失（透過 SQL_ATTR_CONNECTION_DEAD 回報），ODBC 驅動程式管理員將會藉由呼叫驅動程式中的 SQLDisconnect 來終結該連接。 新的連線要求在集區中可能找不到可用的連接。 最後，驅動程式管理員可能會建立新的連接，假設該集區是空的。  
  
 若要使用連接集區，應用程式會執行下列步驟：  
  
1.  藉由呼叫**SQLSetEnvAttr**來啟用連接共用，以將 SQL_ATTR_CONNECTION_POOLING 環境屬性設定為 SQL_CP_ONE_PER_DRIVER 或 SQL_CP_ONE_PER_HENV。 必須先進行此呼叫，應用程式才會配置要啟用連接共用的共用環境。 **SQLSetEnvAttr**呼叫中的環境控制碼應設定為 null，這會使 SQL_ATTR_CONNECTION_POOLING 進程層級的屬性。 如果屬性設定為 SQL_CP_ONE_PER_DRIVER，每個驅動程式都支援單一連接集區。 如果應用程式適用于許多驅動程式和少數環境，這可能會更有效率，因為可能需要較少的比較。 如果設定為 SQL_CP_ONE_PER_HENV，每個環境都支援單一連接集區。 如果應用程式適用于許多環境和少數驅動程式，這可能會更有效率，因為可能需要較少的比較。 將 SQL_ATTR_CONNECTION_POOLING 設定為 SQL_CP_OFF，就會停用連接共用。  
  
2.  藉由呼叫**SQLAllocHandle**並將*HandleType*引數設定為 SQL_HANDLE_ENV，來配置環境。 此呼叫所配置的環境將會是隱含的共用環境，因為已啟用連接共用。 不過，在此環境上呼叫具有 SQL_HANDLE_DBC *HandleType*的**SQLAllocHandle**之前，不會決定要使用的環境。  
  
3.  藉由呼叫**SQLAllocHandle**並將*InputHandle*設為 SQL_HANDLE_DBC，並將*InputHandle*設定為配置給連接共用的環境控制碼，以配置連接。 驅動程式管理員會嘗試尋找符合應用程式所設定之環境屬性的現有環境。 如果沒有這類環境存在，則會建立一個，其中會有1個參考計數（由驅動程式管理員維護）。 如果找到相符的共用環境，環境就會傳回到應用程式，而且其參考計數會遞增。 （在呼叫**SQLConnect**或**SQLDriverConnect**之前，驅動程式管理員不會決定要使用的實際連接）。  
  
4.  呼叫**SQLConnect**或**SQLDriverConnect**來進行連接。 驅動程式管理員會使用**SQLConnect**呼叫中的連接選項（或**SQLDriverConnect**呼叫中的連接關鍵字），以及在連線配置之後所設定的連接屬性，來判斷應該使用集區中的連接。  
  
    > [!NOTE]  
    >  要求的連接如何與共享的連接相符，是由 SQL_ATTR_CP_MATCH 環境屬性所決定。 如需詳細資訊，請參閱[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)。  
  
     使用連接共用的 ODBC 應用程式應該在應用程式初始化期間呼叫[CoInitializeEx](https://go.microsoft.com/fwlink/?LinkID=116307) ，並在應用程式關閉時呼叫[CoUninitialize](https://go.microsoft.com/fwlink/?LinkId=116310) 。  
  
5.  使用連接完成時，會呼叫**SQLDisconnect** 。 連接會傳回到連線集區，並可供重複使用。  
  
 如需深入討論，請參閱[Microsoft 資料存取元件中的](https://go.microsoft.com/fwlink/?LinkId=120776)共用。  
  
## <a name="connection-pooling-considerations"></a>連接共用考慮  
 使用 SQL 命令（而非透過 ODBC API）執行下列任何動作，可能會影響連接的狀態，並在連接共用為使用中時造成未預期的問題：  
  
-   開啟連接並變更預設的資料庫。  
  
-   使用 SET 語句來變更任何可設定的選項（包括 SET ROWCOUNT、ANSI_Null、IMPLICIT_TRANSACTIONS、執行程式表、STATISTICS、TEXTSIZE 和 DATEFORMAT）。  
  
-   建立臨時表和預存程式。  
  
 如果任何這些動作都是在 ODBC API 外部執行，則使用該連接的下一個人員將會自動繼承先前的設定、資料表或程式。  
  
> [!NOTE]  
>  不預期線上狀態中會出現某些設定。 您應該一律在應用程式中設定線上狀態，並確保應用程式會移除任何未使用的連接共用設定。  
  
## <a name="driver-aware-connection-pooling"></a>可感知驅動程式的連接共用  
 從 Windows 8 開始，ODBC 驅動程式可以更有效率地使用集區中的連接。 如需詳細資訊，請參閱可[感知驅動程式的連接](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)共用。  
  
## <a name="see-also"></a>另請參閱  
 [連接到資料來源或驅動程式](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)   
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Microsoft 資料存取元件中的共用](https://go.microsoft.com/fwlink/?LinkId=120776)
