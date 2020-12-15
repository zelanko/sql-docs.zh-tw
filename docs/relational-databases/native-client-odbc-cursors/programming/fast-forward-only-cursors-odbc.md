---
description: 快速順向資料指標 (ODBC)
title: ODBC) 的快速 Forward-Only 資料指標 (|Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fast forward-only cursors
- forward-only cursors
- cursors [ODBC], fast forward-only
- ODBC cursors, fast forward-only
ms.assetid: 0707d07e-fc95-42ed-9280-b7e508ac8c62
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ef941028ffaf9c515b42d319bee522a03c928569
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97438588"
---
# <a name="fast-forward-only-cursors-odbc"></a>快速順向資料指標 (ODBC)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  當連接到的實例時 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式會針對順向、唯讀資料指標支援效能優化。 快速順向資料指標是由驅動程式和伺服器以非常類似於預設結果集的方式在內部實作。 除了具有高效能以外，快速順向資料指標還具有下列特性：  
  
-   不支援[SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) 。 結果集資料行必須繫結至程式變數。  
  
-   偵測到資料指標的結尾時，伺服器就會自動關閉資料指標。 應用程式仍然必須呼叫 [SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md) 或 [SQLFreeStmt](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md) (SQL_CLOSE) ，但驅動程式不需要將關閉要求傳送到伺服器。 這樣可節省透過網路與伺服器之間的往返。  
  
 應用程式會使用驅動程式特有的陳述式屬性 SQL_SOPT_SS_CURSOR_OPTIONS 來要求快速順向資料指標。 設定為 SQL_CO_FFO 時，就會啟用快速順向資料指標，但不啟用自動擷取。 設定為 SQL_CO_FFO_AF 時，則會一併啟用自動擷取選項。 如需自動擷取的詳細資訊，請參閱 [使用自動擷取搭配 ODBC 資料指標](../../../relational-databases/native-client-odbc-cursors/programming/using-autofetch-with-odbc-cursors.md)。  
  
 包含自動擷取的快速順向資料指標可用來透過與伺服器之間的一次往返，擷取小型結果集。 在這些步驟中， *n* 是要傳回的資料列數目：  
  
1.  將 SQL_SOPT_SS_CURSOR_OPTIONS 設定為 SQL_CO_FFO_AF。  
  
2.  將 SQL_ATTR_ROW_ARRAY_SIZE 設定為 *n* + 1。  
  
3.  將結果資料行系結至 *n* + 1 個元素的陣列 (如果有 *n* + 1 個數據列真的提取) ，就是安全的。  
  
4.  使用 **SQLExecDirect** 或 **SQLExecute** 來開啟資料指標。  
  
5.  如果傳回狀態為 SQL_SUCCESS，則呼叫 **SQLFreeStmt** 或 **SQLCloseCursor** 以關閉資料指標。 資料列的所有資料都將位於繫結的程式變數中。  
  
 使用這些步驟， **SQLExecDirect** 或 **SQLExecute** 會傳送資料指標開啟要求，並啟用自動擷取選項。 在收到來自用戶端的單一要求時，伺服器會：  
  
-   開啟資料指標。  
  
-   建立結果集並將資料列傳送至用戶端。  
  
-   由於資料列集大小設定為結果集的資料列數目加上 1，所以伺服器會偵測資料指標的結尾並關閉資料指標。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;的資料指標程式設計詳細資料 ](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
