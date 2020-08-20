---
description: 錯誤和批次
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
ms.openlocfilehash: 1e5cdf4d394ffa1c17173aedc4485b6979cf371e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461490"
---
# <a name="errors-and-batches"></a>錯誤和批次
當執行 SQL 語句批次發生錯誤時，可能會產生下列四種結果之一。  (每個可能的結果都是資料來源特有的結果，甚至可能取決於批次中包含的語句。 )   
  
-   未執行批次中的任何語句。  
  
-   不會執行批次中的語句，而且會回復交易。  
  
-   在執行 error 語句之前的所有語句。  
  
-   除了 error 語句以外的所有語句都會執行。  
  
 在前兩個案例中， **SQLExecute** 和 **SQLExecDirect** 會傳回 SQL_ERROR。 在後兩個案例中，它們可能會傳回 SQL_SUCCESS_WITH_INFO 或 SQL_SUCCESS，視執行而定。 在所有情況下，可以使用 **SQLGetDiagField**、 **SQLGetDiagRec**或 **SQLError**抓取進一步的錯誤資訊。 不過，這項資訊的本質和深度是資料來源特有的。 此外，這項資訊不太可能會完全找出錯誤的語句。
