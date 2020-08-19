---
description: 已建立結果集了嗎？
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 57b65c254f48d9c3f5078c3b2c1f576ae54d4740
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421382"
---
# <a name="was-a-result-set-created"></a>已建立結果集了嗎？
在大部分的情況下，應用程式設計人員會知道其應用程式執行的語句是否會建立結果集。 如果應用程式使用程式設計人員所撰寫的硬式編碼 SQL 語句，就會發生這種情況。 當應用程式在執行時間時建立 SQL 語句時，通常會發生這種情況：程式設計師可以輕鬆地包含程式碼，以旗標是否正在建立 **SELECT** 語句或 **INSERT** 語句。 在少數情況下，程式設計人員不可能知道語句是否會建立結果集。 如果應用程式提供使用者輸入和執行 SQL 語句的方法，這就是如此。 當應用程式在執行時間建立語句來執行程式時，也是如此。  
  
 在這種情況下，應用程式會呼叫 **SQLNumResultCols** 來判斷結果集中的資料行數目。 如果這是0，語句就不會建立結果集;如果是任何其他數位，則語句會建立結果集。  
  
 在準備或執行語句之後，應用程式可以隨時呼叫 **SQLNumResultCols** 。 不過，因為某些資料來源無法輕鬆地描述將由備妥的語句所建立的結果集，所以如果在語句備妥之後但在執行之前呼叫 **SQLNumResultCols** ，效能將會受到影響。  
  
 某些資料來源也支援判斷 SQL 語句在結果集中傳回的資料列數目。 若要這樣做，應用程式會呼叫 **SQLRowCount**。 根據 **SQLGetInfo**的呼叫所傳回的資料指標 (的型別，SQL_DYNAMIC_CURSOR_ATTRIBUTES2、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2、SQL_KEYSET_CURSOR_ATTRIBUTES2 或 SQL_STATIC_CURSOR_ATTRIBUTES2 選項的設定會指出資料列計數所代表的結果) 。 如果傳回的資料列計數是精確、近似或完全無法使用，則此位元遮罩會指出每個資料指標類型。 靜態或索引鍵集驅動資料指標的資料列計數是否受到透過 **SQLBulkOperations** 或 **SQLSetPos**所做的變更影響，或是藉由定位 update 或 delete 語句所影響，取決於先前所列的相同選項引數所傳回的其他位。 如需詳細資訊，請參閱 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 函數描述。
