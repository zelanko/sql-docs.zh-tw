---
title: 結構化查詢語言 (SQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC]
- SQL [ODBC], about SQL
- ODBC [ODBC], SQL
ms.assetid: bebfd93e-0dc0-46b3-a531-518beb7ea976
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 86f9dd843171c02654302694c669f40b6b51ab78
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63232084"
---
# <a name="structured-query-language-sql"></a>結構化查詢語言 (SQL) (Structured Query Language (SQL))
一般的 DBMS 可讓使用者儲存、 存取和修改資料，以有組織、 有效率的方式。 一開始，Dbms 的使用者是程式設計人員。 存取儲存的資料需要 COBOL 之類的程式設計語言中撰寫程式。 雖然這些程式通常撰寫來向非技術性使用者容易使用的介面，資料本身的存取權所需的知識豐富的程式設計人員的服務。 輕鬆存取的資料不是實用的。  
  
 使用者無法完全滿意這種情況。 雖然它們無法存取資料，通常需要說服 DBMS 程式設計人員能夠撰寫特殊的軟體。 例如，如果銷售部門想要看到在上個月的銷售總額，其銷售人員的每個，而且想要這項資訊的公司中的服務的每位銷售人員的長度依排序順序，它會有兩個選擇：程式已經存在於允許完全如此一來，要存取的資訊，或是部門必須要求程式設計人員能夠撰寫這類程式。 在許多情況下，這會是很值得，而且它們都是一次性，或臨機操作，查詢是昂貴的解決方案的更多工作。 所越來越多的使用者想要輕鬆地存取，此問題已越來越大。  
  
 允許使用者存取臨機操作為基礎的資料時，需要提供他們的語言來表達其要求。 資料庫的單一要求被指查詢;這類語言稱為查詢語言。 基於此目的，開發許多查詢語言，但其中一種成為最受歡迎：結構化的查詢語言，在 1970 年代發明了 ibm。 它通常已知其縮略字，SQL，作為 「 ess-提示-ell 」 和 「 後方 」 的發音。 SQL 成為標準在 1986 年 ANSI 和 ISO 標準中 1987;絕佳的許多資料庫管理系統中目前使用它。  
  
 雖然 SQL 解決使用者的臨機操作的需求，需要資料存取程式的電腦沒有不會消失。 事實上，大部分的資料庫存取權仍然 （以及） 程式設計形式的定期排程的報表和統計分析的資料輸入程式與這類訂單輸入和資料使用操作程式，例如用來協調帳戶和產生的工作順序。  
  
 這些程式也會使用 SQL，使用下列三種技術之一：  
  
-   **內嵌 SQL**，在 SQL 陳述式內嵌在主應用程式語言如 C 或 COBOL。  
  
-   **SQL 模組**、 哪些 SQL 陳述式是在 DBMS 編譯並且從主應用程式語言中。  
  
-   **呼叫層級介面**，或 CLI，其中包含函式，將 SQL 陳述式對 DBMS 和 DBMS 從擷取的結果。  
  
> [!NOTE]  
>  它是一詞會使用呼叫層級介面，而不是應用程式發展介面 (API) 的歷程記錄不小心的是相同的另一種說法。 在資料庫的世界中，API 用來描述 SQL 本身：SQL 是以 DBMS 的 API。  
  
 這些選項中，雖然大部分主要 Dbms 支援專屬的 Cli，是最常使用內嵌的 SQL。  
  
 此章節包含下列主題。  
  
-   [處理 SQL 陳述式](../../odbc/reference/processing-a-sql-statement.md)  
  
-   [內嵌 SQL](../../odbc/reference/embedded-sql.md)  
  
-   [SQL 模組](../../odbc/reference/sql-modules.md)  
  
-   [呼叫層級介面](../../odbc/reference/call-level-interfaces.md)
