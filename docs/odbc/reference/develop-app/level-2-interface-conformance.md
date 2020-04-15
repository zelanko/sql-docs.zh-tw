---
title: 等級 2 介面一致性 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- level 2 interface conformance levels [ODBC]
- conformance levels [ODBC], interface
ms.assetid: 2dc87840-f2fe-43dd-9d7b-bd95523081d9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3ee57d716cbb93f855e1fd78d41bff62a681eb6c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306159"
---
# <a name="level-2-interface-conformance"></a>層級 2 介面一致性
2 級介面一致性級別包括 1 級介面一致性級別功能以及以下功能:  
  
|||  
|-|-|  
|201|使用資料庫表和檢視的三部分名稱。 (有關詳細資訊,請參閱[級別 1 介面一致性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)中的由兩部分組成的命名支援功能 101 。|  
|202|通過調用**SQLDescribeParam**來描述動態參數。|  
|203|不僅使用輸入參數,還使用輸出和輸入/輸出參數,以及存儲過程的結果值。|  
|204|通過在列號 0 上調用**SQLDescribeCol**和**SQLColAttribute,** 使用書籤(包括檢索書籤);通過調用 SQLFetchScroll,將*Fetch 方向*參數設置為SQL_FETCH_BOOKMARK;通過調用**SQLFetchScroll,** 即可獲取。並通過調用**SQLBulk 操作**,將*操作*參數設置為SQL_UPDATE_BY_BOOKMARK、SQL_DELETE_BY_BOOKMARK或SQL_FETCH_BY_BOOKMARK,通過書籤操作更新、刪除和提取。|  
|205|通過調用**SQLColumn 特權****、SQL 外鍵**和**SQLTable 特權**來檢索有關數據字典的高級資訊。|  
|206|使用 ODBC 函數而不是 SQL 語句執行其他資料庫操作,透過使用 SQL_ADD 呼叫**SQLBulk 操作,** 或者使用SQL_DELETE或SQL_UPDATE**調用 SQLSetPos。** (支援對**SQLSetPos**的呼叫,*將 LockType*參數設定為SQL_LOCK_EXCLUSIVE或SQL_LOCK_UNLOCK不是一致性級別的一部分,而是可選功能。|  
|207|為指定的單個語句啟用 ODBC 函數的非同步執行。|  
|208|通過調用**SQL 特別列**獲取表的SQL_ROWVER行標識列。 (有關詳細資訊,請參閱對**SQL 特殊列**的支援,其中*識別符類型*參數設置為 SQL_BEST_ROWID作為[核心介面一致性](../../../odbc/reference/develop-app/core-interface-conformance.md)中的要素 20。|  
|209|將SQL_ATTR_CONCURRENCY語句屬性設置為SQL_CONCUR_READ_ONLY以外的至少一個值。|  
|210|超時登錄請求和 SQL 查詢(SQL_ATTR_LOGIN_TIMEOUT和SQL_ATTR_QUERY_TIMEOUT)的能力。|  
|211|更改默認隔離級別的能力;使用「可序列化」隔離等級執行事務的能力。|
