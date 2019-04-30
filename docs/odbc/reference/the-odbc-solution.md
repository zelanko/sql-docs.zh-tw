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
manager: craigg
ms.openlocfilehash: 5adf32800f4c2bc2b4a0874ca7efc22f04ffd110
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63200480"
---
# <a name="the-odbc-solution"></a>ODBC 解決方案
問題，然後是 ODBC 如何標準化資料庫存取權？ 有兩個架構的需求：  
  
-   應用程式必須能夠存取多個 Dbms，使用相同的原始程式碼，而不需要重新編譯或重新連結。  
  
-   應用程式必須能夠同時存取多個 Dbms。  
  
 還有一個更多問題的詳細資訊，因為 marketplace 實境：  
  
-   ODBC 應該公開的 DBMS 功能？ 只有功能通用於所有 Dbms 或任何可用於任何 DBMS 的功能嗎？  
  
 ODBC 會以下列方式解決這些問題︰  
  
-   **ODBC 是呼叫層級介面。** 若要解決此問題的應用程式存取多個 Dbms，使用相同的原始碼的方式，ODBC 會定義標準的 CLI。 這包含所有從 Open Group 和 ISO/IEC CLI 規格中的函式，並提供常用應用程式所需的其他函數。  
  
     不同的程式庫或驅動程式，是為了支援 ODBC 的每個 DBMS。 驅動程式會實作 ODBC API 函式。 若要使用不同的驅動程式，應用程式不必重新編譯或重新連結。 相反地，應用程式只會載入新的驅動程式，並在它呼叫的函式。 若要同時存取多個 Dbms，應用程式載入多個驅動程式。 驅動程式支援的方式是特定作業系統。 例如，在 Microsoft® Windows® 作業系統中，驅動程式都是動態連結程式庫 (Dll)。  
  
-   **ODBC 定義標準的 SQL 文法。** 除了標準的呼叫層級介面，ODBC 會定義標準的 SQL 文法。 此文法是以開啟群組 SQL CAE 規格為基礎。 兩個文法之間的差異很小，而主要是因為所需的 SQL 文法之間的差異內嵌 SQL (Open Group) 和 CLI (ODBC)。 另外還有一些擴充功能文法公開未涵蓋的 Open Group 文法的常用的語言功能。  
  
     應用程式可以提交陳述式使用 ODBC 或特定 DBMS 的文法。 如果陳述式會使用不同的 DBMS 特定文法 ODBC 文法，驅動程式會傳送至資料來源之前，先將它轉換。 不過，這類轉換很少，因為大部分的 Dbms 已使用標準 SQL 文法。  
  
-   **ODBC 提供驅動程式管理員來管理同時存取多個 Dbms。** 雖然使用驅動程式可解決問題的同時存取多個 Dbms，若要這樣做的程式碼可能相當複雜。 專為搭配所有驅動程式的應用程式無法以靜態方式連結到任何驅動程式。 相反地，它們必須在執行階段載入驅動程式，並在其中呼叫的函式，函式指標的資料表。 這種情況變得更複雜的應用程式同時使用多個驅動程式。  
  
     而不是強迫每個應用程式，若要這樣做，ODBC 會提供驅動程式管理員。 驅動程式管理員實作所有的 ODBC 函式-主要為傳遞呼叫 ODBC 函數，在 驅動程式-和以靜態方式連結至應用程式或應用程式在執行階段載入。 因此，應用程式會呼叫 ODBC 函數名稱中的驅動程式管理員 中，而不是每個驅動程式中的指標。  
  
     當應用程式需要特定的驅動程式時，它會先要求用來識別此驅動程式，然後要求驅動程式管理員載入的驅動程式在連接控制代碼。 驅動程式管理員載入驅動程式，並將每個函式的位址儲存在驅動程式。 若要呼叫 ODBC 函數的驅動程式中，應用程式在驅動程式管理員會呼叫該函式中，並將連接控制代碼傳遞驅動程式也一樣。 驅動程式管理員會使用先前儲存的地址，然後呼叫函數。  
  
-   **ODBC 會公開大量的 DBMS 功能，但不需要支援所有的驅動程式。** 如果 ODBC 公開通用於所有 Dbms 的功能，它會是沒什麼用處;畢竟，原因有許多不同的 Dbms 現存是它們有不同的功能。 如果 ODBC 公開任何 DBMS 提供每一項功能，它是不可能實作的驅動程式。  
  
     相反地，ODBC 會公開大量功能-多個支援大部分的 Dbms 層，但需要的驅動程式來實作這些功能的子集。 只有在基礎 DBMS 所支援它們，或如果他們選擇要模擬它們，驅動程式會實作其餘的功能。 因此，可以撰寫應用程式所公開之該 DBMS，使用只將所有的 Dbms，使用這些功能，或要檢查的特定功能的支援，並據以採取動作的驅動程式，利用單一 DBMS 的功能。  
  
     ODBC，讓應用程式可以判斷哪些功能驅動程式和 DBMS 的支援，提供兩個函式 (**SQLGetInfo**並**SQLGetFunctions**) 所傳回的驅動程式和 DBMS 的一般資訊功能和函式清單的驅動程式支援。 ODBC 也已經定義 API 和 SQL 文法一致性層級，其指定的驅動程式支援的功能有廣泛的範圍。 如需詳細資訊，請參閱 <<c0> [ 一致性層級](../../odbc/reference/develop-app/conformance-levels.md)。  
  
     請務必記住 ODBC 定義的所有功能，它會公開的通用介面。 基於這個原因，應用程式包含功能的特定程式碼，而不是特定 DBMS 的程式碼，並可以使用公開 （expose） 這些功能的任何驅動程式。 這個的其中一個優點是，應用程式不需要更新時增強 DBMS 所支援的功能;相反地，安裝更新的驅動程式時，應用程式會自動使用的功能因為其程式碼特定功能，不特定驅動程式或 DBMS 專屬。
