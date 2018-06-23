---
title: 提取和更新資料列集 (ODBC) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- rowsets [ODBC]
ms.assetid: cf0eb3b4-8b72-49fc-a845-95edc360cf93
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 740b549021c4ef5fc9253b8e774b3d5e38323b2d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36144717"
---
# <a name="fetch-and-update-rowsets-odbc"></a>提取和更新資料列集 (ODBC)
    
### <a name="to-fetch-and-update-rowsets"></a>提取和更新資料列集  
  
1.  （選擇性） 呼叫[SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) with POSITIONED 若要變更的資料列集中的資料列 (R) 數目。  
  
2.  呼叫[SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401)或[SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md)取得資料列集。  
  
3.  如果使用繫結資料行，請將繫結資料行緩衝區中目前可用的資料值和資料長度用於資料列集。  
  
     如果使用未繫結的資料行，每個資料列呼叫[SQLSetPos](http://go.microsoft.com/fwlink/?LinkId=58407)利用 SQL_POSITION 設定資料指標位置，然後針對每個未繫結的資料行：  
  
    -   呼叫[SQLGetData](../../native-client-odbc-api/sqlgetdata.md)上次繫結的資料列集的資料行之後，一或多次，以取得資料繫結資料行。 呼叫[SQLGetData](../../native-client-odbc-api/sqlgetdata.md)應該是為了增加資料行編號。  
  
    -   呼叫 [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) 多次，以便從 text 或 image 資料行取得資料。  
  
4.  設定任何資料執行中的 text 或 image 資料行。  
  
5.  呼叫[SQLSetPos](http://go.microsoft.com/fwlink/?LinkId=58407)或[SQLBulkOperations](http://go.microsoft.com/fwlink/?LinkId=58398)若要設定資料指標位置，重新整理、 更新、 刪除或加入資料列集中的資料列。  
  
     如果資料執行中的 text 或 image 資料行用於更新或加入作業，請處理它們。  
  
6.  （選擇性） 執行定位的更新或刪除陳述式，指定資料指標名稱 (可從[SQLGetCursorName](../../native-client-odbc-api/sqlgetcursorname.md)) 和相同的連接上使用不同的陳述式控制代碼。  
  
## <a name="see-also"></a>另請參閱  
 [使用資料指標的使用說明主題&#40;ODBC&#41;](using-cursors-how-to-topics-odbc.md)  
  
  