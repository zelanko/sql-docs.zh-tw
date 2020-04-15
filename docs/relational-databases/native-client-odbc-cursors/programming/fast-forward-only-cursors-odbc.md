---
title: 只快進游標 (ODBC) |微軟文件
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 50d79875e0f3f661c0a959f50ce68c4f2761d186
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298413"
---
# <a name="fast-forward-only-cursors-odbc"></a>快速順向資料指標 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  連接到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的實體時,[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本機用戶端 ODBC 驅動程式支援僅轉發、唯讀游標的效能最佳化。 快速順向資料指標是由驅動程式和伺服器以非常類似於預設結果集的方式在內部實作。 除了具有高效能以外，快速順向資料指標還具有下列特性：  
  
-   [不支援 SQLGet 資料](../../../relational-databases/native-client-odbc-api/sqlgetdata.md)。 結果集資料行必須繫結至程式變數。  
  
-   偵測到資料指標的結尾時，伺服器就會自動關閉資料指標。 應用程式仍必須調用[SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md)或[SQLFreeStmt(SQL_CLOSE),](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md)但驅動程式不必將關閉的請求發送到伺服器。 這樣可節省透過網路與伺服器之間的往返。  
  
 應用程式會使用驅動程式特有的陳述式屬性 SQL_SOPT_SS_CURSOR_OPTIONS 來要求快速順向資料指標。 設定為 SQL_CO_FFO 時，就會啟用快速順向資料指標，但不啟用自動擷取。 設定為 SQL_CO_FFO_AF 時，則會一併啟用自動擷取選項。 關於自動擷取的詳細資訊,請參考使用[ODBC 游標使用自動提取](../../../relational-databases/native-client-odbc-cursors/programming/using-autofetch-with-odbc-cursors.md)。  
  
 包含自動擷取的快速順向資料指標可用來透過與伺服器之間的一次往返，擷取小型結果集。 在這些步驟中 *,n*是要返回的行數:  
  
1.  將 SQL_SOPT_SS_CURSOR_OPTIONS 設定為 SQL_CO_FFO_AF。  
  
2.  將SQL_ATTR_ROW_ARRAY_SIZE設置為*n* = 1。  
  
3.  將結果列綁定到*n* = 1 元素的陣列(如果實際提取*了 n* = 1 行,則要安全)。  
  
4.  使用**SQLExecDirect**或**SQLExecute**打開游標。  
  
5.  如果返回狀態為SQL_SUCCESS,則調用**SQLFreeStmt**或**SQLCloseCursor**關閉游標。 資料列的所有資料都將位於繫結的程式變數中。  
  
 通過這些步驟 **,SQLExecDirect**或**SQLExecute**會在啟用自動提取選項後發送游標打開請求。 在收到來自用戶端的單一要求時，伺服器會：  
  
-   開啟資料指標。  
  
-   建立結果集並將資料列傳送至用戶端。  
  
-   由於資料列集大小設定為結果集的資料列數目加上 1，所以伺服器會偵測資料指標的結尾並關閉資料指標。  
  
## <a name="see-also"></a>另請參閱  
 [游標程式設計詳細資訊&#40;ODBC&#41;](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
