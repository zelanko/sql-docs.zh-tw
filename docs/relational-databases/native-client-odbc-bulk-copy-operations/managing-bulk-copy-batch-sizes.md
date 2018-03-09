---
title: "管理大量複製批次大小 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-bulk-copy-operations
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, bulk copy
- ODBC, bulk copy operations
- batches [ODBC]
- bulk copy [ODBC], batch sizes
ms.assetid: 4b24139f-788b-45a6-86dc-ae835435d737
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ff6ef76f4cd59d845f95f17e8b072dc1311052f4
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="managing-bulk-copy-batch-sizes"></a>管理大量複製批次大小
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  大量複製作業中批次的主要用途是定義交易的範圍。 如果沒有設定批次大小，則大量複製函數會將整個大量複製作業視為一筆交易。 如果有設定批次大小，則每一個批次都構成一筆在批次完成時認可的交易。  
  
 如果大量複製在執行時沒有指定任何批次大小，而且發生了錯誤，則整個大量複製都會回復。 長時間執行的大量複製的復原可能要花一段很長的時間。 如果有設定批次大小，則大量複製會將每個批次視為一筆交易並認可每個批次。 如果發生錯誤，只需要回復最後一個沒有完成的批次。  
  
 批次大小也會影響鎖定負擔。 當執行大量複製針對[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，可以使用指定 TABLOCK 提示[bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)取得資料表鎖定，而非資料列鎖定。 對於整個大量複製作業而言，設定單一資料表鎖定所需的負擔最低。 如果沒有指定 TABLOCK，則會在個別的資料列上設定鎖定，而在大量複製期間維持所有鎖定的負擔可能會使效能降低。 因為鎖定只會在交易期間設定，所以指定批次大小可以藉由定期產生釋放目前所設定之鎖定的認可來解決這個問題。  
  
 在大量複製許多資料列時，組成批次的資料列數可能會對效能造成很大的影響。 批次大小的建議是依所執行之大量複製的類型而定。  
  
-   大量複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，請指定 TABLOCK 大量複製提示並設定大型的批次大小。  
  
-   如果沒有指定 TABLOCK，則將批次大小限制為小於 1,000 資料列。  
  
 當大量複製中，從資料檔時，藉由呼叫指定批次大小**bcp_control**使用 BCPBATCH 選項，然後再呼叫[bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md)。 當大量複製程式變數使用[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)和[bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)，批次大小由呼叫[bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md)之後呼叫[bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) *x*次，其中*x*批次中的資料列數。  
  
 除了指定交易大小外，批次也會影響資料列何時會透過網路傳送到伺服器。 大量複製函數通常會快取中的資料列**bcp_sendrow**直到網路封包填滿，然後再將完整的封包傳送到伺服器。 當應用程式呼叫**bcp_batch**，不過，目前的封包傳送到伺服器，不論它是否已滿。 使用很小的批次大小如果造成傳送許多部分填滿的封包到伺服器，則可能會使效能降低。 例如，呼叫**bcp_batch**之後每個**bcp_sendrow**會導致在不同的封包中傳送的每個資料列，而且除非資料列很大，會浪費每個封包中的空間。 雖然應用程式可以藉由呼叫變更大小，SQL Server 的網路封包的預設大小是 4 KB， [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)指定 SQL_ATTR_PACKET_SIZE 屬性。  
  
 批次的另一個副作用是每個批次會被視為未完成的結果集，直到它已完成但**bcp_batch**。 如果在批次未完成，而連接控制代碼上嘗試任何其他作業[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式會發出錯誤包含 SQLState ="HY000"以及以下的錯誤訊息字串：  
  
```  
"[Microsoft][SQL Server Native Client] Connection is busy with  
results for another hstmt."  
```  
  
## <a name="see-also"></a>另請參閱  
 [執行大量複製作業 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)   
 [資料的大量匯入及匯出 &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)  
  
  
