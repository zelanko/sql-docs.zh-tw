---
title: 使用資料類型識別碼 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301419"
---
# <a name="using-data-type-identifiers"></a>使用資料類型識別碼
應用程式會以兩種方式使用資料類型識別碼：將其緩衝區描述到驅動程式，並從驅動程式抓取結果集的相關中繼資料，讓它們能夠判斷要用來儲存資料的 C 緩衝區類型。 應用程式會呼叫下列函式來執行這些工作：  
  
-   **SQLBindParameter**、 **SQLBindCol**和**SQLGetData** -描述應用程式緩衝區的 C 資料類型。  
  
-   **SQLBindParameter** -描述動態參數的 SQL 資料類型。  
  
-   **SQLColAttribute**和**SQLDescribeCol** -取得結果集資料行的 SQL 資料類型。  
  
-   **SQLDescribeParameter** -取得參數的 SQL 資料類型。  
  
-   **SQLColumns**、 **SQLProcedureColumns**和**SQLSpecialColumns** -用來捕獲各種架構資訊的 SQL 資料類型  
  
-   **SQLGetTypeInfo** -取得支援的資料類型清單  
  
 資料類型識別碼會儲存在描述項的 SQL_DESC_CONCISE_TYPE 欄位中。 描述項函式**SQLSetDescField**和**SQLSetDescRec**可以與適當的類型搭配使用，以執行上述清單中所列的工作。 如需詳細資訊，請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。
