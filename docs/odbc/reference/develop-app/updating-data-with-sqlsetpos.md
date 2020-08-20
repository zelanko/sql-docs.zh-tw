---
description: 使用 SQLSetPos 更新資料
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eccc08e7af81b2b2b13dd50b2cfb0f5701174e70
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476280"
---
# <a name="updating-data-with-sqlsetpos"></a>使用 SQLSetPos 更新資料
應用程式可以使用 **SQLSetPos**來更新或刪除資料列集中的任何資料列。 呼叫 **SQLSetPos** 是用來建立和執行 SQL 語句的方便替代方法。 它可讓 ODBC 驅動程式支援定點更新，即使資料來源不支援定位的 SQL 語句。 它是透過函式呼叫達成完整資料庫存取的典範的一部分。  
  
 **SQLSetPos** 會在目前的資料列集上運作，而且只能在呼叫 **SQLFetchScroll**之後使用。 應用程式會指定要更新、刪除或插入的資料列編號，驅動程式會從資料列集緩衝區抓取該資料列的新資料。 **SQLSetPos** 也可用來將指定的資料列指定為目前的資料列，或從資料來源重新整理資料列集中的特定資料列。  
  
 使用 SQL_ATTR_ROW_ARRAY_SIZE 的*屬性*引數呼叫**SQLSetStmtAttr**來設定資料列集大小。 不過， **SQLSetPos**只會在呼叫**SQLFetch**或**SQLFetchScroll**之後使用新的資料列集大小。 例如，如果資料列集大小有所變更，則會呼叫 **SQLSetPos** ，然後呼叫 **SQLFetch** 或 **SQLFetchScroll** ，而 **SQLSetPos** 的呼叫會使用舊的資料列集大小，而 **SQLFetch** 或 **SQLFetchScroll** 則使用新的資料列集大小。  
  
 資料列集中的第一個資料列是資料列號碼 1。 **SQLSetPos**中的*RowNumber*引數必須識別資料列集中的資料列;也就是說，其值必須介於1到最近提取的資料列數目之間， (可能小於資料列集大小) 。 如果 *RowNumber* 是0，則作業會套用至資料列集內的每個資料列。  
  
 由於大部分與關係資料庫的互動都是透過 SQL 來完成，因此不會廣泛支援 **SQLSetPos** 。 不過，驅動程式可以藉由建立及執行 **UPDATE** 或 **DELETE** 語句，輕鬆地模擬它。  
  
 為了判斷 **SQLSetPos** 支援哪些作業，應用程式會使用 SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 資訊選項來呼叫 **SQLGetInfo** ， (視資料指標) 的類型而定。  
  
 此章節包含下列主題。  
  
-   [使用 SQLSetPos 更新資料列集中的資料列](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)  
  
-   [使用 SQLSetPos 刪除資料列集中的資料列](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)
