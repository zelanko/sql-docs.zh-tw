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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 96a48d60cc0c127f41e6e1b79b9faf29ea4392cf
ms.sourcegitcommit: eacc2d979f1f13cfa07e0aa4887eb9d48824b633
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533819"
---
# <a name="driver-manager-connection-pooling"></a>驅動程式管理員連線共用
連接共用，可讓應用程式使用來自不需要重新建立每次使用的連接集區的連接。 一旦連線已建立並放在集區中，應用程式可以重複使用該連線，而不執行完整的連線程序。  
  
 使用共用的連接可能會導致效能大幅提升，因為應用程式可以儲存在連線上所涉及的額外負荷。 這可以是透過網路連線的中介層應用程式，或重複連線和中斷連線，例如網際網路應用程式的應用程式特別重要。  
  
 除了效能的提升，連接共用架構可讓環境和其相關聯的連接，以供在單一處理序中的多個元件。 這表示相同的處理序中的獨立元件，可以不知道彼此的存在與彼此互動。 連接集區中的連線可以重複使用由多個元件。  
  
> [!NOTE]
>  發生 ODBC 2 的 ODBC 應用程式可以使用連接共用。*x*行為，只要應用程式可以呼叫*SQLSetEnvAttr*。 使用連接共用時，應用程式必須執行 SQL 陳述式變更資料庫或資料庫，例如變更的內容\<*資料庫名稱*>，如此會變更資料所使用的目錄來源。  


 ODBC 驅動程式必須是完整的安全執行緒，而且連接不能有執行緒親和性，以支援連接共用。 這表示驅動程式能夠處理任何執行緒上呼叫，在任何時間，而且能夠連線到另一個執行緒，使用連接和中斷連線的第三個執行緒上的一個執行緒上。  
  
 連接集區會維護由驅動程式管理員。 當應用程式會呼叫從集區描繪連接**SQLConnect**或**SQLDriverConnect**當應用程式呼叫會傳回至集區**SQLDisconnect**. 集區的大小，以動態方式成長，根據要求的資源配置。 它會縮小根據閒置逾時：如果連接非使用中的一段時間 （它尚未使用的連接中），它會從集區中移除。 集區的大小只受到記憶體條件約束和伺服器上的限制。  
  
 驅動程式管理員會決定特定的連接集區中是否應根據傳入的引數**SQLConnect**或是**SQLDriverConnect**，並根據連接屬性配置連接之後設定。  
  
 當驅動程式管理員會共用連接時，它必須能夠判斷是否連線仍然運作正常，再交給連線。 否則，驅動程式管理員在保留交給應用程式的無作用連接發生暫時性網路失敗時。 在 ODBC 3 已定義新的連接屬性 *.x*:SQL_ATTR_CONNECTION_DEAD。 這是傳回 sql_cd_true; 或 SQL_CD_FALSE 唯讀連接屬性。 Sql_cd_true; 的值表示此連接已經遺失，雖然 SQL_CD_FALSE 的值表示連接是仍在作用中。 （符合舊版的 ODBC 驅動程式也可以支援這個屬性）。  
  
 驅動程式必須有效率地實作此選項，或是它將會影響他人連接共用的效能。 具體來說，若要取得此連接屬性的呼叫應該不會造成伺服器往返。 相反地，驅動程式應該只會傳回連線的最後一個已知的狀態。 如果最後一個往返於伺服器失敗，而不死，如果最後一個旅程成功連線。  
  
## <a name="remarks"></a>備註  
 如果連線已遺失 （透過 SQL_ATTR_CONNECTION_DEAD 報告），ODBC 驅動程式管理員將驅動程式中呼叫 SQLDisconnect 摧毀該連線。 新的連接要求可能找不到可用的連接集區中。 最後，驅動程式管理員可能會建立新的連線，假設空的集區。  
  
 若要使用之連接集區，應用程式會執行下列步驟：  
  
