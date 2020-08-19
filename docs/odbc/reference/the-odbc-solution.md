---
description: ODBC 解決方案
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f1a1c216dc67c33eadc9a058263087978f176297
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428860"
---
# <a name="the-odbc-solution"></a>ODBC 解決方案
接下來的問題是 ODBC 如何將資料庫存取標準化？ 架構需求有兩種：  
  
-   應用程式必須能夠使用相同的原始程式碼來存取多個 Dbms，而不需要重新編譯或重新連結。  
  
-   應用程式必須能夠同時存取多個 Dbms。  
  
 另外還有一個問題，因為 marketplace 事實：  
  
-   ODBC 應公開哪些 DBMS 功能？ 只有所有 Dbms 或任何 DBMS 都有通用的功能？  
  
 ODBC 可透過下列方式解決這些問題：  
  
-   **ODBC 是呼叫層級的介面。** 為了解決應用程式如何使用相同原始程式碼來存取多個 Dbms 的問題，ODBC 定義了標準的 CLI。 這包含 CLI 規格中 Open Group 和 ISO/IEC 的所有函式，並提供應用程式通常需要的其他功能。  
  
     每個支援 ODBC 的 DBMS 都需要不同的程式庫或驅動程式。 驅動程式會實作用於 ODBC API 中的函式。 若要使用不同的驅動程式，則不需要重新編譯或重新連結應用程式。 相反地，應用程式只會載入新的驅動程式，並在其中呼叫函數。 若要同時存取多個 Dbms，應用程式會載入多個驅動程式。 支援的驅動程式是作業系統特定的。 例如，在 Microsoft® Windows®作業系統上，驅動程式是 (Dll) 的動態連結程式庫。  
  
-   **ODBC 會定義標準的 SQL 文法。** 除了標準的呼叫層級介面，ODBC 也會定義標準的 SQL 文法。 此文法以 Open Group SQL CAE 規格為基礎。 這兩個文法之間的差異很小，主要是因為內嵌 SQL (Open Group) 和 CLI (ODBC) 所需的 SQL 文法之間的差異。 此外，也有一些文法的擴充功能，可公開開放式群組文法未涵蓋的常用語言功能。  
  
     應用程式可以使用 ODBC 或 DBMS 特定文法來提交語句。 如果語句使用與 DBMS 特定文法不同的 ODBC 文法，驅動程式會先轉換它，然後再將它傳送到資料來源。 不過，這類轉換很罕見，因為大部分 Dbms 都已經使用標準的 SQL 文法。  
  
-   **ODBC 提供驅動程式管理員來管理對多個 Dbms 的同時存取。** 雖然使用驅動程式可解決同時存取多個 Dbms 的問題，但是執行這項作業的程式碼可能很複雜。 設計來搭配所有驅動程式使用的應用程式，無法以靜態方式連結到任何驅動程式。 相反地，它們必須在執行時間載入驅動程式，並透過函式指標的表格來呼叫它們中的函式。 如果應用程式同時使用多個驅動程式，則情況會變得更複雜。  
  
     ODBC 會提供驅動程式管理員，而不是強制每個應用程式執行這項作業。 驅動程式管理員會將所有的 ODBC 函式（大多是在驅動程式中對 ODBC 函式的傳遞呼叫）執行，而且會以靜態方式連結至應用程式，或在執行時間由應用程式載入。 因此，應用程式會在驅動程式管理員中依名稱呼叫 ODBC 函數，而不是每個驅動程式中的指標。  
  
     當應用程式需要特定驅動程式時，它會先要求用來識別驅動程式的連接控制碼，然後要求驅動程式管理員載入驅動程式。 驅動程式管理員會載入驅動程式，並將每個函式的位址儲存在驅動程式中。 若要在驅動程式中呼叫 ODBC 函數，應用程式會在驅動程式管理員中呼叫該函式，並傳遞驅動程式的連接控制碼。 然後，驅動程式管理員會使用先前儲存的位址來呼叫該函式。  
  
-   **ODBC 公開大量的 DBMS 功能，但不需要驅動程式來支援所有功能。** 如果 ODBC 只公開所有 Dbms 通用的功能，則很少使用;畢竟，現在有許多不同的 Dbms 存在，是因為它們具有不同的功能。 如果 ODBC 公開任何 DBMS 中可用的每項功能，驅動程式就不可能執行。  
  
     相反地，ODBC 會公開大量的功能，大部分 Dbms 都支援這些功能，但只需要驅動程式來執行這些功能的子集。 驅動程式只有在基礎 DBMS 支援或選擇模擬它們時，才會執行其餘功能。 因此，您可以撰寫應用程式來利用該 DBMS 的驅動程式所公開的單一 DBMS 功能，僅使用所有 Dbms 所使用的功能，或檢查特定功能的支援，並據以回應。  
  
     為了讓應用程式能夠判斷驅動程式和 DBMS 支援哪些功能，ODBC 提供兩個函式 (**SQLGetInfo** 和 **SQLGetFunctions**) ，以傳回有關驅動程式和 dbms 功能的一般資訊，以及驅動程式支援的函式清單。 ODBC 也會定義 API 和 SQL 文法一致性層級，以指定驅動程式支援的廣泛功能範圍。 如需詳細資訊，請參閱 [一致性層級](../../odbc/reference/develop-app/conformance-levels.md)。  
  
     請務必記住，ODBC 會針對其公開的所有功能定義通用介面。 因此，應用程式包含特定功能的程式碼，而不是 DBMS 特定的程式碼，而且可以使用任何公開這些功能的驅動程式。 其中一個優點是，當 DBMS 支援的功能增強時，不需要更新應用程式。相反地，安裝更新的驅動程式時，應用程式會自動使用這些功能，因為它的程式碼是特定功能，而不是特定的驅動程式或 DBMS 特定的。
