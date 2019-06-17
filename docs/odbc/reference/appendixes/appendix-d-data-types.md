---
title: 附錄 D：資料類型 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 75ff7e83aa87bca9f33a3a8f44447af2eb60c581
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63026767"
---
# <a name="appendix-d-data-types"></a>附錄 D：資料型別
ODBC 定義資料類型的兩個的集合：SQL 資料類型和 C 資料類型。 SQL 資料類型表示的資料類型儲存在資料來源的資料。 C 資料類型表示資料儲存在應用程式緩衝區中的資料類型。  
  
 SQL 資料類型是由每個 DBMS 根據 SQL-92 標準定義。 SQL-92 標準中所指定每個 SQL 資料類型，如 ODBC 定義的型別識別項，也就是 **#define**為 ODBC 函數的引數傳遞或傳回結果集的中繼資料中的值。 唯一的 SQL-92 不支援 ODBC 資料類型為位元 （ODBC SQL_BIT 類型會有不同的特性）、 BIT_VARYING、 TIME_WITH_TIMEZONE、 TIMESTAMP_WITH_TIMEZONE 和 NATIONAL_CHARACTER。 驅動程式會負責將資料來源特有的 SQL 資料類型對應至 ODBC SQL 資料型別識別項和驅動程式專用的 SQL 資料型別識別項。 實作描述項的 SQL_DESC_CONCISE_TYPE 欄位中指定的 SQL 資料類型。  
  
 ODBC 定義的 C 資料類型和其對應的 ODBC 型別識別項。 應用程式指定的 C 資料類型將會收到傳遞適當的 C 類型識別項中的結果集資料的緩衝區*TargetType*呼叫中的引數**SQLBindCol**或**SQLGetData**。 它會指定藉由傳遞適當的 C 類型識別項中包含的陳述式的參數緩衝區的 C 類型*ValueType*呼叫中的引數**SQLBindParameter**。 應用程式描述項的 SQL_DESC_CONCISE_TYPE 欄位中指定的 C 資料類型。  
  
> [!NOTE]  
>  沒有任何驅動程式特有的 C 資料型別。  
  
 每個 SQL 資料類型對應到 ODBC C 資料類型。 在傳回之前的資料從資料來源，此驅動程式將它轉換成指定的 C 資料類型。 之前將資料傳送至資料來源，此驅動程式將它轉換從指定的 C 資料類型。  
  
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
  
 如需 ODBC 資料類型的說明，請參閱 < [ODBC 中的資料類型](../../../odbc/reference/develop-app/data-types-in-odbc.md)。 如需驅動程式專用的 SQL 資料類型資訊，請參閱驅動程式的文件。
