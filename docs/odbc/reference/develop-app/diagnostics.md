---
title: 診斷 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 72e79d377371277720e2fcc15a31ce715693d832
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52512093"
---
# <a name="diagnostics"></a>診斷
ODBC 中的函式會傳回兩種方式的診斷資訊。 傳回碼指出整體成功或失敗的函式，而診斷記錄會提供有關函數的詳細的資訊。 即使函式成功，則會傳回至少一個診斷記錄-標頭記錄集。  
  
 診斷資訊在開發階段用於捕捉程式設計錯誤，例如無效的控制代碼和語法錯誤硬式編碼的 SQL 陳述式中。 它是在執行階段用來在使用者輸入的 SQL 陳述式中攔截執行階段錯誤和警告，例如資料截斷、 存取違規和語法錯誤。  
  
 此章節包含下列主題。  
  
-   [傳回碼](../../../odbc/reference/develop-app/return-codes-odbc.md)  
  
-   [診斷記錄](../../../odbc/reference/develop-app/diagnostic-records.md)  
  
-   [使用 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [實作 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [診斷處理範例](../../../odbc/reference/develop-app/diagnostic-handling-examples.md)
