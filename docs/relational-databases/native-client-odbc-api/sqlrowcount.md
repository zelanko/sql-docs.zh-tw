---
title: SQLRowCount |微軟文件
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3cfb76dbd1732e32238c484f589d3b4696ff89d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302297"
---
# <a name="sqlrowcount"></a>SQLRowCount
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  當參數值陣列綁定為語句執行時,如果任何參數值行在語句執行中生成錯誤條件 **,SQLRowCount**將返回SQL_ERROR。 不通過函數的*RowCountPtr*參數返回任何值。  
  
 應用程式可以利用 SQL_ATTR_PARAMS_PROCESSED_PTR 陳述式屬性擷取錯誤發生前所處理的參數數目。  
  
 此外，應用程式可以使用透過 SQL_ATTR_PARAM_STATUS_PTR 陳述式屬性繫結的狀態值陣列，擷取衝突參數資料列的陣列位移。 應用程式可以周遊狀態陣列來判斷所處理的資料列實際數目。  
  
 執行具有[!INCLUDE[tsql](../../includes/tsql-md.md)]OUTPUT 子句的插入、更新、刪除或 MERGE 語句時,SQLRowCount 不會返回受影響的行計數,直到使用 OUTPUT 子句生成的結果集中的所有行。 要消耗這些行,請致電 SQLFetch 或 SQLFetchScroll。 SQLResultCols 將返回 -1,直到使用所有結果行。 在 SQLFetch 或 SQLFetch 返回SQL_NO_DATA後,應用程式必須調用 SQLRowCount 以確定受影響的行數,然後再調用 SQLMoreResult 移動到下一個結果。  
  
## <a name="see-also"></a>另請參閱  
 [SQLRow( S) Count 函數](https://go.microsoft.com/fwlink/?LinkId=59367)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
