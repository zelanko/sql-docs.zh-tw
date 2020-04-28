---
title: 宣告應用程式&#39;s ODBC 版本 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ba346ed7f7a261446110c5513026d20a86fd3a19
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81285228"
---
# <a name="declaring-the-application39s-odbc-version"></a>宣告應用程式&#39;s ODBC 版本
在應用程式佈建連接之前，必須先設定 SQL_ATTR_ODBC_VERSION 環境屬性。 此屬性說明當使用下列專案時，應用程式會遵循 ODBC *2.x 或 odbc* *3.x 規格：*  
  
-   **SQLSTATEs**。 ODBC *2.x 和 odbc* 3.x 中的許多 SQLSTATE 值都不同 *。*  
  
-   **日期、時間和時間戳記類型識別碼**。 下表顯示 ODBC 2.x*和 odbc 3.x*中的日期、*時間和時間*戳資料的類型識別碼。  
  
    |ODBC *2.x*|ODBC *3.x*|  
    |----------------|----------------|  
    |**SQL 類型識別碼**||  
    |SQL_DATE|SQL_TYPE_DATE|  
    |SQL_TIME|SQL_TYPE_TIME|  
    |SQL_TIMESTAMP|SQL_TYPE_TIMESTAMP|  
    |**C 類型識別碼**||  
    |SQL_C_DATE|SQL_C_TYPE_DATE|  
    |SQL_C_TIME|SQL_C_TYPE_TIME|  
    |SQL_C_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|  
  
-   _ _ **SQLTables 中的 CatalogName 引數**。   在 ODBC *2.x 中，* *CatalogName*引數中的萬用字元（"%" 和 "_"）會以字面方式處理。 在 ODBC *3.x 中，* 它們會被視為萬用字元。 因此，*遵循 ODBC 2.x*規格的應用程式不能使用這些做為萬用字元，而且在使用它們做為常值時，不會將它們換用。 遵循*ODBC 3.x*規格的應用程式可以使用這些字元做為萬用字元，或將它們當做常值使用。 如需詳細資訊，請參閱[目錄函數中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 ODBC 3.x*驅動程式*管理員*和 odbc* 3.x 驅動程式會檢查應用程式所寫入的 ODBC 規格版本，並據以回應。 例如，如果應用程式*遵循 ODBC 2.x*規格，並在呼叫**SQLPrepare**之前呼叫**SQLExecute** ，*則 ODBC 3.X*驅動程式管理員會傳回 SQLSTATE S1010 （函數序列錯誤）。 如果應用程式*遵循 ODBC 3.x*規格，驅動程式管理員會傳回 SQLSTATE HY010 （函數序列錯誤）。 如需詳細資訊，請參閱回溯[相容性和標準合規性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。  
  
> [!IMPORTANT]  
>  遵循 ODBC 3.x 規格的應用程式必須使用條件*式程式碼*，以*避免在使用 odbc 2.x*驅動程式時*使用 odbc 3.x*的新功能。 ODBC *2.x 驅動程式不支援 odbc 3.x*的新功能，*只是*因為應用程式宣告它遵循 odbc *3.x 規格。* 此外，ODBC *3.x 驅動程式*不會停止支援 odbc 3.x 的新功能， *3.x*因為應用程式會宣告它遵循 odbc *2.x 規格。*
