---
title: "使用資料類型識別項 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], identifiers
- identifiers [ODBC], data types
ms.assetid: 467e0c0c-a818-4737-8a24-3d8e15c7e162
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7dbffa887dbe29c6bf1cd686537ebd6dbe6981fa
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="using-data-type-identifiers"></a>使用資料類型識別碼
應用程式使用資料類型識別碼有兩種： 描述其緩衝區，以驅動程式，以及擷取的結果集從驅動程式，以便決定要用來儲存資料緩衝處理的 C 類型相關的中繼資料。 應用程式呼叫下列函數來執行這些工作：  
  
-   **SQLBindParameter**， **SQLBindCol**，和**SQLGetData** — 來描述應用程式緩衝區的 C 資料類型。  
  
-   **SQLBindParameter** — 來描述 SQL 資料類型的動態參數。  
  
-   **SQLColAttribute**和**SQLDescribeCol** -擷取 SQL 資料類型的結果集資料行。  
  
-   **SQLDescribeParameter** -擷取 SQL 資料類型的參數。  
  
-   **SQLColumns**， **SQLProcedureColumns**，和**SQLSpecialColumns** -擷取 SQL 資料類型的各種不同的結構描述資訊  
  
-   **SQLGetTypeInfo** — 若要擷取的清單支援的資料類型  
  
 資料類型識別碼會儲存在 SQL_DESC_CONCISE_TYPE 欄位描述元。 描述元函式**SQLSetDescField**和**SQLSetDescRec**可以適當的型別與用來執行上述清單中所列的工作。 如需詳細資訊，請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。
