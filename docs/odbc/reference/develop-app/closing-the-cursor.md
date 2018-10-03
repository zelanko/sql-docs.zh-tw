---
title: 關閉資料指標 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], closing
- closing cursors [ODBC]
ms.assetid: 4f19bf5e-6d8c-40ae-a975-cfd62a0790ec
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 632a922abb544a379892dfa168f55efd605304c8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47792956"
---
# <a name="closing-the-cursor"></a>關閉資料指標
當應用程式完成使用資料指標時，它會呼叫**SQLCloseCursor**來關閉資料指標。 例如：  
  
```  
SQLCloseCursor(hstmt);  
```  
  
 應用程式會關閉資料指標，直到開啟資料指標的陳述式不能用於大部分其他作業，例如執行其他的 SQL 陳述式。 如需可以在資料指標開啟時呼叫的函式的完整清單，請參閱[附錄 b: ODBC 狀態轉換資料表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
> [!NOTE]  
>  若要關閉資料指標，應用程式應該呼叫**SQLCloseCursor**，而非**SQLCancel**。  
  
 資料指標維持開啟的直到明確關閉，但當認可或回復交易，在此情況下某些資料來源時關閉資料指標。 特別是，服役年限結果的設定，當**SQLFetch**傳回 sql_no_data 為止，不會關閉資料指標。 甚至是空的結果集 （一個陳述式執行成功，但這會不傳回任何資料列時所建立的結果集） 上的資料指標必須明確地關閉。
