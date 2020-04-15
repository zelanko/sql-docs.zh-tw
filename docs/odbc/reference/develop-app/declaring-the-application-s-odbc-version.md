---
title: 宣告應用程式&#39;其 ODBC 版本 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285228"
---
# <a name="declaring-the-application39s-odbc-version"></a>宣告應用程式&#39;其 ODBC 版本
在應用程式分配連接之前,它必須設置SQL_ATTR_ODBC_VERSION環境屬性。 此屬性指出,當使用以下項時,應用程式遵循 ODBC *2.x*或 ODBC *3.x*規範:  
  
-   **SQLSTATEs**. 許多 SQLSTATE 值在 ODBC *2.x*和 ODBC *3.x*中是不同的。  
  
-   **日期、時間與時間戳類型識別碼**。 下表顯示了 ODBC *2.x*和 ODBC *3.x*中日期、時間和時間戳數據的類型識別碼。  
  
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
  
-   _SQLTables 的目錄名稱_  **參數**。 在 ODBC *2.x*中,*目錄名稱*參數中的通配符 ("%" 和「+」)從字面上處理。 在 ODBC *3.x*中,它們被視為通配符。 因此,遵循 ODBC *2.x*規範的應用程式不能將這些字元用作通配符,並且在將它們用作文本時不會轉義它們。 遵循 ODBC *3.x*規範的應用程式可以將這些字元用作通配元或轉義它們,並將其用作文本。 有關詳細資訊,請參閱[目錄函數 中的參數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 ODBC *3.x*驅動程式管理員和 ODBC *3.x*驅動程式檢查編寫應用程式的 ODBC 規範的版本並做出相應回應。 例如,如果應用程式遵循 ODBC *2.x*規範,並在調用**SQLPrepare**之前呼叫**SQLExecute,** 則 ODBC *3.x*驅動程式管理器返回 SQLSTATE S1010(函數序列錯誤)。 如果應用程式遵循 ODBC *3.x*規範,驅動程式管理員將返回 SQLSTATE HY010(函數序列錯誤)。 有關詳細資訊,請參閱[向後相容性和標準合規性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。  
  
> [!IMPORTANT]  
>  遵循 ODBC *3.x*規範的應用程式必須使用條件代碼,以避免在使用 ODBC *2.x*驅動程式時使用 ODBC *3.x*新增功能。 ODBC *2.x*驅動程式不支援 ODBC *3.x*新增的功能,只是因為應用程式聲明它遵循 ODBC *3.x*規範。 此外,ODBC *3.x*驅動程式不會僅僅因為應用程式聲明遵循 ODBC *2.x*規範而停止支援 ODBC *3.x*新增功能。
