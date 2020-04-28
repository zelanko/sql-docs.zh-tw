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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a09f46d3fd6aa2f9b9c7310af6d3ddc90f78389f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305149"
---
# <a name="diagnostics"></a>診斷
ODBC 中的函數會以兩種方式傳回診斷資訊。 傳回碼表示函式的整體成功或失敗，而診斷記錄則提供有關函數的詳細資訊。 至少一個診斷記錄-即使函式成功，也會傳回標頭記錄。  
  
 診斷資訊會在開發期間用來攔截程式設計錯誤，例如硬式編碼 SQL 語句中的無效控制碼和語法錯誤。 它會在執行時間用來攔截執行時間錯誤和警告，例如使用者所輸入的 SQL 語句中的資料截斷、存取違規和語法錯誤。  
  
 此章節包含下列主題。  
  
-   [傳回碼](../../../odbc/reference/develop-app/return-codes-odbc.md)  
  
-   [診斷記錄](../../../odbc/reference/develop-app/diagnostic-records.md)  
  
-   [使用 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [實作 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [診斷處理範例](../../../odbc/reference/develop-app/diagnostic-handling-examples.md)
