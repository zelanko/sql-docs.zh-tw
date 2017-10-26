---
title: "ODBC 解決方案 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], using ODBC
ms.assetid: 34b80790-e010-4b90-8eaa-03189f5d8986
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c7288fcb9fad7b2567f7fec16cf0f407b2f6b2e4
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="the-odbc-solution"></a>ODBC 方案
這個問題，然後是 ODBC 方式標準化資料庫存取權？ 有兩個架構的需求：  
  
-   應用程式必須能夠存取多個使用相同的原始碼，而不需要重新編譯或重新連結的 Dbms。  
  
-   應用程式必須能夠同時存取多個 Dbms。  
  
 還有一個更多問題，因為 marketplace 現實：  
  
-   ODBC 應該公開的 DBMS 功能？ 只有功能通用於所有 Dbms 或任何功能，可在任何 DBMS 嗎？  
  
 ODBC 會以下列方式解決這些問題：  
  
-   **ODBC 是在呼叫層級介面。** 若要解決此問題的應用程式如何存取多個使用相同的原始碼的 Dbms，ODBC 會定義標準 CLI。 這包含所有從 Open Group 和 ISO/IEC CLI 規格中的函式，並提供常用應用程式所需的其他函數。  
  
     不同的程式庫或驅動程式，無須針對每個支援 ODBC 的 DBMS。 驅動程式會實作 ODBC API 函式。 若要使用不同的驅動程式，應用程式無須重新編譯或重新連結。 相反地，應用程式只會載入新的驅動程式，並在它呼叫函式。 若要同時存取多個 Dbms，應用程式會載入多個驅動程式。 驅動程式如何支援是特定作業系統。 例如，Microsoft® Windows® 作業系統上，驅動程式是動態連結程式庫 (Dll)。  
  
-   **ODBC 定義標準的 SQL 文法。** 除了標準的呼叫層級介面，ODBC 會定義標準的 SQL 文法。 此文法以開啟群組 SQL CAE 規格為基礎。 兩個文法之間的差異是次要和主要是因為所需的 SQL 文法之間的差異內嵌 SQL (Open Group) 和 CLI (ODBC)。 另外還有一些擴充功能未涵蓋的 Open Group 文法通常可用的語言功能公開文法。  
  
     應用程式可以提交陳述式中使用 ODBC 或特定 DBMS 的文法。 如果陳述式使用 ODBC 文法的不同 DBMS 專屬文法，驅動程式會傳送至資料來源之前，先將它轉換。 不過，這類轉換很少，因為大部分 Dbms 已經使用標準 SQL 文法。  
  
-   **ODBC 提供驅動程式管理員管理多個 Dbms 同時存取。** 雖然使用驅動程式可解決此問題的同時存取多個 Dbms，可能相當複雜的程式碼，若要這樣做。 專為搭配使用的所有驅動程式的應用程式無法以靜態方式連結到任何驅動程式。 相反地，必須在執行階段載入驅動程式，並在這些呼叫的函式的函式指標的資料表。 這種情況會變得更複雜應用程式同時使用多個驅動程式。  
  
     而不是強迫若要這樣做的每個應用程式，ODBC 會提供驅動程式管理員。 驅動程式管理員會實作所有 ODBC 函數 — 當做傳遞 ODBC 驅動程式中的函式呼叫，並以靜態方式連結到應用程式或應用程式在執行階段載入。 因此，應用程式呼叫 ODBC 函數，依名稱驅動程式管理員 中，而不是由每個驅動程式中的指標。  
  
     當應用程式需要特定的驅動程式時，它會先要求連接控制代碼，用來識別此驅動程式，然後要求驅動程式管理員載入的驅動程式。 驅動程式管理員會載入驅動程式，並將驅動程式中的每個函式的位址。 若要呼叫 ODBC 函數驅動程式中，應用程式會呼叫此函式在驅動程式管理員，並將連接控制代碼傳遞驅動程式。 驅動程式管理員會使用先前儲存的位址，然後呼叫函數。  
  
-   **ODBC 公開大量的 DBMS 功能，但不需要支援所有的驅動程式。** 如果 ODBC 公開通用於所有 Dbms 的功能，它會是很少使用。畢竟，原因有許多不同的 Dbms 今日讓是它們有不同的功能。 如果 ODBC 公開可用在任何 DBMS 中的每一項功能，將不可能的實作中的驅動程式。  
  
     相反地，ODBC 會公開大量的功能 — 超過大部分 Dbms 所支援，但需要的驅動程式來實作這些功能的子集。 驅動程式實作其餘的功能，或他們選擇以模擬它們才支援這些功能基礎 DBMS。 因此，應用程式可以撰寫利用單一 DBMS 的功能，因為該 DBMS，來使用所有的 Dbms 所使用的功能，或是檢查的特定功能的支援，並據以採取動作的驅動程式所公開。  
  
     ODBC 應用程式就可以判斷哪些功能的驅動程式和 DBMS 支援，以便提供兩個函式 (**SQLGetInfo**和**SQLGetFunctions**) 會在傳回的驅動程式和 DBMS 的一般資訊功能和函數的清單的驅動程式支援。 ODBC 也定義應用程式開發介面和 SQL 文法一致性層級，其指定的驅動程式支援的功能有廣泛的範圍。 如需詳細資訊，請參閱[一致性層級](../../odbc/reference/develop-app/conformance-levels.md)。  
  
     請務必記得 ODBC 定義的所有功能，它會公開的通用介面。 因為這個緣故，應用程式包含特定功能的程式碼，不 DBMS 專屬的程式碼，並可以使用任何這些公開功能的驅動程式。 這其中一個優點是應用程式不需要更新時增強 DBMS 所支援的功能;相反地，安裝更新的驅動程式時，應用程式會自動使用功能因為其程式碼特定功能、 不特定驅動程式或 DBMS 專屬。

