---
title: SQLRowCount |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLRowCount function
ms.assetid: 967ed3d4-3d31-4485-ac92-027076ebc829
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2610d8691748e316396ccd7babcc0c9e4991aa29
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47796926"
---
# <a name="sqlrowcount"></a>SQLRowCount
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  繫結參數值的陣列針對陳述式執行時**SQLRowCount**會傳回 SQL_ERROR，如果任何資料列的參數值在陳述式執行產生錯誤狀況。 會傳回任何值，透過*RowCountPtr*函式的引數。  
  
 應用程式可以利用 SQL_ATTR_PARAMS_PROCESSED_PTR 陳述式屬性擷取錯誤發生前所處理的參數數目。  
  
 此外，應用程式可以使用透過 SQL_ATTR_PARAM_STATUS_PTR 陳述式屬性繫結的狀態值陣列，擷取衝突參數資料列的陣列位移。 應用程式可以周遊狀態陣列來判斷所處理的資料列實際數目。  
  
 當[!INCLUDE[tsql](../../includes/tsql-md.md)]利用 OUTPUT 子句的 INSERT、 UPDATE、 DELETE 或 MERGE 陳述式執行、 SQLRowCount 將不會傳回受到影響，直到已經耗用 OUTPUT 子句所產生之結果集中的所有資料列的資料列計數。 若要取用這些資料列，您呼叫 SQLFetch 或 SQLFetchScroll。 Sqlresultcols&lt 會傳回-1，直到已經耗用所有結果資料列。 SQLFetch 或 SQLFetchScroll 傳回 SQL_NO_DATA 之後，應用程式必須呼叫 SQLRowCount 來判斷受影響之前呼叫 SQLMoreResults 移至下一個結果資料列數目。  
  
## <a name="see-also"></a>另請參閱  
 [SQLRowCount 函數](http://go.microsoft.com/fwlink/?LinkId=59367)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
