---
title: 驅動程式任務 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC], tasks
ms.assetid: 184c795a-c2e8-4d20-9902-12e60b2f0e45
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1b30df63a3c955d2ed074ab13649ea55c21a6da7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294198"
---
# <a name="driver-tasks"></a>驅動程式工作
驅動程式執行的特定工作包括:  
  
-   連接到數據源並從斷開。  
  
-   檢查驅動程式管理員未檢查的函數錯誤。  
  
-   啟動交易;這對應用程式是透明的。  
  
-   將 SQL 語句提交到數據源以進行執行。 驅動程式必須將 ODBC SQL 修改為特定於 DBMS 的 SQL;這通常僅限於將 ODBC 定義的轉義子句替換為特定於 DBMS 的 SQL。  
  
-   將資料發送到數據源並從資料源檢索數據,包括轉換應用程式指定的數據類型。  
  
-   將特定於 DBMS 的錯誤映射到 ODBC SQLSTAT。
