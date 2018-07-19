---
title: 關閉資料指標 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], closing
- closing cursors [ODBC]
ms.assetid: 4f19bf5e-6d8c-40ae-a975-cfd62a0790ec
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 794180396f9b233d32283f46264a696c80559d21
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32907713"
---
# <a name="closing-the-cursor"></a>關閉資料指標
當使用資料指標完成應用程式時，它會呼叫**SQLCloseCursor**來關閉資料指標。 例如：  
  
```  
SQLCloseCursor(hstmt);  
```  
  
 應用程式會關閉資料指標，直到開啟資料指標的陳述式無法用於大部分其他作業，例如執行另一個 SQL 陳述式。 如需可以在資料指標開啟時呼叫的函式的完整清單，請參閱[附錄 b: ODBC 狀態轉換表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
> [!NOTE]  
>  若要關閉資料指標，應用程式應該呼叫**SQLCloseCursor**，而非**SQLCancel**。  
  
 資料指標維持開啟直到明確關閉它們，除了時認可或回復交易，在此情況下某些資料來源關閉資料指標。 特別是，達到結果結束設定，當**SQLFetch**傳回 sql_no_data 之後，不會關閉資料指標。 甚至是空的結果集 （陳述式執行成功，但是會不傳回任何資料列時，建立結果集） 資料指標必須明確地關閉。
