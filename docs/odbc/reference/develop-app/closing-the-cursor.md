---
description: 關閉資料指標
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cd9465f0fc076a4f41dd8bf4cb3463ce5a47de84
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461569"
---
# <a name="closing-the-cursor"></a>關閉資料指標
當應用程式完成使用資料指標時，它會呼叫 **SQLCloseCursor** 來關閉資料指標。 例如：  
  
```  
SQLCloseCursor(hstmt);  
```  
  
 在應用程式關閉資料指標之前，開啟資料指標的語句無法用於大部分的其他作業，例如執行另一個 SQL 語句。 如需可在資料指標開啟時呼叫之函式的完整清單，請參閱 [附錄 B： ODBC 狀態轉換資料表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
> [!NOTE]  
>  若要關閉資料指標，應用程式應該呼叫 **SQLCloseCursor**，而不是 **SQLCancel**。  
  
 資料指標會一直保持開啟，直到明確關閉為止，但交易認可或回復時除外，在此情況下，某些資料來源會關閉資料指標。 尤其是，當 **SQLFetch** 傳回 SQL_NO_DATA 時，若到達結果集的結尾，則不會關閉資料指標。 即使是空結果集上的資料指標， (當語句順利執行但未傳回任何資料列時，所建立的結果集會) 必須明確地關閉。
