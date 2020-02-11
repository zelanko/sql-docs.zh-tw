---
title: 使用 SQLSetPos 更新資料 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d2895ec765df3910dbbaa1e76ba1579e4afe5cca
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68091655"
---
# <a name="updating-data-with-sqlsetpos"></a>使用 SQLSetPos 更新資料
應用程式可以使用**SQLSetPos**來更新或刪除資料列集中的任何資料列。 呼叫**SQLSetPos**是用來建立和執行 SQL 語句的方便替代方式。 即使資料來源不支援定位的 SQL 語句，它也可讓 ODBC 驅動程式支援定點更新。 這是使用函式呼叫來達到完整資料庫存取的範例的一部分。  
  
 **SQLSetPos**會在目前的資料列集上運作，而且只能在呼叫**SQLFetchScroll**之後使用。 應用程式會指定要更新、刪除或插入的資料列數目，而驅動程式會從資料列集緩衝區中抓取該資料列的新資料。 **SQLSetPos**也可以用來指定指定的資料列做為目前的資料列，或從資料來源重新整理資料列集中的特定資料列。  
  
 資料列集大小是透過 SQL_ATTR_ROW_ARRAY_SIZE 的*屬性*引數呼叫**SQLSetStmtAttr**所設定。 不過， **SQLSetPos**只會在呼叫**SQLFetch**或**SQLFetchScroll**之後，才使用新的資料列集大小。 例如，如果資料列集大小已變更，則會呼叫**SQLSetPos** ，然後呼叫**SQLFetch**或**SQLFetchScroll** ，而**SQLFetch**或**SQLFetchScroll**會使用新的資料列集大小，而**SQLSetPos**會使用舊的資料列集大小。  
  
 資料列集中的第一個資料列是資料列號碼 1。 **SQLSetPos**中的*RowNumber*引數必須識別資料列集中的資料列;也就是說，其值必須介於1到最近提取的資料列數目（可能小於資料列集大小）之間。 如果*RowNumber*是0，則作業會套用至資料列集中的每個資料列。  
  
 由於大部分與關係資料庫的互動都是透過 SQL 來完成，因此不會廣泛支援**SQLSetPos** 。 不過，驅動程式可以藉由建立**UPDATE**或**DELETE**語句來輕鬆模擬它。  
  
 為了判斷**SQLSetPos**支援哪些作業，應用程式會使用 SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 資訊選項（視游標的類型而定）來呼叫**SQLGetInfo** 。  
  
 此章節包含下列主題。  
  
-   [使用 SQLSetPos 更新資料列集中的資料列](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)  
  
-   [使用 SQLSetPos 刪除資料列集中的資料列](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)
