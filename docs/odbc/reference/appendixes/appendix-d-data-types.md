---
description: 附錄 D：資料類型
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 77ca1ac4b4628880e6f0a87237b347aadb66584d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411484"
---
# <a name="appendix-d-data-types"></a>附錄 D：資料類型
ODBC 會定義兩組資料類型： SQL 資料類型和 C 資料類型。 SQL 資料類型指出儲存在資料來源之資料的資料類型。 C 資料類型指出儲存在應用程式緩衝區中資料的資料類型。  
  
 SQL 資料類型是根據 SQL-92 標準來定義每個 DBMS。 針對 SQL-92 標準中所指定的每個 SQL 資料類型，ODBC 會定義類型識別碼，這是一個 **#define** 值，這個值會以 ODBC 函數中的引數形式傳遞，或在結果集的中繼資料中傳回。 ODBC 所不支援的 SQL-92 資料類型是 BIT (ODBC SQL_BIT 類型有不同的特性) 、BIT_VARYING、TIME_WITH_TIMEZONE、TIMESTAMP_WITH_TIMEZONE 和 NATIONAL_CHARACTER。 驅動程式負責將資料來源特定的 SQL 資料類型對應至 ODBC SQL 資料類型識別碼和驅動程式特定的 SQL 資料類型識別碼。 SQL 資料類型是在執行描述項的 [SQL_DESC_CONCISE_TYPE] 欄位中指定。  
  
 ODBC 會定義 C 資料類型及其對應的 ODBC 類型識別碼。 應用程式會在呼叫**SQLBindCol**或**SQLGetData**時，藉由在*TargetType*引數中傳遞適當的 C 類型識別碼，以指定接收結果集資料之緩衝區的 c 資料類型。 它會指定包含語句參數之緩衝區的 C 類型，方法是在**SQLBindParameter**呼叫中的*ValueType*引數中傳遞適當的 C 類型識別碼。 C 資料類型是在應用程式描述項的 [SQL_DESC_CONCISE_TYPE] 欄位中指定。  
  
> [!NOTE]  
>  沒有任何驅動程式特定的 C 資料類型。  
  
 每個 SQL 資料類型都會對應至 ODBC C 資料類型。 從資料來源傳回資料之前，驅動程式會將它轉換成指定的 C 資料類型。 將資料傳送到資料來源之前，驅動程式會從指定的 C 資料類型進行轉換。  
  
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
  
 如需 ODBC 資料類型的說明，請參閱 [odbc 中的資料類型](../../../odbc/reference/develop-app/data-types-in-odbc.md)。 如需有關驅動程式特定的 SQL 資料類型的詳細資訊，請參閱驅動程式的檔。
