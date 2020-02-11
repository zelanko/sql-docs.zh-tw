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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6902b82c74e953d6009d7e5352608477d92122d6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68051127"
---
# <a name="errors-and-batches"></a>錯誤和批次
執行 SQL 語句批次時發生錯誤時，可能會發生下列四種結果的其中一種。 （每個可能的結果都是資料來源特有，甚至可能會取決於批次中所包含的語句）。  
  
-   不會執行批次中的任何語句。  
  
-   不會執行批次中的任何語句，而且會回復交易。  
  
-   在執行 error 語句之前的所有語句。  
  
-   除了 error 語句之外，所有的語句都會執行。  
  
 在前兩個案例中， **SQLExecute**和**SQLExecDirect**會傳回 SQL_ERROR。 在後面兩個案例中，它們可能會傳回 SQL_SUCCESS_WITH_INFO 或 SQL_SUCCESS，視執行而定。 在所有情況下，可以使用**SQLGetDiagField**、 **SQLGetDiagRec**或**SQLError**來抓取進一步的錯誤資訊。 不過，這項資訊的本質和深度是資料來源特有的。 此外，這項資訊不太可能會確切地識別錯誤中的語句。
