---
title: "已將結果集建立嗎？ | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: result sets [ODBC], determining if created
ms.assetid: 4a83b8cb-2d57-4e64-b497-80bd587ee1f9
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e2777ca00cf9535e1c3ddb41eee11f0c5ba6eb5f
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="was-a-result-set-created"></a>已將結果集建立嗎？
在大部分情況下，應用程式設計人員知道他們的應用程式執行的陳述式是否會建立結果集。 如果應用程式會使用硬式編碼 SQL 陳述式寫入由程式設計人員，這會是大小寫。 通常的情況是當應用程式在執行階段建構 SQL 陳述式： 程式設計人員可以輕鬆地包含程式碼，加上旗標是否**選取**陳述式或**插入**正在陳述式建構。 在少數情況下，程式設計人員可能無法知道是否陳述式會建立結果集。 這是當應用程式可讓使用者輸入並執行 SQL 陳述式。 它也是如此應用程式建構在執行階段執行程序的陳述式時。  
  
 在這種情況下，應用程式呼叫**SQLNumResultCols**來判斷結果集中的資料行數目。 如果這是 0，陳述式未建立結果集;如果是其他任何數字，陳述式未建立結果集。  
  
 應用程式可以呼叫**SQLNumResultCols**在任何時間之後的陳述式會準備並執行。 不過，因為某些資料來源無法輕易地說明所建立的已備妥的陳述式的結果集，會降低效能如果**SQLNumResultCols**陳述式已備妥，但會在執行之前呼叫。  
  
 某些資料來源也支援決定 SQL 陳述式傳回結果集內的資料列數目。 若要這樣做，應用程式會呼叫**SQLRowCount**。 確實的資料列計數所代表的內容會以選項的設定 SQL_DYNAMIC_CURSOR_ATTRIBUTES2、 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2、 SQL_KEYSET_CURSOR_ATTRIBUTES2 或 SQL_STATIC_CURSOR_ATTRIBUTES2 （取決於資料指標的類型）呼叫所傳回的**SQLGetInfo**。 此位元遮罩表示每個資料指標類型，傳回的資料列計數是否正確、 近似值，或根本不是可用。 是否為靜態的資料列計數，或透過所做的變更會影響索引鍵集驅動資料指標**SQLBulkOperations**或**SQLSetPos**，或者藉由定位的 update 或 delete 陳述式，會取決於其他位元傳回先前所列的相同選項引數。 如需詳細資訊，請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函式描述。
