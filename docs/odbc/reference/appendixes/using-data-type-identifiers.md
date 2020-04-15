---
title: 使用資料類型識別碼 ( A)微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- identifiers [ODBC], data types
ms.assetid: 467e0c0c-a818-4737-8a24-3d8e15c7e162
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8be8eef0441d48ed03ea6ccf8f656627c1dd9b63
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301419"
---
# <a name="using-data-type-identifiers"></a>使用資料類型識別碼
應用程式使用數據類型識別碼的方式有兩種:向驅動程式描述其緩衝區,以及從驅動程式檢索有關結果集的元數據,以便確定用於儲存資料的 C 緩衝區類型。 應用程式呼叫以下函數執行這些工作:  
  
-   **SQLBind參數****、SQLBindCol**和**SQLGetData** - 描述應用程式緩衝區的 C 資料類型。  
  
-   **SQLBind參數**- 描述動態參數的 SQL 資料類型。  
  
-   **SQLColAttribute**和**SQLDescribeCol** - 檢索結果集列的 SQL 資料類型。  
  
-   **SQL描述參數**- 檢索參數的 SQL 資料類型。  
  
-   **SQL 欄****、SQL 程式列**與**SQL 特殊欄**- 檢索各種架構資訊的 SQL 資料類型  
  
-   **SQLGetTypeInfo** - 檢索受支援的資料類型清單  
  
 資料類型識別碼儲存在描述符的SQL_DESC_CONCISE_TYPE欄位中。 描述符功能**SQLSetDescField**和**SQLSetDescCRec**可與適當的類型一起使用,以執行上一列表中列出的任務。 有關詳細資訊,請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。
