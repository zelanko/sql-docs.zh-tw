---
title: 管理大量複製批次大小 |Microsoft Docs
description: 瞭解大量複製的批次大小如何定義交易的範圍，這會影響 SQL Server Native Client ODBC 中的錯誤行為和鎖定負荷。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, bulk copy
- ODBC, bulk copy operations
- batches [ODBC]
- bulk copy [ODBC], batch sizes
ms.assetid: 4b24139f-788b-45a6-86dc-ae835435d737
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f9be8ff6adc10b74ae176011dd1ae0f3a2b9cae1
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465019"
---
# <a name="managing-bulk-copy-batch-sizes"></a>管理大量複製批次大小
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  大量複製作業中批次的主要用途是定義交易的範圍。 如果沒有設定批次大小，則大量複製函數會將整個大量複製作業視為一筆交易。 如果有設定批次大小，則每一個批次都構成一筆在批次完成時認可的交易。  
  
 如果大量複製在執行時沒有指定任何批次大小，而且發生了錯誤，則整個大量複製都會回復。 長時間執行的大量複製的復原可能要花一段很長的時間。 如果有設定批次大小，則大量複製會將每個批次視為一筆交易並認可每個批次。 如果發生錯誤，只需要回復最後一個沒有完成的批次。  
  
 批次大小也會影響鎖定負擔。 對執行大量複製時 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，可以使用 [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) 來指定 TABLOCK 提示，以取得表鎖，而不是資料列鎖定。 對於整個大量複製作業而言，設定單一資料表鎖定所需的負擔最低。 如果沒有指定 TABLOCK，則會在個別的資料列上設定鎖定，而在大量複製期間維持所有鎖定的負擔可能會使效能降低。 因為鎖定只會在交易期間設定，所以指定批次大小可以藉由定期產生釋放目前所設定之鎖定的認可來解決這個問題。  
  
 在大量複製許多資料列時，組成批次的資料列數可能會對效能造成很大的影響。 批次大小的建議是依所執行之大量複製的類型而定。  
  
-   大量複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，請指定 TABLOCK 大量複製提示並設定大型的批次大小。  
  
-   如果沒有指定 TABLOCK，則將批次大小限制為小於 1,000 資料列。  
  
 從資料檔大量複製時，在呼叫 [bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md)之前，會使用 BCPBATCH 選項來呼叫 **bcp_control** ，以指定批次大小。 使用 [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)和 [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)從程式變數進行大量複製時，批次大小是藉由在呼叫 [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) *x* 次之後呼叫 [bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md)來控制，其中 *x* 是批次中的資料列數目。  
  
 除了指定交易大小外，批次也會影響資料列何時會透過網路傳送到伺服器。 大量複製函數通常會快取 **bcp_sendrow** 的資料列，直到網路封包填滿，然後再將完整的封包傳送至伺服器。 不過，當應用程式呼叫 **bcp_batch** 時，會將目前的封包傳送到伺服器，不論是否已填滿。 使用很小的批次大小如果造成傳送許多部分填滿的封包到伺服器，則可能會使效能降低。 例如，在每個 **bcp_sendrow** 之後呼叫 **bcp_batch** 會導致每個資料列都傳送至個別的封包，而且除非資料列很大，否則每個封包中都會浪費空間。 SQL Server 的預設網路封包大小為 4 KB，但應用程式可以藉由呼叫 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 指定 SQL_ATTR_PACKET_SIZE 屬性來變更大小。  
  
 批次的另一個副作用是，在使用 **bcp_batch** 完成之前，每個批次都會被視為未完成的結果集。 當批次未完成時，如果在連接控制碼上嘗試任何其他作業， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式會發出錯誤，其中 SQLState = "HY000" 和錯誤訊息字串：  
  
```  
"[Microsoft][SQL Server Native Client] Connection is busy with  
results for another hstmt."  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;執行大量複製作業 ](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)   
 [資料的大量匯入及匯出 &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)  
  
  
