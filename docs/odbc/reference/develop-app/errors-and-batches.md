---
title: 錯誤和批次 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300428"
---
# <a name="errors-and-batches"></a>錯誤和批次
當執行一批 SQL 語句時發生錯誤時,可能會出現以下四個結果之一。 (每個可能的結果都是特定於數據源的,甚至可能取決於批處理中包含的語句。  
  
-   未執行批處理中的語句。  
  
-   未執行批處理中的語句,並且事務將回滾。  
  
-   執行錯誤語句之前的所有語句。  
  
-   除錯誤語句之外的所有語句都執行。  
  
 在前兩種情況下 **,SQLExecute**和**SQLExecDirect**返回SQL_ERROR。 在後兩種情況下,它們可能返回SQL_SUCCESS_WITH_INFO或SQL_SUCCESS,具體取決於實現。 在所有情況下,可以使用**SQLGetDiagField、SQLGetDiagRec**或**SQLGetDiagRec** **SQLError**檢索進一步的錯誤資訊。 但是,此資訊的性質和深度是特定於數據源的。 此外,此資訊不可能準確識別錯誤語句。
