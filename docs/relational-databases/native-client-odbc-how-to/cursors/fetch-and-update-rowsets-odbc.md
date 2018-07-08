---
title: 提取和更新資料列集 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- rowsets [ODBC]
ms.assetid: cf0eb3b4-8b72-49fc-a845-95edc360cf93
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 364647bdd5fe1d5c28a2dce9d1a105d908470d76
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37413097"
---
# <a name="fetch-and-update-rowsets-odbc"></a>提取和更新資料列集 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

    
### <a name="to-fetch-and-update-rowsets"></a>提取和更新資料列集  
  
1.  （選擇性） 呼叫[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) with POSITIONED，若要變更資料列集中的資料列 (R) 數目。  
  
2.  呼叫[SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401)或是[SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)取得資料列集。  
  
3.  如果使用繫結資料行，請將繫結資料行緩衝區中目前可用的資料值和資料長度用於資料列集。  
  
     如果使用未繫結的資料行，每個資料列呼叫[SQLSetPos](http://go.microsoft.com/fwlink/?LinkId=58407)利用 SQL_POSITION 來設定資料指標位置，然後針對每個未繫結的資料行：  
  
    -   呼叫[SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md)一或多次，以取得資料在最後一個繫結的資料列集的資料行之後，未繫結資料行。 若要呼叫[SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md)應該遞增資料行編號的順序。  
  
    -   呼叫 [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) 多次，以便從 text 或 image 資料行取得資料。  
  
4.  設定任何資料執行中的 text 或 image 資料行。  
  
5.  呼叫[SQLSetPos](http://go.microsoft.com/fwlink/?LinkId=58407)或是[SQLBulkOperations](http://go.microsoft.com/fwlink/?LinkId=58398)若要設定資料指標位置，重新整理、 更新、 刪除或加入資料列集內的資料列。  
  
     如果資料執行中的 text 或 image 資料行用於更新或加入作業，請處理它們。  
  
6.  （選擇性） 執行定位的更新或刪除陳述式，指定資料指標名稱 (可從[SQLGetCursorName](../../../relational-databases/native-client-odbc-api/sqlgetcursorname.md)) 和相同的連接上使用不同的陳述式控制代碼。  
  
## <a name="see-also"></a>另請參閱  
 [使用資料指標使用說明主題&#40;ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/cursors/using-cursors-how-to-topics-odbc.md)  
  
  
