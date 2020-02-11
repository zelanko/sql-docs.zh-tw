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
ms.openlocfilehash: de22797bdcf4ff526a8c17aee313567da3114b60
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036539"
---
# <a name="closing-the-cursor"></a>關閉資料指標
當應用程式完成使用資料指標時，它會呼叫**SQLCloseCursor**來關閉資料指標。 例如：  
  
```  
SQLCloseCursor(hstmt);  
```  
  
 在應用程式關閉資料指標之前，資料指標開啟所在的語句無法用於大部分的其他作業，例如執行另一個 SQL 語句。 如需可在資料指標開啟時呼叫之函式的完整清單，請參閱[附錄 B： ODBC 狀態轉換資料表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
> [!NOTE]  
>  若要關閉資料指標，應用程式應該呼叫**SQLCloseCursor**，而不是**SQLCancel**。  
  
 資料指標會保持開啟狀態，直到明確關閉為止，除非交易已認可或回復，在此情況下，某些資料來源會關閉資料指標。 特別是，到達結果集的結尾時，當**SQLFetch**傳回 SQL_NO_DATA 時，不會關閉資料指標。 即使是空的結果集的資料指標（當語句成功執行但未傳回任何資料列時所建立的結果集）都必須明確地關閉。
