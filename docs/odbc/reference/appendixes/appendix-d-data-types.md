---
title: "附錄 d： 資料類型 |Microsoft 文件"
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
- C data types [ODBC], defined
- SQL data types [ODBC], defined
- data types [ODBC]
- data types [ODBC], about data types
ms.assetid: 981d49c3-3531-4543-aa75-5bd9e4f67000
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fe3088b5a750bd47f4d9a2c8288a1cedbd87be4c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="appendix-d-data-types"></a>附錄 d： 資料類型
ODBC 定義兩組資料類型： SQL 資料類型和 C 資料類型。 SQL 資料類型表示資料儲存在資料來源的資料類型。 C 資料類型表示資料儲存在應用程式緩衝區中的資料類型。  
  
 SQL 資料類型是由每個 DBMS 符合 sql-92 標準中定義。 Sql-92 標準中所指定每個 SQL 資料類型，如 ODBC 定義的型別識別碼，也就是**#define**作為 ODBC 函數的引數傳遞或傳回結果集的中繼資料中的值。 唯一的 SQL 92 不支援 ODBC 資料類型為位元 （ODBC SQL_BIT 類型具有不同的特性）、 BIT_VARYING、 TIME_WITH_TIMEZONE、 TIMESTAMP_WITH_TIMEZONE 和 NATIONAL_CHARACTER。 驅動程式會負責將資料來源專用的 SQL 資料類型對應至 ODBC SQL 資料類型識別碼和驅動程式特有的 SQL 資料類型識別項。 SQL 資料型別是欄位中指定 SQL_DESC_CONCISE_TYPE 實作描述元。  
  
 ODBC 定義的 C 資料類型和其對應的 ODBC 類型識別項。 應用程式指定 C 資料類型，將會收到傳遞適當的 C 類型識別項中的結果集資料的緩衝區*TargetType*呼叫中的引數**SQLBindCol**或**SQLGetData**。 它會指定藉由傳遞適當的 C 類型識別項中包含的陳述式參數的緩衝區的 C 類型*ValueType*呼叫中的引數**SQLBindParameter**。 C 資料類型為欄位中指定 SQL_DESC_CONCISE_TYPE 應用程式描述元。  
  
> [!NOTE]  
>  沒有驅動程式特有的 C 資料型別。  
  
 每個 SQL 資料類型會對應到 ODBC C 資料類型。 從資料來源傳回資料之前，驅動程式將它轉換成指定的 C 資料類型。 然後再將資料傳送至資料來源，此驅動程式將它轉換從指定的 C 資料類型。  
  
 本附錄包含下列主題。  
  
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
  
 如需 ODBC 資料類型的說明，請參閱[ODBC 中的資料型別](../../../odbc/reference/develop-app/data-types-in-odbc.md)。 如需驅動程式特有的 SQL 資料類型資訊，請參閱驅動程式的文件。
