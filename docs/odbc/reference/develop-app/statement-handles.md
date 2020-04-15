---
title: 語句句柄 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 65d6d78b-a8c8-489a-9dad-f8d127a44882
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1be90fe10d10a0b087d1c9724fed249805eb4dba
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299674"
---
# <a name="statement-handles"></a>陳述式控制代碼
*語句*最容易被視為 SQL 語句,例如**從員工中選擇\***。 但是,語句不僅僅是一個 SQL 語句 - 它包含與該 SQL 語句關聯的所有資訊,例如由語句創建的任何結果集以及在執行語句中使用的參數。 語句甚至不需要具有應用程式定義的 SQL 語句。 例如,當在語句上執行目錄函數(如**SQLTables)** 時,它將執行預定義的 SQL 語句,該語句返回表名稱的清單。  
  
 每個語句都由語句句柄標識。 語句與單個連接相關聯,並且該連接上可以有多個語句。 某些驅動程式限制他們支持的活動語句數;**SQLGetInfo**中的SQL_MAX_CONCURRENT_ACTIVITIES選項指定驅動程式在單個連接上支援多少個活動語句。 如果語句的結果處於掛起狀態,則語句定義為*活動*,其中結果為結果集,或者受**INSERT、UPDATE**或**UPDATE****DELETE**語句 影響的行計數,或者通過多次調用**SQLPutData**發送數據。  
  
 在實現 ODBC(驅動程式管理員或驅動程式)的程式碼段中,語句句柄識別包含語句資訊的結構,例如:  
  
-   語句的狀態  
  
-   目前語句級診斷  
  
-   繫結到敘述的參數與結果集列的應用程式變數的位址  
  
-   每個文片屬性的目前設定  
  
 語句句柄用於大多數 ODBC 函數。 值得注意的是,它們用於綁定參數和結果集列 **(SQLBind 參數**和**SQLBindCol),** 準備和執行語句 **(SQLPrepare、SQLExecute**和**SQLExecDirect),** 檢索**SQLExecute**中繼資料 **(SQLCol 屬性**和**SQLDescribeCol),** 提取結果 **(SQLFetch),** 並檢索診斷 **(SQLGetDiagField**和**SQLGetDiagRec)。** 它們還用於目錄函數 **(SQLColumns、SQLTables**等)和許多其他函**SQLTables**數。  
  
 語句句柄使用**SQLAllocHandle**分配,並釋放**SQLFreeHandle**。
