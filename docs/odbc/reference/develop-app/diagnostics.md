---
description: 診斷
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
ms.openlocfilehash: 918dce41ca1c7e7b43c1a6d25de2c75a83312715
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476710"
---
# <a name="diagnostics"></a>診斷
ODBC 中的函數會以兩種方式傳回診斷資訊。 傳回碼表示函式的整體成功或失敗，而診斷記錄會提供函數的詳細資訊。 至少要有一個診斷記錄（標頭記錄）會傳回，即使函式成功也一樣。  
  
 診斷資訊會在開發階段用來捕捉程式設計錯誤，例如硬式編碼的 SQL 語句中的無效控制碼和語法錯誤。 它是在執行時間用來攔截執行時間錯誤和警告，例如資料截斷、存取違規，以及使用者輸入的 SQL 語句中的語法錯誤。  
  
 此章節包含下列主題。  
  
-   [傳回碼](../../../odbc/reference/develop-app/return-codes-odbc.md)  
  
-   [診斷記錄](../../../odbc/reference/develop-app/diagnostic-records.md)  
  
-   [使用 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [實作 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [診斷處理範例](../../../odbc/reference/develop-app/diagnostic-handling-examples.md)
