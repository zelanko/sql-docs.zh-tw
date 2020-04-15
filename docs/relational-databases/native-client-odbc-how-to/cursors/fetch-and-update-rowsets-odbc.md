---
title: 擷取與更新列集 (ODBC) |微軟文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowsets [ODBC]
ms.assetid: cf0eb3b4-8b72-49fc-a845-95edc360cf93
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cec50f99fe5f56c9ce613a8b12c0349823f6f461
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299571"
---
# <a name="fetch-and-update-rowsets-odbc"></a>提取和更新資料列集 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

    
### <a name="to-fetch-and-update-rowsets"></a>提取和更新資料列集  
  
1.  或者,使用SQL_ROW_ARRAY_SIZE調用[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)以更改行集中的行數 (R)。  
  
2.  呼叫[SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401)或[SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)獲取行集。  
  
3.  如果使用繫結資料行，請將繫結資料行緩衝區中目前可用的資料值和資料長度用於資料列集。  
  
     如果使用未綁定列,則每行將調用 SQLSetPos,SQL_POSITION設置游標位置;如果使用未綁定列,則調用[SQLSetPos,](https://go.microsoft.com/fwlink/?LinkId=58407)以設定游標位置。然後,對於每個未綁定列:  
  
    -   調用[SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md)一次或多次,以獲取行集最後一個綁定列之後的未綁定列的數據。 對[SQLGetData 的](../../../relational-databases/native-client-odbc-api/sqlgetdata.md)調用應按增加列號的順序進行。  
  
    -   呼叫 [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) 多次，以便從 text 或 image 資料行取得資料。  
  
4.  設定任何資料執行中的 text 或 image 資料行。  
  
5.  呼叫[SQLSetPos](https://go.microsoft.com/fwlink/?LinkId=58407)或[SQLBulk 操作](https://go.microsoft.com/fwlink/?LinkId=58398)以設定行集中的遊標位置、刷新、更新、刪除或添加行。  
  
     如果資料執行中的 text 或 image 資料行用於更新或加入作業，請處理它們。  
  
6.  或者,執行定位的更新或 DELETE 語句,指定游標名稱(可從[SQLGetCursorName](../../../relational-databases/native-client-odbc-api/sqlgetcursorname.md)中提供),並在同一連接上使用不同的語句句柄。  
  
## <a name="see-also"></a>另請參閱  
 [使用游標操作主題&#40;ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/cursors/using-cursors-how-to-topics-odbc.md)  
  
  
