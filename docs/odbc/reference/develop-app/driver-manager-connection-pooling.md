---
description: 驅動程式管理員連線共用
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
ms.openlocfilehash: 4c3c2fecc26cf2d8bbf5d53598a7b28ce7db5612
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92195570"
---
# <a name="driver-manager-connection-pooling"></a>驅動程式管理員連線共用
連線共用可讓應用程式使用來自不需要重新建立以供每次使用之連接集區的連接。 一旦建立連線並將其放入集區之後，應用程式就可以重複使用該連接，而不需要執行完整的連接程式。  
  
 使用共用的連接可能會大幅提升效能，因為應用程式可以節省建立連接所需的額外負荷。 對於透過網路連線的仲介層應用程式，或重複連線和中斷連接的應用程式（例如網際網路應用程式），這可能特別重要。  
  
 除了效能提升之外，連接共用架構還可讓多個元件在單一進程中使用環境與其相關聯的連接。 這表示相同進程中的獨立元件可以彼此互動，而不需要彼此察覺。 多個元件可以重複使用連接集區中的連線。  
  
> [!NOTE]
>  ODBC 應用程式可以使用連接共用，以產生 ODBC 2。*x* 行為，只要應用程式可以呼叫 *SQLSetEnvAttr*。 使用連接共用時，應用程式不能執行 SQL 語句來變更資料庫或資料庫的內容，例如變更 \<*database name*> 變更資料來源所使用之目錄的。  


 ODBC 驅動程式必須是完全安全線程，而且連接不能有線程親和性來支援連接共用。 這表示驅動程式能夠隨時處理任何執行緒上的呼叫，並可在一個執行緒上連接、使用另一個執行緒上的連接，以及在第三個執行緒上中斷連接。  
  
 連接集區是由驅動程式管理員維護。 當應用程式呼叫 **SQLConnect** 或 **SQLDriverConnect** 時，會從集區中繪製連接，當應用程式呼叫 **SQLDisconnect**時，會將連接傳回集區。 集區的大小會根據要求的資源配置，以動態方式成長。 它會根據未活動的超時時間進行縮減：如果連接在一段時間內處於非使用中狀態 (未在連接) 中使用，則會從集區中移除。 集區的大小只受限於伺服器上的記憶體限制和限制。  
  
 驅動程式管理員會根據在 **SQLConnect** 或 **SQLDriverConnect**中傳遞的引數，以及在配置連線之後設定的連接屬性，判斷是否應該使用集區中的特定連接。  
  
 當驅動程式管理員共用連線時，它必須能夠判斷連接是否仍在運作中，再進行連線。 否則，當發生暫時性的網路失敗時，驅動程式管理員會持續將無法連線到應用程式。 ODBC 3.x： SQL_ATTR_CONNECTION_DEAD 中定義了新的連接*屬性。* 這是唯讀的連接屬性，可傳回 SQL_CD_TRUE 或 SQL_CD_FALSE。 值 SQL_CD_TRUE 表示連接已遺失，而值 SQL_CD_FALSE 表示連接仍在使用中。 符合舊版 ODBC 的 (驅動程式也可以支援此屬性。 )   
  
 驅動程式必須有效率地執行這個選項，否則它將會影響連接共用的效能。 具體而言，取得這個連接屬性的呼叫不應該導致往返于伺服器。 相反地，驅動程式應該只傳回連接的最後已知狀態。 如果最後一次到伺服器的行程失敗，連接就會失敗，如果最後一次行程成功，則不會失效。  
  
## <a name="remarks"></a>備註  
 如果 (透過 SQL_ATTR_CONNECTION_DEAD) 回報的連接遺失，ODBC 驅動程式管理員會在驅動程式中呼叫 SQLDisconnect，以終結該連接。 新的連接要求在集區中找不到可用的連接。 最後，如果集區是空的，驅動程式管理員可能會建立新的連接。  
  
 若要使用連接集區，應用程式會執行下列步驟：  
  
