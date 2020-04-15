---
title: 使用 SQLSetPos 更新資料 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
- SQLSetPos function [ODBC], updating data
ms.assetid: e9625b59-06a0-4883-b155-b932ba7528d9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 16476a1e1007905f34ec2e70ce6032eb8d81fe7a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286158"
---
# <a name="updating-data-with-sqlsetpos"></a>使用 SQLSetPos 更新資料
應用程式可以使用**SQLSetPos**更新或刪除行集中的任何行。 呼叫**SQLSetPos**是建構和執行 SQL 語句的便捷替代方法。 它允許 ODBC 驅動程式支援定位更新,即使資料來源不支援定位 SQL 語句也是如此。 它是通過函數調用實現完整資料庫存取模式的一部分。  
  
 **SQLSetPos**在當前行集中運行,只能在調用**SQLFetchScroll**後使用。 應用程式指定要更新、刪除或插入的行數,驅動程式將從行集緩衝區檢索該行的新資料。 **SQLSetPos**還可用於指定的行指定為當前行,或從資料源刷新行集中的特定行。  
  
 行集大小由對**SQLSetStmtAttr**的調用設置,*屬性*參數為SQL_ATTR_ROW_ARRAY_SIZE。 但是 **,SQLSetPos**使用新的行集大小,僅在調用**SQLFetch**或**SQLFetchScroll**後。 例如,如果更改了行集大小,則調用**SQLSetPos,** 然後調用**SQLFetch**或**SQLFetchScroll,** 而**SQLSetPos 的**調用使用舊的行集大小,而**SQLFetch**或**SQLFetchScroll**使用新的行集大小。  
  
 資料列集中的第一個資料列是資料列號碼 1。 **SQLSetPos**中的*行編號*參數必須標識行集中的行;因此,在行集中,必須標識行數。也就是說,其值必須介於 1 和最近提取的行數(可能小於行集大小)之間。 如果*RowNumber*為 0,則該操作將應用於行集中的每一行。  
  
 由於與關係資料庫的大多數交互都是通過 SQL 完成的,因此**SQLSetPos**不受廣泛支援。 但是,驅動程式可以通過構造和執行**UPDATE**或**DELETE**語句來輕鬆類比它。  
  
 要確定**SQLSetPos**支援的操作,應用程式使用SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1或SQL_STATIC_CURSOR_ATTRIBUTES1資訊選項(取決於游標的類型)調用**SQLGetInfo。**  
  
 此章節包含下列主題。  
  
-   [使用 SQLSetPos 更新資料列集中的資料列](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)  
  
-   [使用 SQLSetPos 刪除資料列集中的資料列](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)
