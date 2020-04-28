---
title: 錯誤和批次 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- batches [ODBC], errors
- sql_success_with_info [ODBC]
- sql_success [ODBC]
- SQL statements [ODBC], batches
- sql_error [ODBC]
ms.assetid: 6debd41d-9f4c-4f4c-a44b-2993da5306f0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 36a402686a695a08748df24a7b40a228d7a2ca7f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300428"
---
# <a name="errors-and-batches"></a>錯誤和批次
執行 SQL 語句批次時發生錯誤時，可能會發生下列四種結果的其中一種。 （每個可能的結果都是資料來源特有，甚至可能會取決於批次中所包含的語句）。  
  
-   不會執行批次中的任何語句。  
  
-   不會執行批次中的任何語句，而且會回復交易。  
  
-   在執行 error 語句之前的所有語句。  
  
-   除了 error 語句之外，所有的語句都會執行。  
  
 在前兩個案例中， **SQLExecute**和**SQLExecDirect**會傳回 SQL_ERROR。 在後面兩個案例中，它們可能會傳回 SQL_SUCCESS_WITH_INFO 或 SQL_SUCCESS，視執行而定。 在所有情況下，可以使用**SQLGetDiagField**、 **SQLGetDiagRec**或**SQLError**來抓取進一步的錯誤資訊。 不過，這項資訊的本質和深度是資料來源特有的。 此外，這項資訊不太可能會確切地識別錯誤中的語句。
