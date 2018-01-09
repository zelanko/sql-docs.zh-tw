---
title: "僅向前快轉資料指標 (ODBC) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-cursors
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- fast forward-only cursors
- forward-only cursors
- cursors [ODBC], fast forward-only
- ODBC cursors, fast forward-only
ms.assetid: 0707d07e-fc95-42ed-9280-b7e508ac8c62
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b3e3a10930bb0cdd6dfb9c442ff7c548cb59ab92
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="fast-forward-only-cursors-odbc"></a>快速順向資料指標 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  當連接到的執行個體[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會針對順向、 唯讀資料指標支援效能最佳化。 快速順向資料指標是由驅動程式和伺服器以非常類似於預設結果集的方式在內部實作。 除了具有高效能以外，快速順向資料指標還具有下列特性：  
  
-   [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md)不支援。 結果集資料行必須繫結至程式變數。  
  
-   偵測到資料指標的結尾時，伺服器就會自動關閉資料指標。 應用程式仍然必須呼叫[SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md)或[SQLFreeStmt](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md)(SQL_CLOSE)，但是驅動程式不需要在關閉要求傳送至伺服器。 這樣可節省透過網路與伺服器之間的往返。  
  
 應用程式會使用驅動程式特有的陳述式屬性 SQL_SOPT_SS_CURSOR_OPTIONS 來要求快速順向資料指標。 設定為 SQL_CO_FFO 時，就會啟用快速順向資料指標，但不啟用自動擷取。 設定為 SQL_CO_FFO_AF 時，則會一併啟用自動擷取選項。 如需有關自動擷取選項的詳細資訊，請參閱[使用自動擷取搭配 ODBC 資料指標](../../../relational-databases/native-client-odbc-cursors/programming/using-autofetch-with-odbc-cursors.md)。  
  
 包含自動擷取的快速順向資料指標可用來透過與伺服器之間的一次往返，擷取小型結果集。 在這些步驟中，  *n* 是要傳回的資料列數目：  
  
1.  將 SQL_SOPT_SS_CURSOR_OPTIONS 設定為 SQL_CO_FFO_AF。  
  
2.  將 SQL_ATTR_ROW_ARRAY_SIZE 設定為 *n*  + 1。  
  
3.  將結果資料行繫結至陣列的 *n*  + 1 個元素 (為了安全起見如果 *n*  + 1 個資料列實際上提取)。  
  
4.  開啟資料指標，其中一種**SQLExecDirect**或**SQLExecute**。  
  
5.  如果傳回的狀態是 SQL_SUCCESS，然後呼叫**SQLFreeStmt**或**SQLCloseCursor**來關閉資料指標。 資料列的所有資料都將位於繫結的程式變數中。  
  
 這些步驟， **SQLExecDirect**或**SQLExecute**傳送資料指標開啟要求具有啟用自動擷取選項。 在收到來自用戶端的單一要求時，伺服器會：  
  
-   開啟資料指標。  
  
-   建立結果集並將資料列傳送至用戶端。  
  
-   由於資料列集大小設定為結果集的資料列數目加上 1，所以伺服器會偵測資料指標的結尾並關閉資料指標。  
  
## <a name="see-also"></a>請參閱  
 [資料指標程式設計詳細資料 &#40; ODBC &#41;](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
