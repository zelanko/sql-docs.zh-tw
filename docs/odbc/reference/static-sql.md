---
title: 靜態 SQL |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- static SQL [ODBC]
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- SQL statements [ODBC], static SQL
- embedded SQL [ODBC]
- SQL [ODBC], static SQL
ms.assetid: 667d92ec-fed9-4028-81d4-bb9ba867356a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2e6d053e4d2a5520432c4c1debbafb35fdb17bc4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016746"
---
# <a name="static-sql"></a>靜態 SQL
內嵌的 SQL 中所示[內嵌 SQL 範例](../../odbc/reference/embedded-sql-example.md)稱為靜態 SQL。 因為在程式中的 SQL 陳述式都是靜態的所以稱為靜態 SQL也就是說，不會變更每個執行程式的時間。 上一節所述，編譯程式的其餘部分時，會編譯這些陳述式。  
  
 靜態 SQL 也適用於多種情況，而且可用在任何可以在程式的設計階段決定的資料存取的應用程式。 例如，訂單項目計劃一律使用相同的陳述式來插入新的順序，和航班訂位系統一律使用相同的陳述式來變更可保留座位的狀態。 每個陳述式會透過主應用程式變數中; 使用一般化不同的值，請插入銷售訂單，並可保留不同的基座。 由於這類陳述式可以是硬式編碼在程式中，這類程式會有陳述式需要進行剖析、 驗證和最佳化一次，在編譯時期的優點。 這會導致相當快速的程式碼。
