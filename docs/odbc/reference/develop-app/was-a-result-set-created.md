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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68078964"
---
# <a name="was-a-result-set-created"></a>已建立結果集了嗎？
在大部分情況下，應用程式設計人員會知道其應用程式執行的語句是否會建立結果集。 如果應用程式使用程式設計人員所撰寫的硬式編碼 SQL 語句，就會發生這種情況。 當應用程式在執行時間時，通常會發生這種情況：程式設計人員可以輕鬆地包含程式碼，以旗標是否正在建立**SELECT**語句或**INSERT**語句。 在少數情況下，程式設計人員可能不知道語句是否會建立結果集。 如果應用程式提供使用者輸入和執行 SQL 語句的方法，就會發生這種情況。 當應用程式在執行時間建立語句來執行程式時，也是如此。  
  
 在這種情況下，應用程式會呼叫**SQLNumResultCols**來判斷結果集中的資料行數目。 如果這個值為0，則語句不會建立結果集;如果是任何其他數位，語句就會建立結果集。  
  
 應用程式可以在準備或執行語句之後的任何時間呼叫**SQLNumResultCols** 。 不過，因為某些資料來源無法輕鬆地描述將由備妥的語句所建立的結果集，所以如果在語句準備好但執行之前呼叫**SQLNumResultCols** ，效能就會受到影響。  
  
 某些資料來源也支援判斷 SQL 語句在結果集中傳回的資料列數目。 若要這樣做，應用程式會呼叫**SQLRowCount**。 資料列計數所代表的確切內容，會以 SQL_DYNAMIC_CURSOR_ATTRIBUTES2、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2、SQL_KEYSET_CURSOR_ATTRIBUTES2 或 SQL_STATIC_CURSOR_ATTRIBUTES2 選項（根據游標的類型而定）的設定來表示，而這是由**SQLGetInfo**的呼叫所傳回。 這個位元遮罩會指出每個資料指標類型，傳回的資料列計數是精確、近似還是無法使用。 靜態或索引鍵集驅動資料指標的資料列計數是否會受到透過**SQLBulkOperations**或**SQLSetPos**所做的變更影響，或由定位 update 或 delete 語句所影響，取決於先前所列的相同 option 引數所傳回的其他位。 如需詳細資訊，請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函數描述。
