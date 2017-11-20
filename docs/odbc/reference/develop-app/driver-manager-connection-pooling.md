---
title: "驅動程式管理員連接共用 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection pooling [ODBC]
- pooled connections [ODBC]
- connecting to driver [ODBC], connection pooling
- connecting to data source [ODBC], connection pooling
ms.assetid: ee95ffdb-5aa1-49a3-beb2-7695b27c3df9
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b589f7aa0e110767b7dca9be7aa82edee486b058
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="driver-manager-connection-pooling"></a>驅動程式管理員連接共用
連接共用可讓應用程式不需要重新建立每次使用的連接集區使用的連接。 一旦已經建立連接，並放在集區中，應用程式可以重複使用該連接，而不執行完整的連線程序。  
  
 使用共用的連接可能會導致效能大幅提升，因為應用程式可以儲存負擔參與建立連線。 這可以是透過網路連線的中介層應用程式或重複連線或中斷連線，例如網際網路應用程式的應用程式特別重要。  
  
 改善效能，除了連接共用架構可讓的環境和其相關聯的連接，以供單一處理序中的多個元件。 這表示相同的處理序中的獨立元件，可以不知道彼此的情況下彼此互動。 連接集區中的連線可以重複使用多個元件。  
  
> [!NOTE]  
>  發生 ODBC 2 的 ODBC 應用程式可以使用連接共用。*x*行為，只要應用程式可以呼叫*SQLSetEnvAttr*。 當使用連接共用時，應用程式必須執行 SQL 陳述式變更資料庫或資料庫，例如變更的內容\<*資料庫**名稱*>，變更資料來源所使用的目錄。  
  
 ODBC 驅動程式必須是完全安全的執行緒，而且連接不能有支援連接共用的執行緒相似性。 這表示驅動程式能夠處理任何執行緒上呼叫，在任何時間，而且可以連線，另一個執行緒上使用的連線，並在第三個執行緒上中斷連線的一個執行緒上。  
  
 連接集區會維護由驅動程式管理員。 當應用程式呼叫從集區描繪連接**SQLConnect**或**SQLDriverConnect**和應用程式進行呼叫時，傳回集區**SQLDisconnect**. 集區的大小，以動態方式會根據要求的資源配置。 此舉可縮小的閒置逾時根據： 如果連接為非作用中一段時間 （它尚未使用的連接中），則會移除從集區。 集區的大小只受到記憶體條件約束和伺服器的限制。  
  
 驅動程式管理員會決定是否應該根據傳入的引數使用特定的連接集區中**SQLConnect**或**SQLDriverConnect**，並根據連接屬性配置連接之後設定。  
  
 當驅動程式管理員會共用連接時，它必須能夠判斷連線是否仍正常才能送出連線。 否則，驅動程式管理員會保留在送出應用程式的無作用連接發生暫時性網路失敗時。 新的連接屬性已經定義在 ODBC 3*.x*: SQL_ATTR_CONNECTION_DEAD。 這是傳回 sql_cd_true; 或 SQL_CD_FALSE 唯讀連接屬性。 Sql_cd_true; 的值表示 SQL_CD_FALSE 的值表示連接仍在作用中時，連接到已遺失。 （符合較早版本的 ODBC 驅動程式也可以支援此屬性）。  
  
 驅動程式必須有效地實作這個選項，或者它會影響到使用連接共用的效能。 具體而言，呼叫以取得此連接屬性應該不會造成伺服器往返。 相反地，驅動程式應該只會傳回連線的最後已知的狀態。 無作用，如果最後一個往返於伺服器失敗，而不失效，如果最後一個路線成功連線。  
  
## <a name="remarks"></a>備註  
 如果連線已遺失 （透過 SQL_ATTR_CONNECTION_DEAD 報告），ODBC 驅動程式管理員將驅動程式中呼叫 SQLDisconnect 摧毀該連接。 新的連接要求可能無法找到可用的連接集區中。 最後，驅動程式管理員可能會讓新的連接，假設空的集區。  
  
 若要使用之連接集區，應用程式會執行下列步驟：  
  
