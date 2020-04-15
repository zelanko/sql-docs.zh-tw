---
title: 分配存儲 |微軟文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- column-wise binding [ODBC]
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- SQLBindCol function
- storing data [ODBC]
- result sets [ODBC], storage
- SQL Server Native Client ODBC driver, data storage
- row-wise binding
- binding result sets [SQL Server Native Client]
- array binding
ms.assetid: 11c81955-5300-495f-925f-9256f2587b58
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 067abcfc8aa5bfd781e6656e3ced9f9e1e573e5f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297868"
---
# <a name="assigning-storage"></a>指派儲存體
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  應用程式可以在執行 SQL 陳述式之前或之後指派結果的儲存體。 如果應用程式先準備或執行 SQL 陳述式，它就可以查詢結果集的相關資訊，然後再指派結果的儲存體。 例如，如果結果集是未知的，應用程式就必須擷取資料行的數目，然後才能指派它們的儲存體。  
  
 要關聯資料列的儲存,應用程式呼叫[SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md)並傳遞它:  
  
-   要轉換資料的目標資料類型。  
  
-   資料之輸出緩衝區的位址。  
  
     應用程式必須配置這個緩衝區，而且緩衝區必須夠大，足以用轉換的格式來保存資料。  
  
-   輸出緩衝區的長度。  
  
     如果傳回的資料具有固定寬度 C (例如整數、實數或資料結構)，系統就會忽略此值。  
  
-   要傳回可用資料之位元組數目的儲存緩衝區位址。  
  
 應用程式也可以將結果集資料行繫結至程式變數的陣列，以便支援在區塊中提取結果集資料行。 陣列繫結有兩種不同的類型：  
  
-   當每個資料行繫結至自己的變數陣列時，就會完成資料行取向繫結。  
  
     按列方向綁定是透過調用[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)來指定的,*其屬性*設置為*SQL_ATTR_ROW_BIND_TYPE,ValuePtr*設置為SQL_BIND_BY_COLUMN。 所有陣列的元素數目都必須相同。  
  
-   當 SQL 陳述式的所有參數都是以單位的形式繫結至含有參數個別變數的結構陣列時，就會完成資料列取向繫結。  
  
     按行綁定透過調用**SQLSetStmtAttr**來指定 *,其中屬性*設定為SQL_ATTR_ROW_BIND_TYPE,ValuePtr 設定為包含將接收結果集列的變數的結構的*ValuePtr*大小。  
  
 應用程式也會將 SQL_ATTR_ROW_ARRAY_SIZE 設定為資料行或資料列陣列中的元素數目，並且設定 SQL_ATTR_ROW_STATUS_PTR 和 SQL_ATTR_ROWS_FETCHED_PTR。  
  
## <a name="see-also"></a>另請參閱  
 [處理結果&#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
