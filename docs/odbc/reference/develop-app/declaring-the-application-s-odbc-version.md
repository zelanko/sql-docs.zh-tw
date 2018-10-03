---
title: 宣告應用程式&#39;的 ODBC 版本 s |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- declaring ODBC version [ODBC]
- data sources [ODBC], declaring ODBC version
- ODBC drivers [ODBC], declaring ODBC version
- connecting to driver [ODBC], declaring ODBC version
- connecting to data source [ODBC], declaring ODBC version
- version declaration [ODBC]
ms.assetid: 083a1ef5-580a-4979-9cf3-50f4549a080a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cd212f45e02ddce4c64a8b4a7d664ddaedf8090a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47666826"
---
# <a name="declaring-the-application39s-odbc-version"></a>宣告應用程式&#39;s 的 ODBC 版本
應用程式配置連接之前，它必須設定 SQL_ATTR_ODBC_VERSION 環境屬性。 這個屬性會指出應用程式遵循 ODBC 2。*x*或 ODBC 3。*x*規格，使用下列項目時：  
  
-   **Sqlstate**。 SQLSTATE 值的 ODBC 2 不同。*x*和 ODBC 3。*x*。  
  
-   **日期、 時間和時間戳記類型識別碼**。 下表顯示日期、 時間和 ODBC 2 中的時間戳記資料的型別識別項。*x*和 ODBC 3。*x*。  
  
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
  
-   *CatalogName***引數中 SQLTables**。   在 ODBC 2。*x*中的萬用字元 （"%"和"_"） *CatalogName*引數將依字面解譯。 在 ODBC 3。*x*，它們會被視為萬用字元。 因此，應用程式會遵循 ODBC 2。*x*規格不能使用這些因為萬用字元的字元，並不會逸出它們時使用它們做為常值。 依照 ODBC 3 應用程式。*x*規格可以使用這些動作當做萬用字元的字元或逸出它們，並將其當做常值。 如需詳細資訊，請參閱 <<c0> [ 目錄函式中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 ODBC 3 *.x*驅動程式管理員和 ODBC 3 *.x*驅動程式檢查應用程式會寫入至其中的 ODBC 規格的版本，並據以回應。 比方說，如果應用程式會遵循 ODBC 2。*x*規格並呼叫**SQLExecute**再呼叫**SQLPrepare**，ODBC 3 *.x*驅動程式管理員會傳回 SQLSTATE S1010 （函數順序錯誤）。 如果應用程式會遵循 ODBC 3 *.x*規格，驅動程式管理員會傳回 SQLSTATE HY010 （函數順序錯誤）。 如需詳細資訊，請參閱 <<c0> [ 回溯相容性與標準相容性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。  
  
> [!IMPORTANT]  
>  請依照下列 ODBC 3 的應用程式。*x*規格必須使用條件式的程式碼，以避免使用 ODBC 3 的新功能。*x*時使用的 ODBC 2。*x*驅動程式。 ODBC 2。*x*驅動程式不支援 ODBC 3 的新功能。*x*只是因為應用程式宣告，它會遵循 ODBC 3。*x*規格。 此外，ODBC 3。*x*驅動程式不會停止支援 ODBC 3 的新功能。*x*只是因為應用程式宣告，它會遵循 ODBC 2。*x*規格。