1.  啟用連接共用，藉由呼叫**SQLSetEnvAttr** SQL_CP_ONE_PER_DRIVER 或 SQL_CP_ONE_PER_HENV 設定 SQL_ATTR_CONNECTION_POOLING 環境屬性。 應用程式配置共用的連接共用是啟用的環境之前，必須進行這個呼叫。 環境中的控制代碼呼叫**SQLSetEnvAttr**應該設定為 null，這可讓 SQL_ATTR_CONNECTION_POOLING 處理序層級屬性。 如果屬性設定為 SQL_CP_ONE_PER_DRIVER，每個驅動程式支援單一連接集區。 如果應用程式的運作方式與許多驅動程式和幾個環境，這可能是更有效率的情況，因為可能需要較少的比較。 如果設定為單一連接集區，SQL_CP_ONE_PER_HENV 支援每個環境。 如果您的環境與幾個驅動程式，應用程式運作，這可能是更有效率的情況，因為可能需要較少的比較。 藉由設定 SQL_ATTR_CONNECTION_POOLING SQL_CP_OFF 來停用連接共用。  
  
2.  藉由呼叫配置環境**SQLAllocHandle**與*HandleType*引數設定為 SQL_HANDLE_ENV。 這個呼叫所配置的環境將會隱含的共用的環境，因為已啟用連接共用。 不決定要使用的環境，不過，直到**SQLAllocHandle**與*HandleType*利用 SQL_HANDLE_DBC 的呼叫在這個環境。  
  
3.  藉由呼叫配置連接**SQLAllocHandle**與*InputHandle*設定為 SQL_HANDLE_DBC，而*InputHandle*設為配置環境控制代碼連接共用。 驅動程式管理員會嘗試尋找現有的環境符合應用程式所設定的環境屬性。 如果沒有這類環境存在，會建立一個，1 的參考計數 （在驅動程式管理員所維護）。 如果找到相符的共用的環境，則環境會傳回到應用程式和其參考計數會遞增。 (使用實際的連接不會決定之前由驅動程式管理員**SQLConnect**或**SQLDriverConnect**稱為。)  
  
4.  呼叫**SQLConnect**或**SQLDriverConnect**來進行連接。 驅動程式管理員會使用的連接選項的呼叫中**SQLConnect** (或連接關鍵字，在呼叫**SQLDriverConnect**) 和連接配置之後，設定連接屬性決定應使用哪個連接集區中。  
  
    > [!NOTE]  
    >  要求的連線共用連接至對應的方式取決於 SQL_ATTR_CP_MATCH 環境屬性。 如需詳細資訊，請參閱[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)。  
  
     使用連接共用的 ODBC 應用程式應該呼叫[CoInitializeEx](http://go.microsoft.com/fwlink/?LinkID=116307)應用程式初始化期間和[CoUninitialize](http://go.microsoft.com/fwlink/?LinkId=116310)應用程式關閉時。  
  
5.  呼叫**SQLDisconnect**完成連線。 連接傳回連接集區，而且會變成可供重複使用。  
  
 如需深入的討論，請參閱[Microsoft Data Access Components 中共用](http://go.microsoft.com/fwlink/?LinkId=120776)。  
  
## <a name="connection-pooling-considerations"></a>連接共用的考量  
 執行任何下列動作使用的 SQL 命令 （而非透過 ODBC API），可能會影響連接的狀態，而且使用中連接共用時，會造成無法預期的問題：  
  
-   開啟連接，並變更預設資料庫。  
  
-   若要變更任何可設定的選項 （包括 SET ROWCOUNT、 ANSI_NULL、 IMPLICIT_TRANSACTIONS、 計畫、 統計資料、 TEXTSIZE，與 DATEFORMAT） 中使用 SET 陳述式。  
  
-   建立暫存資料表和預存程序。  
  
 如果任何這些動作執行 ODBC API 之外下, 一步使用連接的人員會自動繼承先前的設定、 資料表或程序。  
  
> [!NOTE]  
>  不預期要出現在連接狀態的特定設定。 您一定要在您的應用程式中設定的連接狀態，並確保應用程式會移除任何未使用的連接共用的設定。  
  
## <a name="driver-aware-connection-pooling"></a>可感知驅動程式的連接共用  
 Windows 8 中從開始，ODBC 驅動程式可以使用連線集區中更有效率。 如需詳細資訊，請參閱[感知驅動程式的連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。  
  
## <a name="see-also"></a>另請參閱  
 [連接到資料來源或驅動程式](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)   
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Microsoft Data Access Components 中的共用](http://go.microsoft.com/fwlink/?LinkId=120776)