1.  啟用連接共用，藉由呼叫**SQLSetEnvAttr**設 SQL_CP_ONE_PER_DRIVER 或 SQL_CP_ONE_PER_HENV SQL_ATTR_CONNECTION_POOLING 環境屬性。 應用程式配置的連接共用是啟用共用的環境之前，必須進行此呼叫。 呼叫中的環境控制代碼**SQLSetEnvAttr**應設為 null，使得 SQL_ATTR_CONNECTION_POOLING 處理序層級屬性。 如果屬性設定為 SQL_CP_ONE_PER_DRIVER，每個驅動程式支援單一連接集區。 如果應用程式會使用許多驅動程式和幾個環境，這可能是更有效率的情況，因為可能需要較少的比較。 如果設為 SQL_CP_ONE_PER_HENV，單一連接集區的支援，則每個環境。 如果應用程式會使用您的環境和幾個驅動程式，這可能是更有效率的情況，因為可能需要較少的比較。 SQL_ATTR_CONNECTION_POOLING 設 SQL_CP_OFF 已停用連接共用。  
  
2.  配置環境，藉由呼叫**SQLAllocHandle**具有*HandleType*引數設定為 SQL_HANDLE_ENV。 這個呼叫所配置的環境將會隱含的共用的環境，因為已啟用連線共用。 不會決定要使用的環境，不過，直到**SQLAllocHandle**具有*HandleType*利用 SQL_HANDLE_DBC 的呼叫在這個環境上。  
  
3.  藉由呼叫配置連接**SQLAllocHandle**具有*InputHandle*設定為 SQL_HANDLE_DBC，而*InputHandle*設為配置環境控制代碼連接共用。 驅動程式管理員會嘗試尋找現有的環境符合應用程式設定的環境屬性。 如果沒有這類環境存在，會建立一個，1 參考計數 （在驅動程式管理員所維護）。 如果找到相符的共用的環境，則環境會傳回到應用程式和其參考計數會漸增。 (使用實際的連接不會決定透過驅動程式管理員直到**SQLConnect**或是**SQLDriverConnect**稱為。)  
  
4.  呼叫**SQLConnect**或是**SQLDriverConnect**來進行連線。 驅動程式管理員的呼叫中使用的連線選項**SQLConnect** (或連接關鍵字，在呼叫**SQLDriverConnect**) 和之後連接配置的連接屬性設定決定應使用哪個集區中的連接。  
  
    > [!NOTE]  
    >  要求的連線來共用連接如何比對是由 SQL_ATTR_CP_MATCH 環境屬性來決定。 如需詳細資訊，請參閱 < [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)。  
  
     使用連接共用的 ODBC 應用程式應該呼叫[CoInitializeEx](https://go.microsoft.com/fwlink/?LinkID=116307)應用程式初始化期間並[CoUninitialize](https://go.microsoft.com/fwlink/?LinkId=116310)應用程式關閉時。  
  
5.  呼叫**SQLDisconnect**完成與連線。 連接傳回連接集區，並可重複使用。  
  
 如需深入的討論，請參閱[Microsoft Data Access Components 中的共用](https://go.microsoft.com/fwlink/?LinkId=120776)。  
  
## <a name="connection-pooling-considerations"></a>連接共用的考量  
 執行任何下列動作使用的 SQL 命令 （而非透過 ODBC API），可能會影響連接的狀態，而且啟用連接共用時，會造成無法預期的問題：  
  
-   開啟連接，並變更預設資料庫。  
  
-   您可以使用 SET 陳述式來變更任何可設定的選項 （包括其 SET ROWCOUNT、 ANSI_NULL、 IMPLICIT_TRANSACTIONS、 執行程序表、 統計資料、 TEXTSIZE 和 DATEFORMAT）。  
  
-   建立暫存資料表和預存程序。  
  
 如果任何這些動作執行 ODBC API 之外下, 一步 會使用連接的人員會自動繼承先前的設定、 資料表或程序。  
  
> [!NOTE]  
>  預期不會出現在 連線狀態的特定設定。 您一律應在您的應用程式中設定的連接狀態，並確保應用程式會移除任何未使用的連接共用設定。  
  
## <a name="driver-aware-connection-pooling"></a>可感知驅動程式的連接共用  
 從 Windows 8 開始，ODBC 驅動程式可以使用連線集區中更有效率。 如需詳細資訊，請參閱 <<c0> [ 感知驅動程式的連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。  
  
## <a name="see-also"></a>另請參閱  
 [連接至資料來源或驅動程式](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)   
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Microsoft Data Access Components 中的共用](https://go.microsoft.com/fwlink/?LinkId=120776)
