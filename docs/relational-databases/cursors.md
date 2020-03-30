---
title: 資料指標 | Microsoft Docs
ms.custom: ''
ms.date: 03/11/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- results [SQL Server], cursors
- Transact-SQL cursors, about cursors
- cursors [SQL Server]
- data access [SQL Server], cursors
- result sets [SQL Server], cursors
- requesting cursors
- cursors [SQL Server], about cursors
ms.assetid: e668b40c-bd4d-4415-850d-20fc4872ee72
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a053f49a6ab3b42e31c5b71c2d2d558ea3170440
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "79112333"
---
# <a name="cursors"></a>資料指標
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  關聯式資料庫中的作業會針對完整的資料列集運作。 例如，由 `SELECT` 陳述式所傳回的資料列集包括所有滿足陳述式 `WHERE` 子句之條件的資料列。 由陳述式傳回的完整資料列稱為結果集。 應用程式 (尤其是互動式線上應用程式) 不一定能夠以一個單位有效地運用整個結果集。 這些應用程式需要一個機制，一次運用一個資料列或小型資料列區塊。 資料指標就是一種結果集的擴充，提供此種機制。  
  
 資料指標擴充結果處理的方式是：  
  
-   允許定位於結果集中的特定資料列。  
  
-   從結果集的目前位置，擷取一個資料列或資料列區塊。  
  
-   支援結果集目前位置上資料列的資料修改。  
  
-   支援以不同可見性層級來檢視其他使用者對結果集所呈現的資料庫資料所作的變更。  
  
-   讓指令碼、預存程序和觸發程序中的 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式能夠存取結果集中的資料。  
  
