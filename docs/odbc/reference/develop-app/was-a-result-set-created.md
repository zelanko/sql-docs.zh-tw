---
title: 已建立結果集了嗎？ | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], determining if created
ms.assetid: 4a83b8cb-2d57-4e64-b497-80bd587ee1f9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0f748e75f4e1579446b72b519356f2f649889fe0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078964"
---
# <a name="was-a-result-set-created"></a>已建立結果集了嗎？
在大部分情況下，應用程式設計人員會知道其應用程式執行的陳述式是否會建立結果集。 如果應用程式使用硬式編碼 SQL 陳述式寫入由程式設計師，這會是大小寫。 應用程式在執行階段建構 SQL 陳述式時，其乃常見情況：程式設計人員可以輕鬆地包含加上旗標的程式碼是否**選取** 陳述式或**插入**建構陳述式。 在少數情況下，程式設計人員可能不知道陳述式是否會建立結果集。 這是當應用程式提供方法，以讓使用者輸入並執行 SQL 陳述式，則為 true。 它也是如此應用程式建構的陳述式在執行程序的執行階段時。  
  
 在此情況下，應用程式會呼叫**SQLNumResultCols**來判斷結果集中的資料行數目。 如果這是 0，陳述式未建立結果集;如果是其他任何數字，該陳述式未建立結果集。  
  
 應用程式可以呼叫**SQLNumResultCols**在完成備妥陳述式，或執行後的任何時間。 不過，因為某些資料來源無法輕易地描述所建立的已備妥的陳述式的結果集，將會降低效能如果**SQLNumResultCols**備妥的陳述式之後，但會在執行之前呼叫。  
  
 某些資料來源也支援判斷 SQL 陳述式會傳回結果集中的資料列數目。 若要這樣做，應用程式會呼叫**SQLRowCount**。 完全的資料列計數所代表的意義會以選項的設定 SQL_DYNAMIC_CURSOR_ATTRIBUTES2、 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2、 SQL_KEYSET_CURSOR_ATTRIBUTES2，還是 SQL_STATIC_CURSOR_ATTRIBUTES2 （取決於資料指標類型）藉由呼叫傳回**SQLGetInfo**。 此位元遮罩表示針對每個資料指標類型，傳回的資料列計數是精確、 近似值，或根本不是可用。 是否為靜態的資料列計數，或透過所做的變更會影響索引鍵集驅動資料指標**SQLBulkOperations**或是**SQLSetPos**，或者藉由定位的 update 或 delete 陳述式，會取決於其他位元傳回先前所列的相同選項引數。 如需詳細資訊，請參閱 < [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函式描述。
