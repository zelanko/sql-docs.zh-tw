---
title: 驅動程式管理員連接池 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305819"
---
# <a name="driver-manager-connection-pooling"></a>驅動程式管理員連線共用
連接池使應用程式能夠使用連接池中的連接,而不需要為每個使用重新建立連接池。 創建連接並將其放置在池中後,應用程式可以重用該連接,而無需執行完整的連接過程。  
  
 使用池連接可以顯著提高性能,因為應用程式可以節省進行連接所涉及的開銷。 對於透過網路連接的中間層應用程式或重複連接和斷開連接的應用程式(如 Internet 應用程式)來說,這一點尤其重要。  
  
 除了性能提升之外,連接池體系結構還允許環境及其關聯連接在單個進程中由多個元件使用。 這意味著同一進程中的獨立元件可以相互交互,而不必相互瞭解。 連接池中的連接可以由多個元件反覆使用。  
  
> [!NOTE]
>  顯示 ODBC 2 的 ODBC 應用程式可以使用連接池。*x*行為,只要應用程式可以呼叫*SQLSetEnvAttr*。 使用連接池時,應用程式不得執行更改資料庫或資料庫上下文的 SQL 語句,\<例如更改*資料庫名稱*>更改数据源使用的目录。  


 ODBC 驅動程式必須完全線程安全,並且連接不能具有線程關聯以支援連接池。 這意味著驅動程式能夠隨時處理任何線程上的調用,並能夠在一個線程上連接、在另一個線程上使用連接以及斷開第三個線程的連接。  
  
 連接池由驅動程式管理器維護。 當應用程式呼叫**SQLConnect**或**SQLDriverConnect**時,連接從池中繪製,並在應用程式呼叫**SQLDisconnect**時傳回到池中。 池的大小根據請求的資源分配動態增長。 它根據非活動超時收縮:如果連接在一段時間內處於非活動狀態(在連接中未使用),則從池中刪除連接。 池的大小僅受記憶體約束和伺服器上的限制的限制。  
  
 驅動程式管理員確定是否應根據**SQLConnect**或**SQLDriverConnect**中傳遞的參數以及分配連接後設定的連接屬性使用池中的特定連接。  
  
 當驅動程式管理器正在池連接時,它需要能夠在分發連接之前確定連接是否仍在工作。 否則,每當發生暫時性網路故障時,驅動程式管理器會繼續將死連接分發到應用程式。 在 ODBC 3 *.x*: SQL_ATTR_CONNECTION_DEAD 中定義了新的連接屬性。 這是一個唯讀連接屬性,返回SQL_CD_TRUE或SQL_CD_FALSE。 值SQL_CD_TRUE表示連接已丟失,而值SQL_CD_FALSE表示連接仍然處於活動狀態。 (符合早期版本的 ODBC 的驅動程式也可以支援此屬性。  
  
 驅動程式必須有效地實現此選項,否則將損害連接池性能。 具體而言,獲取此連接屬性的調用不應導致伺服器的往返行程。 相反,驅動程式應僅返回連接的最後已知狀態。 如果上次伺服器訪問失敗,則連接已死,如果上次訪問成功,連接不會死。  
  
## <a name="remarks"></a>備註  
 如果連接已丟失(通過SQL_ATTR_CONNECTION_DEAD報告),ODBC 驅動程式管理員將透過在驅動程式中呼叫 SQLDisconnect 來破壞該連接。 新的連接請求可能無法在池中找到可用的連接。 最終,假設池為空,驅動程式管理器可能會建立新的連接。  
  
 要使用連線池,應用程式將執行以下步驟:  
  
1.  通過調用**SQLSetEnvAttr**將SQL_ATTR_CONNECTION_POOLING環境屬性設置為SQL_CP_ONE_PER_DRIVER或SQL_CP_ONE_PER_HENV,從而啟用連接池。 在應用程式分配要為其啟用連接池的共用環境之前,必須進行此調用。 對**SQLSetEnvAttr**調用中的環境句柄應設置為 null,這使得SQL_ATTR_CONNECTION_POOLING進程級屬性。 如果屬性設置為SQL_CP_ONE_PER_DRIVER,則每個驅動程式支援單個連接池。 如果應用程式與許多驅動程式和很少的環境一起工作,則這可能更有效率,因為可能需要較少的比較。 如果設置為SQL_CP_ONE_PER_HENV,則每個環境都支援單個連接池。 如果應用程式與許多環境和很少的驅動程式一起工作,則這可能更有效率,因為可能需要較少的比較。 通過將SQL_ATTR_CONNECTION_POOLING設置為SQL_CP_OFF,將禁用連接池。  
  
2.  通過將*句柄類型*參數設置為SQL_HANDLE_ENV調用**SQLAllocHandle**來分配環境。 此調用分配的環境將是隱式共用環境,因為連接池已啟用。 但是,在此環境中調用具有*SQL_HANDLE_DBC*的**SQLAllocHandle,** 才能確定要使用的環境。  
  
3.  通過將**SQLAllocHandle**與*輸入句柄*設置為 SQL_HANDLE_DBC,並將*InputHandle*設置為分配給連接池的環境句柄來分配連接。 驅動程式管理員嘗試尋找與應用程式設定的環境屬性匹配的現有環境。 如果不存在此類環境,則創建一個環境,引用計數(由驅動程式管理器維護)為 1。 如果找到匹配的共用環境,環境將返回到應用程式,其引用計數將遞增。 (在調用**SQLConnect**或**SQLDriverConnect**之前,驅動程式管理員不會確定要使用的實際連接。  
  
4.  調用**SQLConnect**或**SQLDriverConnect**進行連接。 驅動程式管理員在調用**SQLConnect**時使用連接選項(或**SQLDriverConnect**呼叫中的連接關鍵字)和連接分配後設定的連接屬性來確定應在池中使用哪個連接。  
  
    > [!NOTE]  
    >  請求的連接如何與池連接匹配由SQL_ATTR_CP_MATCH環境屬性確定。 有關詳細資訊,請參閱[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)。  
  
     使用連線池的 ODBC 應用程式應在應用程式初始化期間呼叫[Co 初始化 Ex,](https://go.microsoft.com/fwlink/?LinkID=116307)並在應用程式關閉時呼叫[CoUn 初始化](https://go.microsoft.com/fwlink/?LinkId=116310)。  
  
5.  使用連線完成後呼叫**SQL 中斷連線**。 連接返回到連接池,並可供重用。  
  
 有關深入討論,請參閱在[Microsoft 資料存取元件中進行池化](https://go.microsoft.com/fwlink/?LinkId=120776)。  
  
## <a name="connection-pooling-considerations"></a>連線池注意事項  
 使用 SQL 指令執行以下任一動作(而不是透過 ODBC API)可能會影響連線的狀態,並在連接池處於活動狀態時導致意外問題:  
  
-   打開連接並更改默認資料庫。  
  
-   使用 SET 語句更改任何可設定選項(包括設置、ANSI_NULL、IMPLICIT_TRANSACTIONS、SHOWPLAN、STATISTICS、TEXTSIZE 和日期格式)。  
  
-   創建臨時表和存儲過程。  
  
 如果其中任何一個操作是在 ODBC API 之外執行的,則使用連接的下一個人將自動繼承以前的設置、表或過程。  
  
> [!NOTE]  
>  不要期望某些設置處於連接狀態。 應始終在應用程式中設置連接狀態,並確保應用程式刪除任何未使用的連接池設置。  
  
## <a name="driver-aware-connection-pooling"></a>可感知驅動程式的連接共用  
 從 Windows 8 開始,ODBC 驅動程式可以更有效地使用池中的連接。 有關詳細資訊,請參閱[驅動程式感知連接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。  
  
## <a name="see-also"></a>另請參閱  
 [連接到資料來源或驅動程式](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)   
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [在 Microsoft 資料存取元件中進行池化](https://go.microsoft.com/fwlink/?LinkId=120776)
