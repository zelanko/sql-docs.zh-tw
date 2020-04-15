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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c171a154dd16a291c5dbe1dcade8c01ea95fb084
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294546"
---
# <a name="was-a-result-set-created"></a>已建立結果集了嗎？
在大多數情況下,應用程式程式師知道應用程式執行的語句是否會創建結果集。 如果應用程式使用程式師編寫的硬編碼 SQL 語句,則就是這種情況。 通常,當應用程式在運行時建構 SQL 語句時,通常就是這種情況:程式師可以輕鬆地包含標記正在構造**SELECT**語句還是**INSERT**語句的代碼。 在某些情況下,程式師不可能知道語句是否會創建結果集。 如果應用程式為使用者提供了一種輸入和執行 SQL 語句的方法,則為這種情況為 1。 當應用程式在運行時構造語句以執行過程時也是如此。  
  
 在這種情況下,應用程式調用**SQLNumResultCols**以確定結果集中的列數。 如果為 0,則語句未創建結果集;如果為 0,則語句未創建結果集。如果是任何其他數位,則語句確實創建了結果集。  
  
 在準備或執行語句後,應用程式可以隨時調用**SQLNumResultCols。** 但是,由於某些數據源無法輕鬆描述由準備好的語句創建的結果集,因此,如果在準備語句后但在執行語句之前調用**SQLNumResultCols,** 性能將受到影響。  
  
 某些數據源還支援確定 SQL 語句在結果集中返回的行數。 此應用程式呼叫**SQLRow( S) 。** 行計數表示的確切內容由調用**SQLGetInfo**返回的SQL_DYNAMIC_CURSOR_ATTRIBUTES2、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2、SQL_KEYSET_CURSOR_ATTRIBUTES2或SQL_STATIC_CURSOR_ATTRIBUTES2選項(取決於游標的類型)的設置指示。 此位掩碼指示每個游標類型返回的行計數是精確、近似還是根本不可用。 靜態或按鍵集驅動的遊標的行計數是否受通過**SQLBulk 操作**或**SQLSetPos**所做的更改或定位的更新或刪除語句的影響,取決於前面列出的相同選項參數返回的其他位。 有關詳細資訊,請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函數說明。
