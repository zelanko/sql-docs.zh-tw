---
title: "診斷 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC]
- functions [ODBC], diagnostic information
- diagnostic information [ODBC], about diagnostic information
ms.assetid: 450abd88-90a1-4fbc-b417-8efbdd8e1dea
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: adb6f66ecfbff558fd163437a56453efb4265185
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="diagnostics"></a>診斷
在 ODBC 中的函式會傳回兩種方式的診斷資訊。 傳回碼指出整體成功或失敗的函式，而診斷記錄會提供有關函數的詳細的資訊。 至少一個診斷記錄： 標頭記錄 — 即使函式成功時傳回。  
  
 診斷資訊在開發時間用於捕捉程式設計錯誤，例如無效的控制代碼和語法錯誤硬式編碼的 SQL 陳述式中。 它是在執行階段用來攔截執行階段錯誤和警告，例如資料截斷、 存取違規和語法錯誤，使用者所輸入的 SQL 陳述式中。  
  
 此章節包含下列主題。  
  
-   [傳回碼](../../../odbc/reference/develop-app/return-codes-odbc.md)  
  
-   [診斷記錄](../../../odbc/reference/develop-app/diagnostic-records.md)  
  
-   [使用 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [實作 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [診斷的處理範例](../../../odbc/reference/develop-app/diagnostic-handling-examples.md)

