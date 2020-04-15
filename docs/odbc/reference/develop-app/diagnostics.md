---
title: 診斷 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC]
- functions [ODBC], diagnostic information
- diagnostic information [ODBC], about diagnostic information
ms.assetid: 450abd88-90a1-4fbc-b417-8efbdd8e1dea
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a09f46d3fd6aa2f9b9c7310af6d3ddc90f78389f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305149"
---
# <a name="diagnostics"></a>診斷
ODBC 中的函數以兩種方式返回診斷資訊。 返回代碼指示函數的總體成功或失敗,而診斷記錄提供有關該函數的詳細資訊。 即使函數成功,也至少返回一個診斷記錄 - 標頭記錄。  
  
 診斷資訊在開發時用於捕獲程式設計錯誤,如硬編碼 SQL 語句中的無效句柄和語法錯誤。 它在運行時用於捕獲運行時錯誤和警告,如使用者輸入的 SQL 語句中的數據截斷、訪問衝突以及語法錯誤。  
  
 此章節包含下列主題。  
  
-   [傳回碼](../../../odbc/reference/develop-app/return-codes-odbc.md)  
  
-   [診斷記錄](../../../odbc/reference/develop-app/diagnostic-records.md)  
  
-   [使用 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [實作 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [診斷處理範例](../../../odbc/reference/develop-app/diagnostic-handling-examples.md)
