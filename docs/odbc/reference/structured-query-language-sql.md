---
title: 結構化查詢語言 (SQL) （SQL） |Microsoft Docs
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
ms.openlocfilehash: 6cae344e97bf6e5dc8affbf164f80eb8935846e1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68019036"
---
# <a name="structured-query-language-sql"></a>結構化查詢語言 (SQL) (Structured Query Language (SQL))
一般的 DBMS 可讓使用者以組織、有效率的方式來儲存、存取和修改資料。 原本，Dbms 的使用者就是程式設計人員。 存取儲存的資料需要以程式設計語言（例如 COBOL）撰寫程式。 雖然這些程式通常是為了為非技術性使用者提供易記的介面而撰寫的，但資料本身的存取權需要有豐富的程式設計人員服務。 資料的偶爾存取並不實用。  
  
 使用者並不完全滿意這種情況。 雖然他們可以存取資料，但通常需要說服 DBMS 程式設計人員撰寫特殊軟體。 例如，如果銷售部門想要查看上個月中每個銷售人員的總銷售額，並希望此資訊依每位銷售人員在公司中的服務長度排序，則有兩個選擇：程式已存在，允許以這種方式存取訊號，或部門必須要求程式設計人員撰寫這類程式。 在許多情況下，這是比所需更多的工作，而且對於單次或臨機操作的查詢而言，它一律是昂貴的解決方案。 因為越來越多的使用者想要輕鬆存取，所以這個問題的成長和更大。  
  
 允許使用者以臨機操作的方式存取資料，需要提供他們一個語言來表達其要求。 資料庫的單一要求會定義為查詢;這種語言稱為查詢語言。 許多查詢語言都是基於此目的而開發，但其中一種是最受歡迎的：結構化查詢語言 (SQL)，在第1年代的 IBM 中正式推出。 它比較常見的縮寫為 SQL，而且會同時被視為 "ess-ell" 和 "sequel"。 SQL 成為1986中的 ANSI 標準，以及1987中的 ISO 標準;今天在很多資料庫管理系統中都使用它。  
  
 雖然 SQL 已解決使用者的臨機操作需求，但電腦程式的資料存取需求也不會消失。 事實上，大部分的資料庫存取還是以程式設計的方式（也就是），以定期排程的報表和統計分析、資料輸入程式（例如用於訂單輸入的專案）和資料操作程式（例如用來協調帳戶和產生工作訂單。  
  
 這些程式也會使用 SQL，使用下列三種技術之一：  
  
-   **內嵌 sql**，其中 SQL 語句內嵌在 C 或 COBOL 之類的主機語言中。  
  
-   **Sql 模組**，其中 sql 語句會在 DBMS 上編譯，並從主機語言呼叫。  
  
-   **呼叫層級介面**或 CLI，其中包含呼叫的函式，以將 SQL 語句傳遞至 dbms，並從 dbms 抓取結果。  
  
> [!NOTE]  
>  這是一項歷程記錄意外，會使用「呼叫層級介面」（而非應用程式開發介面（API）），另一個詞彙則適用于相同的事物。 在資料庫世界中，API 是用來描述 SQL 本身： SQL 是 DBMS 的 API。  
  
 在這些選擇中，內嵌 SQL 最常使用，雖然大部分的主要 Dbms 都支援專屬 Cli。  
  
 此章節包含下列主題。  
  
-   [處理 SQL 語句](../../odbc/reference/processing-a-sql-statement.md)  
  
-   [內嵌 SQL](../../odbc/reference/embedded-sql.md)  
  
-   [SQL 模組](../../odbc/reference/sql-modules.md)  
  
-   [呼叫層級介面](../../odbc/reference/call-level-interfaces.md)
