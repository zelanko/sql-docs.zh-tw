---
title: ODBC 解決方案 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], using ODBC
ms.assetid: 34b80790-e010-4b90-8eaa-03189f5d8986
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2b35883ff4d621f0ecc092020ad744455281dd63
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286751"
---
# <a name="the-odbc-solution"></a>ODBC 解決方案
那麼,問題是ODBC如何標準化資料庫訪問? 有兩個體系結構要求:  
  
-   應用程式必須能夠使用相同的原始程式碼存取多個 DBMS,而無需重新編譯或重新連結。  
  
-   應用程式必須能夠同時訪問多個 DBMS。  
  
 由於市場現實,還有一個問題:  
  
-   應公開哪些 DBMS 功能? 只有所有 DBMS 共有的功能或任何 DBMS 中可用的功能?  
  
 ODBC 以以下方式解決了這些問題:  
  
-   **ODBC 是一個呼叫級介面。** 為了解決應用程式如何使用同一原始程式碼存取多個 DBM 的問題,ODBC 定義了標準 CLI。 它包含開放組和 ISO/IEC CLI 規範中的所有功能,並提供應用程式通常要求的其他功能。  
  
     支援 ODBC 的每個 DBMS 都需要不同的庫或驅動程式。 驅動程式在 ODBC API 中實現函數。 要使用其他驅動程式,不需要重新編譯或重新連結應用程式。 相反,應用程式只需載入新驅動程式並調用其中的函數。 要同時訪問多個 DBMS,應用程式將載入多個驅動程式。 支援驅動程式的方式特定於作業系統。 例如,在 Microsoft® Windows ®作業系統上,驅動程式是動態連結庫 (DLL)。  
  
-   **ODBC 定義了標準的 SQL 語法。** 除了標準調用級介面外,ODBC 還定義了標準的 SQL 語法。 此語法基於開放組 SQL CAE 規範。 這兩種語法之間的差異很小,這主要是因為嵌入式 SQL(開放組)和 CLI (ODBC) 所需的 SQL 語法之間的差異。 還有一些語法擴展,以公開開放組語法未涵蓋的常用語言功能。  
  
     應用程式可以使用 ODBC 或 DBMS 特定的語法提交語句。 如果語句使用的 ODBC 語法不同於特定於 DBMS 的語法,則驅動程式在將其發送到數據來源之前將其轉換。 但是,此類轉換很少見,因為大多數 DBMS 已經使用標準 SQL 語法。  
  
-   **ODBC 提供了一個驅動程式管理員來管理對多個 DBMS 的同步訪問。** 儘管驅動程式的使用解決了同時訪問多個 DBMS 的問題,但這樣做的程式碼可能很複雜。 設計用於所有驅動程式的應用程式不能以靜態方式連結到任何驅動程式。 相反,它們必須在運行時載入驅動程式,並透過函數指標表調用其中的函數。 如果應用程式同時使用多個驅動程序,情況將變得更加複雜。  
  
     ODBC 不是強制每個應用程式執行此操作,而是提供了一個驅動程式管理器。 驅動程式管理員實現所有 ODBC 函數(主要是在驅動程式中作為對 ODBC 函數的傳遞呼叫),並靜態連結到應用程式或在運行時由應用程式載入。 因此,應用程式在驅動程式管理器中按名稱調用 ODBC 函數,而不是按每個驅動程式中的指標調用。  
  
     當應用程式需要特定驅動程式時,它首先請求一個連接句柄來標識驅動程式,然後請求驅動程式管理器載入驅動程式。 驅動程式管理員載入驅動程式並將每個函數的位址存儲在驅動程式中。 要在驅動程式中調用 ODBC 函數,應用程式將呼叫驅動程式管理器中的該函數並傳遞驅動程式的連接句柄。 然後,驅動程式管理器使用它之前存儲的位址調用函數。  
  
-   **ODBC 公開了大量的 DBMS 功能,但不需要驅動程式來支援所有這些功能。** 如果 ODBC 只公開所有 DBMS 共有的功能,則使用很少;畢竟,今天存在這麼多不同的DBMS的原因是它們有不同的功能。 如果 ODBC 公開了任何 DBMS 中可用的所有功能,則驅動程式將無法實現。  
  
     相反,ODBC 公開了大量的功能(比大多數 DBMS 支援的功能更多),但要求驅動程式僅實現這些功能的子集。 僅當基礎 DBMS 支援這些功能或選擇類比這些功能時,驅動程式才實現這些功能。 因此,可以編寫應用程式來利用該 DBMS 的驅動程式公開的單個 DBMS 的功能,僅使用所有 DBBMS 使用的功能,或者檢查對特定功能的支援並做出相應反應。  
  
     以便應用程式可以確定驅動程式和 DBMS 支援的功能,ODBC 提供了兩個函數 **(SQLGetInfo**和**SQLGet 功能**),傳回有關驅動程式和 DBMS 功能的一般資訊以及驅動程式支援的函數清單。 ODBC 還定義了 API 和 SQL 語法一致性級別,這些級別指定驅動程式支援的廣泛功能範圍。 有關詳細資訊,請參閱[一致性級別](../../odbc/reference/develop-app/conformance-levels.md)。  
  
     請務必記住,ODBC 為其公開的所有功能定義了通用介面。 因此,應用程式包含特定於功能的代碼,而不是特定於 DBMS 的代碼,並且可以使用公開這些功能的任何驅動程式。 這樣做的一個優點是,當 DBMS 支援的功能得到增強時,不需要更新應用程式;相反,在安裝更新的驅動程式時,應用程式會自動使用這些功能,因為它的代碼特定於功能,而不是特定於驅動程式或特定於 DBMS。
