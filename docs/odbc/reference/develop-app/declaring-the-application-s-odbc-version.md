---
title: "宣告的應用程式 &#39; s 的 ODBC 版本 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- declaring ODBC version [ODBC]
- data sources [ODBC], declaring ODBC version
- ODBC drivers [ODBC], declaring ODBC version
- connecting to driver [ODBC], declaring ODBC version
- connecting to data source [ODBC], declaring ODBC version
- version declaration [ODBC]
ms.assetid: 083a1ef5-580a-4979-9cf3-50f4549a080a
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2c021fb123e0a8cf861fa91fe78d3882ba16111e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="declaring-the-application39s-odbc-version"></a>宣告的應用程式 &#39; s 的 ODBC 版本
應用程式配置連接之前，它必須設定 SQL_ATTR_ODBC_VERSION 環境屬性。 這個屬性會指出應用程式遵循 ODBC 2。*x*或 ODBC 3。*x*規格，使用下列項目：  
  
-   **Sqlstate**。 SQLSTATE 值的 ODBC 2 不同。*x*和 ODBC 3。*x*。  
  
-   **日期、 時間和時間戳記類型識別項**。 下表顯示日期、 時間和 ODBC 2 中的時間戳記資料類型識別項。*x*和 ODBC 3。*x*。  
  
    |ODBC 2。*x*|ODBC 3。*x*|  
    |----------------|----------------|  
    |**SQL 類型識別碼**||  
    |SQL_DATE|SQL_TYPE_DATE|  
    |SQL_TIME|SQL_TYPE_TIME|  
    |SQL_TIMESTAMP|SQL_TYPE_TIMESTAMP|  
    |**C 類型識別項**||  
    |SQL_C_DATE|SQL_C_TYPE_DATE|  
    |SQL_C_TIME|SQL_C_TYPE_TIME|  
    |SQL_C_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|  
  
-   *CatalogName***引數中 SQLTables**。 在 ODBC 2。*x*中的萬用字元 （"%"和"_"） *CatalogName*引數會被視為常值。 在 ODBC 3。*x*，它們會被視為萬用字元。 因此，應用程式的 ODBC 2。*x*規格不能做為這些萬用字元的字元，並不會不會逸出，做為常值中使用它們時。 依照 ODBC 3 應用程式。*x*規格可以使用這些萬用字元的字元或逸出，並將其當做常值。 如需詳細資訊，請參閱[目錄函數中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 ODBC 3*.x*驅動程式管理員和 ODBC 3*.x*驅動程式會檢查應用程式寫入 ODBC 規格的版本，並據以回應。 例如，如果應用程式遵循 ODBC 2。*x*規格和呼叫**SQLExecute**之前先呼叫**SQLPrepare**，ODBC 3*.x*驅動程式管理員會傳回 SQLSTATE S1010 （函數順序錯誤）。 如果應用程式遵循 ODBC 3*.x*規格，驅動程式管理員會傳回 SQLSTATE HY010 （函數順序錯誤）。 如需詳細資訊，請參閱[回溯相容性和標準相容性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。  
  
> [!IMPORTANT]  
>  依照 ODBC 3 的應用程式。*x*規格必須使用條件式程式碼來避免使用 ODBC 3 的新功能。*x*時使用的 ODBC 2。*x*驅動程式。 ODBC 2。*x*驅動程式不支援 ODBC 3 的新功能。*x*只是因為應用程式宣告，它會遵循 ODBC 3。*x*規格。 此外，ODBC 3。*x*驅動程式支援 ODBC 3 的新功能不能停止。*x*只是因為應用程式宣告，它會遵循 ODBC 2。*x*規格。
