---
title: ODBC 解決方案 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e6992e084c210cea1b95157744addfd40180fccb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68039338"
---
# <a name="the-odbc-solution"></a>ODBC 解決方案
問題是，ODBC 如何標準化資料庫存取？ 有兩種架構需求：  
  
-   應用程式必須能夠使用相同的原始程式碼存取多個 Dbms，而不需要重新編譯或重新連結。  
  
-   應用程式必須能夠同時存取多個 Dbms。  
  
 另外還有一個問題，原因是 marketplace 現實：  
  
-   ODBC 會公開哪些 DBMS 功能？ 只有所有 dbms 或任何 DBMS 中可用之功能通用的功能？  
  
 ODBC 會以下列方式解決這些問題：  
  
-   **ODBC 是一個呼叫層級介面。** 為了解決應用程式使用相同原始程式碼存取多個 Dbms 的問題，ODBC 會定義標準 CLI。 這包含來自 Open Group 和 ISO/IEC 的 CLI 規格中的所有函式，並提供應用程式通常需要的其他功能。  
  
     每個支援 ODBC 的 DBMS 都需要不同的程式庫或驅動程式。 驅動程式會實作用於 ODBC API 中的函式。 若要使用不同的驅動程式，則不需要重新編譯或重新連結應用程式。 相反地，應用程式只會載入新的驅動程式，並呼叫其中的函式。 若要同時存取多個 Dbms，應用程式會載入多個驅動程式。 驅動程式的支援方式是作業系統特定的。 例如，在 Microsoft® Windows®作業系統上，驅動程式是動態連結程式庫（Dll）。  
  
-   **ODBC 會定義標準 SQL 文法。** 除了標準的呼叫層級介面，ODBC 也會定義標準的 SQL 文法。 此文法以 Open Group SQL CAE 規格為基礎。 這兩個文法之間的差異很小，主要是因為內嵌 SQL （開放式群組）和 CLI （ODBC）所需的 SQL 文法之間的差異。 此外，也有一些文法延伸模組可公開開放式群組文法未涵蓋的常用語言功能。  
  
     應用程式可以使用 ODBC 或 DBMS 特定的文法來提交語句。 如果語句使用與 DBMS 特定文法不同的 ODBC 文法，驅動程式會先轉換它，再將它傳送至資料來源。 不過，這類轉換很罕見，因為大部分的 Dbms 已經使用標準 SQL 文法。  
  
-   **ODBC 提供驅動程式管理員來管理多個 Dbms 的同時存取。** 雖然使用驅動程式可解決同時存取多個 Dbms 的問題，但執行此動作的程式碼可能很複雜。 設計用來與所有驅動程式搭配使用的應用程式，無法以靜態方式連結至任何驅動程式。 相反地，它們必須在執行時間載入驅動程式，並透過函式指標的資料表呼叫其中的函式。 如果應用程式同時使用多個驅動程式，情況就會變得更複雜。  
  
     ODBC 會提供驅動程式管理員，而不會強制每個應用程式執行這項操作。 驅動程式管理員會針對驅動程式中的 ODBC 函式，以靜態方式連結至應用程式，或由應用程式在執行時間載入，來執行所有的 ODBC 函式（大多是以傳遞呼叫形式）。 因此，應用程式會依名稱在驅動程式管理員中呼叫 ODBC 函式，而不是依每個驅動程式中的指標。  
  
     當應用程式需要特定的驅動程式時，它會先要求用來識別驅動程式的連接控制碼，然後要求驅動程式管理員載入驅動程式。 驅動程式管理員會載入驅動程式，並將每個函式的位址儲存在驅動程式中。 為了呼叫驅動程式中的 ODBC 函式，應用程式會在驅動程式管理員中呼叫該函數，並傳遞該驅動程式的連接控制碼。 然後，驅動程式管理員會使用稍早儲存的位址來呼叫函式。  
  
-   **ODBC 會公開大量 DBMS 功能，但不需要驅動程式來支援它們。** 如果 ODBC 只公開所有 Dbms 通用的功能，則使用起來很少;畢竟，現在有許多不同的 Dbms 存在，是因為它們有不同的功能。 如果 ODBC 公開任何 DBMS 中可用的每項功能，則驅動程式可能無法執行。  
  
     相反地，ODBC 會公開大量的功能，但大部分的 Dbms 都不支援，但需要驅動程式才能只執行這些功能的子集。 驅動程式只會在基礎 DBMS 支援其餘功能或選擇模擬它們時，才會執行它們。 因此，應用程式可以撰寫成利用該 DBMS 的驅動程式所公開的單一 DBMS 功能，只使用所有 Dbms 所使用的功能，或檢查特定功能的支援，並據以做出回應。  
  
     為了讓應用程式能夠判斷驅動程式和 DBMS 支援哪些功能，ODBC 提供兩個函式（**SQLGetInfo**和**SQLGetFunctions**），以傳回有關驅動程式和 dbms 功能的一般資訊，以及驅動程式支援的函式清單。 ODBC 也會定義 API 和 SQL 文法一致性層級，以指定驅動程式支援的廣泛功能範圍。 如需詳細資訊，請參閱[一致性層級](../../odbc/reference/develop-app/conformance-levels.md)。  
  
     請務必記住，ODBC 會為它所公開的所有功能定義一個通用介面。 因此，應用程式會包含功能專屬的程式碼，而不是 DBMS 特定的程式碼，而且可以使用任何公開這些功能的驅動程式。 其中一個優點是，當 DBMS 支援的功能增強時，不需要更新應用程式;相反地，當安裝更新的驅動程式時，應用程式會自動使用這些功能，因為它的程式碼是功能特定的，而不是特定的驅動程式或 DBMS 特定的。
