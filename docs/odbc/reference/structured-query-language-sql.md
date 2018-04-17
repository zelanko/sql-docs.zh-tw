---
title: 結構化查詢語言 (SQL) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL [ODBC]
- SQL [ODBC], about SQL
- ODBC [ODBC], SQL
ms.assetid: bebfd93e-0dc0-46b3-a531-518beb7ea976
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: babb38e88d471cedceaa94e3c6696f9b5b59dcce
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="structured-query-language-sql"></a>結構化查詢語言 (SQL) (Structured Query Language (SQL))
一般 DBMS 可讓使用者儲存、 存取及組織且有效率的方式修改資料。 一開始的 Dbms 使用者是程式設計人員。 存取儲存的資料需要 COBOL 之類的程式設計語言中撰寫程式。 這些程式通常已寫入來向非技術性使用者容易使用的介面，同時存取資料本身所需的經驗豐富的程式設計人員的服務。 不會隨便被存取的資料不太實用。  
  
 使用者未完全滿意這種情況。 雖然它們可存取資料，通常需要說服 DBMS 程式設計人員能夠撰寫特殊的軟體。 例如，如果銷售部門想要查看在上個月的銷售總額，其銷售人員的每個，而且想為了排名服務公司中的每位銷售人員的長度是由這項資訊，它有兩個選擇： 其中一個程式已經存在，允許存取完全如此一來，資訊或部門必須要求程式設計人員能夠撰寫這類程式。 在許多情況下，這是很值得，而且它們都是一次，或臨機操作，查詢是昂貴的解決方案的更多工作。 越來越多的使用者想要讓您輕鬆存取，此問題已成長越來越大。  
  
 讓使用者能夠存取臨機操作為基礎的資料需要給予他們，以表示其要求的語言。 單一要求至資料庫定義做為查詢;這類語言稱為查詢語言。 許多查詢語言開發基於此目的，但下列其中一種成為最受歡迎： 結構化查詢語言，請在 IBM 發明 1970年中。 它通常以其縮略字，SQL，識別，並會明顯同時"ess 提示-希臘文 」 和 「 延長";本手冊會使用先前的發音。 SQL 成為 standard 1986 ANSI 和 ISO 標準在 1987 年誕生;絕佳的許多資料庫管理系統中目前使用它。  
  
 雖然 SQL 解決使用者的臨機操作的需求，需資料存取程式的電腦沒有不會消失。 事實上，大部分的資料庫存取仍然 （以及） 程式設計形式的定期排程的報表和統計分析資料輸入程式例如那些訂單項目，與使用資料操作程式，例如用來協調帳戶和產生的工作順序。  
  
 這些程式也會使用 SQL，使用下列三種的技術之一：  
  
-   **內嵌 SQL**，在 SQL 陳述式會內嵌在 C 或 COBOL 這類主機語言。  
  
-   **SQL 模組**，編譯的 dbms 和從主機語言呼叫哪一個 SQL 陳述式中。  
  
-   **呼叫層級介面**，或 CLI，其中包含函式呼叫將 SQL 陳述式新增至 DBMS 和擷取 DBMS 的結果。  
  
> [!NOTE]  
>  它是一詞呼叫層級介面會用來取代應用程式發展介面 (API)，歷程記錄不小心另一種說法相同的動作。 API 用來描述本身的 SQL 資料庫世界： SQL 是 dbms 的 API。  
  
 這些選項，雖然大部分主要 Dbms 支援專屬 Cli，是最常使用內嵌的 SQL。  
  
 此章節包含下列主題。  
  
-   [處理 SQL 陳述式](../../odbc/reference/processing-a-sql-statement.md)  
  
-   [內嵌 SQL](../../odbc/reference/embedded-sql.md)  
  
-   [SQL 模組](../../odbc/reference/sql-modules.md)  
  
-   [呼叫層級介面](../../odbc/reference/call-level-interfaces.md)