1.  藉由呼叫 **SQLSetEnvAttr** 來啟用連接共用，以將 SQL_ATTR_CONNECTION_POOLING 環境屬性設定為 SQL_CP_ONE_PER_DRIVER 或 SQL_CP_ONE_PER_HENV。 您必須在應用程式佈建要啟用連接共用的共用環境之前，進行此呼叫。 **SQLSetEnvAttr**呼叫中的環境控制碼應該設定為 null，這會使 SQL_ATTR_CONNECTION_POOLING 處理層級的屬性。 如果屬性設定為 SQL_CP_ONE_PER_DRIVER，每個驅動程式都支援單一連接集區。 如果應用程式適用于許多驅動程式和少數環境，這可能更有效率，因為可能需要較少的比較。 如果設定為 SQL_CP_ONE_PER_HENV，每個環境都支援單一連接集區。 如果應用程式適用于許多環境和少數驅動程式，則這可能更有效率，因為可能需要較少的比較。 藉由將 SQL_ATTR_CONNECTION_POOLING 設定為 SQL_CP_OFF 來停用連接共用。  
  
2.  藉由呼叫 **SQLAllocHandle** ，並將 *HandleType* 引數設定為 SQL_HANDLE_ENV 來配置環境。 此呼叫所配置的環境將會是隱含的共用環境，因為已啟用連接共用。 但是，在此環境中呼叫 **SQLAllocHandle** 與 *HandleType* 的 SQL_HANDLE_DBC 之前，並不會決定要使用的環境。  
  
3.  藉由呼叫 **SQLAllocHandle** ，並將 *InputHandle* 設定為 SQL_HANDLE_DBC，並將 *InputHandle* 設定為針對連接共用所配置的環境控制碼，以配置連接。 驅動程式管理員會嘗試尋找符合應用程式所設定之環境屬性的現有環境。 如果沒有這樣的環境，則會建立一個，其中有參考計數 (由驅動程式管理員) 1。 如果找到相符的共用環境，環境就會傳回給應用程式，且其參考計數會遞增。 在呼叫 **SQLConnect** 或 **SQLDriverConnect** 之前，驅動程式管理員不會決定要使用的實際連接。 )  (  
  
4.  呼叫 **SQLConnect** 或 **SQLDriverConnect** 來建立連接。 驅動程式管理員會在呼叫中使用連接選項 **SQLConnect** (或) **SQLDriverConnect** 呼叫中的連接關鍵字，以及連接配置之後設定的連接屬性，以決定應該使用集區中的哪個連接。  
  
    > [!NOTE]  
    >  要求的連接如何符合共用的連接，是由 SQL_ATTR_CP_MATCH 環境屬性所決定。 如需詳細資訊，請參閱 [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)。  
  
     使用連接共用的 ODBC 應用程式應該在應用程式初始化期間呼叫 [CoInitializeEx](/windows/win32/api/combaseapi/nf-combaseapi-coinitializeex) ，並在應用程式關閉時呼叫 [CoUninitialize](/windows/win32/api/combaseapi/nf-combaseapi-couninitialize) 。  
  
5.  在連接完成時呼叫 **SQLDisconnect** 。 連接會傳回連接集區，並可供重複使用。  
  
 如需深入討論，請參閱 [Microsoft 資料存取元件中的](/previous-versions/ms810829(v=msdn.10))共用。  
  
## <a name="connection-pooling-considerations"></a>連接共用考慮  
 使用 SQL 命令 (執行下列任何動作，而不是透過 ODBC API) 可能會影響連接的狀態，並在連接共用為作用中時造成未預期的問題：  
  
-   開啟連接並變更預設資料庫。  
  
-   使用 SET 語句來變更任何可設定的選項 (包括 SET ROWCOUNT、ANSI_Null、IMPLICIT_TRANSACTIONS、顯示計畫、STATISTICS、TEXTSIZE 和 DATEFORMAT) 。  
  
-   建立臨時表和預存程式。  
  
 如果任何這些動作是在 ODBC API 外部執行，則使用該連接的下一個人員將會自動繼承先前的設定、資料表或程式。  
  
> [!NOTE]  
>  在連接狀態中，不預期有某些設定存在。 您應一律在應用程式中設定連接狀態，並確定應用程式會移除任何未使用的連接共用設定。  
  
## <a name="driver-aware-connection-pooling"></a>可感知驅動程式的連接共用  
 從 Windows 8 開始，ODBC 驅動程式可以更有效率地使用集區中的連接。 如需詳細資訊，請參閱 [驅動程式感知連接](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)共用。  
  
## <a name="see-also"></a>另請參閱  
 [連接到資料來源或驅動程式](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)   
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Microsoft 資料存取元件中的共用](/previous-versions/ms810829(v=msdn.10))