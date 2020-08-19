---
description: 結構化查詢語言 (SQL) (Structured Query Language (SQL))
title: 結構化查詢語言 (SQL)  (SQL) |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c68f14bd3e1ae5df29f52332d29393bf15c3b665
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428970"
---
# <a name="structured-query-language-sql"></a>結構化查詢語言 (SQL) (Structured Query Language (SQL))
一般 DBMS 可讓使用者以組織、有效率的方式來儲存、存取及修改資料。 原本，Dbms 的使用者是程式設計人員。 存取以程式設計語言（例如 COBOL）撰寫程式時，所需的已儲存資料。 雖然這些程式通常是為了向非技術性使用者提供易記的介面，但對資料本身的存取必須是有知識的程式設計師的服務。 資料的臨時存取並不實用。  
  
 使用者在這種情況下並不完全滿意。 雖然它們可以存取資料，但通常需要說服 DBMS 程式設計師撰寫特殊的軟體。 例如，如果銷售部門想要查看每個銷售人員在上個月的總銷售額，而且希望這項資訊依每位銷售人員在公司內的服務長度排列順序，則有兩個選擇：可能是已存在的方案允許以這種方式存取訊號，或是部門必須要求程式設計師撰寫這類程式。 在許多情況下，這比所需的還多，而且一律是一次或臨機操作查詢的昂貴解決方案。 隨著越來越多的使用者想要輕鬆存取，這個問題的成長和放大。  
  
 允許使用者以臨機操作方式存取資料，需要提供他們用來表達其要求的語言。 資料庫的單一要求會定義為查詢;這種語言稱為查詢語言。 許多查詢語言都是基於這個目的而開發的，但其中一種是最受歡迎的：結構化查詢語言 (SQL) ，在1970年代的 IBM 創造。 它比較常見的縮寫為 SQL，而且會被視為「ess-提示-ell」和「sequel」。 SQL 已成為1986的 ANSI 標準和1987中的 ISO 標準;在許多資料庫管理系統中，今天都使用它。  
  
 雖然 SQL 解決了使用者的臨機操作需求，但是電腦程式的資料存取需求不會消失。 事實上，大部分的資料庫存取仍 (，並以定期排程的報表和統計分析、資料輸入程式（例如用於訂單輸入的資料輸入程式和資料操作程式，例如用於協調帳戶和產生工作訂單的程式）進行) 程式設計。  
  
 這些程式也會使用 SQL，並使用下列三種技術之一：  
  
-   **內嵌 sql**，其中 sql 語句內嵌于主機語言，例如 C 或 COBOL。  
  
-   **Sql 模組**，其中 sql 語句會在 DBMS 上編譯，並從主機語言呼叫。  
  
-   **呼叫層級介面**或 CLI，其中包含呼叫來將 SQL 語句傳遞至 dbms 以及從 dbms 取出結果的函式。  
  
> [!NOTE]  
>  使用詞彙呼叫層級介面（而不是應用程式開發介面） (API) ，另一個詞彙則是相同的。 在資料庫世界中，API 是用來描述 SQL 本身： SQL 是 DBMS 的 API。  
  
 在這些選擇中，內嵌 SQL 是最常用的，但大部分的主要 Dbms 都支援專屬 Cli。  
  
 此章節包含下列主題。  
  
-   [處理 SQL 語句](../../odbc/reference/processing-a-sql-statement.md)  
  
-   [內嵌 SQL](../../odbc/reference/embedded-sql.md)  
  
-   [SQL 模組](../../odbc/reference/sql-modules.md)  
  
-   [呼叫層級介面](../../odbc/reference/call-level-interfaces.md)
