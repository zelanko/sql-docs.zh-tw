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
ms.openlocfilehash: 7e709c74062e31483b042c3930572fb63ca8c786
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67996210"
---
# <a name="appendix-d-data-types"></a>附錄 D：資料類型
ODBC 會定義兩組資料類型： SQL 資料類型和 C 資料類型。 SQL 資料類型表示儲存在資料來源之資料的資料類型。 C 資料類型表示儲存在應用程式緩衝區中之資料的資料類型。  
  
 SQL 資料類型是根據 SQL-92 標準定義的每個 DBMS。 針對 SQL-92 標準中所指定的每個 SQL 資料類型，ODBC 會定義類型識別碼，這是在 ODBC 函式中當做引數傳遞，或在結果集的中繼資料中傳回的 **#define**值。 ODBC 不支援的唯一 SQL-92 資料類型為 BIT （ODBC SQL_BIT 類型具有不同的特性）、BIT_VARYING、TIME_WITH_TIMEZONE、TIMESTAMP_WITH_TIMEZONE 和 NATIONAL_CHARACTER。 驅動程式會負責將資料來源特定的 SQL 資料類型對應至 ODBC SQL 資料類型識別碼和驅動程式特定的 SQL 資料類型識別碼。 SQL 資料類型是在執行描述項的 [SQL_DESC_CONCISE_TYPE] 欄位中指定。  
  
 ODBC 會定義 C 資料類型及其對應的 ODBC 類型識別碼。 應用程式會在呼叫**SQLBindCol**或**SQLGetData**時，藉由在*TargetType*引數中傳遞適當的 c 類型識別碼，來指定將接收結果集資料之緩衝區的 c 資料類型。 它會在呼叫**SQLBindParameter**的*ValueType*引數中傳遞適當的 c 類型識別碼，藉以指定包含語句參數之緩衝區的 c 類型。 C 資料類型是在應用程式描述項的 [SQL_DESC_CONCISE_TYPE] 欄位中指定。  
  
> [!NOTE]  
>  沒有驅動程式特定的 C 資料類型。  
  
 每個 SQL 資料類型都會對應至 ODBC C 資料類型。 從資料來源傳回資料之前，驅動程式會將它轉換成指定的 C 資料類型。 將資料傳送至資料來源之前，驅動程式會將它轉換成指定的 C 資料類型。  
  
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
  
 如需 ODBC 資料類型的說明，請參閱[odbc 中的資料類型](../../../odbc/reference/develop-app/data-types-in-odbc.md)。 如需有關驅動程式特定 SQL 資料類型的詳細資訊，請參閱驅動程式的檔。