> [!TIP]
> 在某些情況下，如果資料表上有主索引鍵，`WHILE` 迴圈可用來取代資料指標，而不會產生資料指標的負荷。
> 不過，有些情況不僅無法避免資料指標，而且實際上也需要它們。 在這種情況下，如果沒有需要根據資料指標來更新資料表，則使用「流管」  資料指標，這表示[且唯讀](#forward-only)的指標。
  
## <a name="cursor-implementations"></a>實作資料指標  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 支援三個資料指標實作。  
  
### <a name="transact-sql-cursors"></a>Transact-SQL 資料指標  
[!INCLUDE[tsql](../includes/tsql-md.md)] 資料指標是以 `DECLARE CURSOR` 語法為基礎，主要用於 [!INCLUDE[tsql](../includes/tsql-md.md)] 指令碼、預存程序和觸發程序。 [!INCLUDE[tsql](../includes/tsql-md.md)] 資料指標會在伺服器上實作，而且由用戶端傳送給伺服器的 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式所管理。 資料指標也可存在批次、預存程序或觸發程序內。  
  
### <a name="application-programming-interface-api-server-cursors"></a>應用程式開發介面 (Application Programming Interface，API) 伺服端資料指標  
API 指標可支援 OLE DB 和 ODBC 中的 API 資料指標函數。 API 伺服端資料指標實作在伺服端上。 每次用戶端應用程式呼叫 API 資料指標函數時， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client OLE DB 提供者或 ODBC 驅動程式都會將要求傳遞至伺服器，以依照 API 伺服端資料指標執行。  
  
### <a name="client-cursors"></a>用戶端資料指標  
用戶端資料指標是由 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式以及實作 ADO API 的 DLL 在內部實作。 用戶端資料指標是透過快取用戶端上的整個結果集資料列來實作。 每次用戶端應用程式呼叫 API 資料指標函數時， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式或 ADO DLL 都會在用戶端上快取的結果集資料列上執行資料指標作業。  
  
## <a name="type-of-cursors"></a>資料指標的類型  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 支援四種資料指標類型。 

> [!NOTE]
> 資料指標可能會利用 tempdb 工作資料表。 就如同溢出的彙總或排序作業，這會發生在 I/O 中，且為潛在的效能瓶頸。 `STATIC` 資料指標從起始就會使用工作資料表。 如需詳細資訊，請參閱[查詢處理架構指南中的工作資料表](../relational-databases/query-processing-architecture-guide.md#worktables)。

### <a name="forward-only"></a>順向  
順向資料指標指定為 `FORWARD_ONLY` 和 `READ_ONLY`，且不支援捲動。 這也稱為「流管」  資料指標，並只支援以循序方式從資料指標的開始到結尾擷取資料列。 提取資料列之前，不會從資料庫擷取那些資料列。 從資料指標提取資料列時，可看見目前使用者執行或其他使用者認可的所有 `INSERT`、`UPDATE` 和 `DELETE` 陳述式的作用對結果集資料列所產生的影響。  
  
 因為無法逆向捲動資料指標，提取資料列之後對資料庫中資料列所進行的大部分變更，都無法經由資料指標看見。 如果已修改用來判斷結果集之資料列位置的值 (例如更新叢集索引所涵蓋的資料行)，就可以經由資料指標看到修改的值。  
  
 雖然資料庫 API 資料指標模型會將順向資料指標視為不同的資料指標類型，但是 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 並不會。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會將順向和捲動視為可以套用至靜態、索引鍵集驅動和動態資料指標的選項。 [!INCLUDE[tsql](../includes/tsql-md.md)] 資料指標支援順向、靜態、索引鍵集驅動和動態資料指標。 資料庫 API 資料指標模式會假設靜態、索引鍵集驅動和動態資料指標一律可以捲動。 當資料庫 API 資料指標屬性 (Attribute 或 Property) 設為順向時， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會將此資料指標實作為順向動態資料指標。  
  
### <a name="static"></a>靜態  
 資料指標開啟時，靜態資料指標的完整結果集會內建於 **tempdb** 。 資料指標開啟的同時，靜態資料指標會將結果集的原貌展現出來。 靜態資料指標可以偵測少量的變更或是沒有變更，但是在捲動時所耗用的資源相當少。  
  
即使資料庫中的變更影響結果集的成員資格，或構成結果集的資料列之資料行數值有所變動時，此類資料指標並不會反映出其中的變更。 靜態資料指標並不會將資料指標開啟後插入資料庫的新資料列顯示出來，即使資料列符合資料指標 `SELECT` 陳述式的搜尋條件。 如果構成結果集的資料列被其他使用者更新，新資料值不會顯示在靜態資料指標上。 靜態資料指標會顯示資料指標開啟後從資料庫刪除的資料列。 總結以上，靜態資料指標中並不會反映出 `UPDATE`、`INSERT` 或 `DELETE` 作業帶來的變動 (除非資料指標經過關閉後重新開啟)，即使是使用同一連接開啟資料指標後的修改也不顯示。  
  
> [!NOTE]
> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 靜態資料指標永遠是唯讀的。  
  
> [!NOTE]
> 因為靜態資料指標的結果集是儲存在 **tempdb** 中的工作資料表，所以結果集中的資料列大小不可超過 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料表的資料列大小的上限。  
> 如需詳細資訊，請參閱[查詢處理架構指南中的工作資料表](../relational-databases/query-processing-architecture-guide.md#worktables)。 如需最大資料列大小的詳細資訊，請參閱 [SQL Server 的最大容量規格](../sql-server/maximum-capacity-specifications-for-sql-server.md)。  
  
[!INCLUDE[tsql](../includes/tsql-md.md)] 對靜態資料指標不太能區分。 部分資料庫 API 會將它們識別為快照集資料指標。  
  
### <a name="keyset"></a>索引鍵集  
開啟資料指標時，索引鍵集驅動資料指標中的成員資格和資料列順序是固定的。 索引鍵集驅動資料指標是由一組唯一的識別碼、索引鍵 (稱為索引鍵集) 所控制。 索引鍵是從結果集中唯一識別資料列的一組資料行建立的。 索引鍵集是一組取自所有資料列的索引鍵值，這些資料列會在開啟資料指標時對 `SELECT` 陳述式加以限定。 開啟資料指標時，會在 **tempdb** 中建立索引鍵集驅動資料指標的索引鍵集。  
  
### <a name="dynamic"></a>動態  
動態資料指標是靜態資料指標的相反。 捲動資料指標時，動態資料指標會反映其結果集中資料列的所有變更。 每回擷取時結果集之中資料列的資料值、順序和成員均會變動。 您可以透過資料指標看到所有使用者執行的全部 `UPDATE`、`INSERT` 和 `DELETE` 陳述式作業。 若是藉由使用 API 函式 (例如 **SQLSetPos**) 或 [!INCLUDE[tsql](../includes/tsql-md.md)] `WHERE CURRENT OF` 子句的資料指標來進行更新，則會馬上看到更新。 至於資料指標外的更新必須經過認可後才看得見，除非資料指標交易隔離等級設定為讀取未認可。 如需隔離等級的詳細資訊，請參閱 [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../t-sql/statements/set-transaction-isolation-level-transact-sql.md)。 
 
> [!NOTE]
> 動態資料指標計劃一律不會使用空間索引。  
  
## <a name="requesting-a-cursor"></a>要求資料指標  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 支援兩種要求資料指標的方法：  
  
-   [!INCLUDE[tsql](../includes/tsql-md.md)]  
  
     [!INCLUDE[tsql](../includes/tsql-md.md)] 語言支援使用 ISO 以後版本的資料指標語法。  
  
-   資料庫應用程式開發介面 (API) 資料指標函數  
  
     [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 支援以下資料庫 API 的資料指標功能：  
  
    -   ADO ([!INCLUDE[msCoName](../includes/msconame-md.md)] ActiveX 資料物件)  
  
    -   OLE DB  
  
    -   ODBC (開放式資料庫連接)  
  
應用程式不應將兩種要求資料指標的方法混合。 使用 API 指定資料指標行為的應用程式也不應執行 [!INCLUDE[tsql](../includes/tsql-md.md)] DECLARE CURSOR 陳述式來要求 [!INCLUDE[tsql](../includes/tsql-md.md)] 資料指標。 如果應用程式已將所有 API 資料指標屬性設回其預設值，只應執行 DECLARE CURSOR。  
  
如果沒有要求 [!INCLUDE[tsql](../includes/tsql-md.md)] 或 API 資料指標， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 預設會傳回完整的結果集 (亦即預設結果集) 給應用程式。  
  
## <a name="cursor-process"></a>資料指標處理過程  
 [!INCLUDE[tsql](../includes/tsql-md.md)] 資料指標和 API 資料指標具有不同的語法，但是下列一般處理過程適用於所有的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料指標：  
  
1.  使資料指標與 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式的結果集建立關聯，並定義資料指標的特性，例如可否更新資料指標中的資料列。  
  
2.  執行 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式，以填入資料指標。  
  
3.  擷取資料指標中您要檢視的資料列。 從資料指標擷取一個資料列或資料列區塊的作業稱為擷取 (Fetch)。 以順向 (Forward) 或逆向 (Backward) 擷取資料列的一系列擷取作業，稱為捲動 (Scroll)。  
  
4.  選擇性地在資料指標目前位置上的資料列執行修改作業 (更新或刪除)。  
  
5.  關閉資料指標。  
  
## <a name="related-content"></a>相關內容  
[資料指標行為](../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)    
[如何實作資料指標](../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
## <a name="see-also"></a>另請參閱  
[DECLARE CURSOR &#40;Transact-SQL&#41;](../t-sql/language-elements/declare-cursor-transact-sql.md)   
[資料指標 &#40;Transact-SQL&#41;](../t-sql/language-elements/cursors-transact-sql.md)   
[資料指標函數 &#40;Transact-SQL&#41;](../t-sql/functions/cursor-functions-transact-sql.md)   
[資料指標預存程序 &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/cursor-stored-procedures-transact-sql.md)   
[SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../t-sql/statements/set-transaction-isolation-level-transact-sql.md)    

  
