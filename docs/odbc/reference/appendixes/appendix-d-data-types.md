---
title: 附錄 D:資料類型 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- C data types [ODBC], defined
- SQL data types [ODBC], defined
- data types [ODBC]
- data types [ODBC], about data types
ms.assetid: 981d49c3-3531-4543-aa75-5bd9e4f67000
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c1abadb962e3a1ee9327bbb8d84e52d180b4a7e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292458"
---
# <a name="appendix-d-data-types"></a>附錄 D：資料類型
ODBC 定義了兩組數據類型:SQL 數據類型和 C 數據類型。 SQL 資料類型指示存儲在數據源中的數據的數據類型。 C 數據類型指示存儲在應用程式緩衝區中的數據的數據類型。  
  
 SQL 資料類型由每個 DBMS 根據 SQL-92 標準定義。 對於 SQL-92 標準中指定的每個 SQL 資料類型,ODBC 定義類型識別碼,該識別子是**一個#define**值,在 ODBC 函數中作為參數傳遞或在結果集的中數據中傳回。 ODBC 不支援的唯一 SQL-92 資料類型是 BIT(ODBC SQL_BIT類型具有不同的特徵)、BIT_VARYING、TIME_WITH_TIMEZONE、TIMESTAMP_WITH_TIMEZONE和NATIONAL_CHARACTER。 驅動程式負責將特定於資料來源的 SQL 資料類型映射到 ODBC SQL 資料類型識別碼和特定於驅動程式的 SQL 資料類型識別碼。 SQL 資料類型在實現描述符SQL_DESC_CONCISE_TYPE欄位中指定。  
  
 ODBC 定義 C 資料類型及其相應的 ODBC 類型識別碼。 應用程式指定緩衝區的 C 數據類型,該類型將透過在呼叫**SQLBindCol**或**SQLGetData**中在*TargetType*參數中傳遞相應的 C 類型識別碼來接收結果集數據。 它通過在調用**SQLBind 參數**中的*ValueType*參數中傳遞相應的 C 類型識別符來指定包含語句參數的緩衝區的 C 類型。 C 資料類型在應用程式描述符號的SQL_DESC_CONCISE_TYPE欄位中指定。  
  
> [!NOTE]  
>  沒有特定於驅動程式的 C 資料類型。  
  
 每個 SQL 資料類型對應於 ODBC C 資料類型。 在從數據源返回數據之前,驅動程式會將其轉換為指定的C資料類型。 在將資料發送到數據來源之前,驅動程式會將其從指定的 C 資料類型轉換。  
  
 本附錄包含以下主題。  
  
-   [使用資料類型識別碼](../../../odbc/reference/appendixes/using-data-type-identifiers.md)  
  
-   [SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md)  
  
-   [C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)  
  
-   [資料類型識別碼和描述項](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)  
  
-   [虛擬類型識別碼](../../../odbc/reference/appendixes/pseudo-type-identifiers.md)  
  
-   [以二進位形式傳輸資料](../../../odbc/reference/appendixes/transferring-data-in-its-binary-form.md)  
  
-   [間隔和數值資料類型的方針](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md)  
  
-   [西曆條件約束](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)  
  
-   [資料行大小、小數位數、傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)  
  
-   [將資料從 SQL 轉換成 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)  
  
-   [將資料從 C 轉換成 SQL 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)  
  
 有關 ODBC 資料型態的說明,請參閱[ODBC 中的資料型態](../../../odbc/reference/develop-app/data-types-in-odbc.md)。 有關特定於驅動程式的 SQL 資料類型的資訊,請參閱驅動程式的文檔。
