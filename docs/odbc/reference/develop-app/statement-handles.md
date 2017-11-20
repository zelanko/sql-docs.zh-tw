---
title: "陳述式控制代碼 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 65d6d78b-a8c8-489a-9dad-f8d127a44882
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 64c949c8b3b3c794d6089ff159e597aeec02cfed
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="statement-handles"></a>陳述式控制代碼
A*陳述式*最容易想像成 SQL 陳述式，例如**選取\*從員工**。 不過，在陳述式是不只是 SQL 陳述式，其中包含所有與該 SQL 陳述式，例如任何結果集的陳述式所建立和執行陳述式中使用的參數相關聯的資訊。 陳述式甚至不必有應用程式定義的 SQL 陳述式。 例如，當目錄函數例如**SQLTables**執行上一個陳述式，它會執行預先定義的 SQL 陳述式會傳回一份資料表的名稱。  
  
 陳述式控制代碼來識別每個陳述式。 陳述式都與單一連線，而且可以有多個陳述式，在該連接上。 有些驅動程式限制它們支援; 使用中陳述式的數目SQL_MAX_CONCURRENT_ACTIVITIES 選項**SQLGetInfo**指定驅動程式支援在單一連接的多少作用中陳述式。 陳述式定義為*active*如果有暫止結果，其中結果是結果集或受影響的資料列計數**插入**，**更新**，或**刪除**陳述式或資料傳送至多個呼叫**SQLPutData**。  
  
 在一段程式碼會實作 ODBC （驅動程式管理員或驅動程式），陳述式控制代碼會識別包含陳述式的詳細資訊，例如結構：  
  
-   陳述式的狀態  
  
-   目前的陳述式層級診斷  
  
-   應用程式變數的位址繫結至陳述式的參數和結果集資料行  
  
-   目前設定的每個陳述式屬性  
  
 陳述式控制代碼會用於大部分的 ODBC 函數。 值得注意的是，它們用在函式來繫結參數和結果集資料行 (**SQLBindParameter**和**SQLBindCol**)、 準備和執行陳述式 (**SQLPrepare****SQLExecute**，和**SQLExecDirect**)，擷取中繼資料 (**SQLColAttribute**和**SQLDescribeCol**)，提取結果 (**SQLFetch**)，並擷取診斷 (**SQLGetDiagField**和**SQLGetDiagRec**)。 它們也可以用在目錄函數 (**SQLColumns**， **SQLTables**等等) 和一些其他功能。  
  
 陳述式控制代碼會配置與**SQLAllocHandle**且已釋放與**SQLFreeHandle**。

