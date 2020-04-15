---
title: 結構化查詢語言 (SQL) |微軟文件
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
ms.openlocfilehash: c669b4424271fc1a3c91dea37159474fb52b97cd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293388"
---
# <a name="structured-query-language-sql"></a>結構化查詢語言 (SQL) (Structured Query Language (SQL))
典型的 DBMS 允許使用者以有組織的高效方式存儲、訪問和修改數據。 最初,DBMS 的使用者是程式師。 存取儲存的資料需要用程式設計語言(如 COBOL)編寫程式。 雖然這些程式通常是為向非技術使用者提供友好的介面而編寫的,但訪問數據本身需要知識淵博的程式師的服務。 隨意訪問數據是不現實的。  
  
 使用者並不完全滿意這種情況。 雖然他們可以訪問數據,但通常需要說服 DBMS 程式師編寫特殊軟體。 例如,如果銷售部門希望查看每個銷售人員上個月的總銷售額,並希望此資訊按公司中每個銷售人員的服務年限順序排列,則它有兩種選擇:要麼已經存在允許以這種方式訪問資訊的程式,要麼部門必須要求程式員編寫此類程式。 在許多情況下,這是比它的價值更多的工作,它總是一個昂貴的解決方案,一次性或臨時,查詢。 隨著越來越多的使用者希望輕鬆訪問,此問題變得越來越大。  
  
 允許使用者臨時訪問數據,需要為他們提供表達請求的語言。 對資料庫的單個請求定義為查詢;對資料庫的單個請求將定義為查詢。這種語言稱為查詢語言。 許多查詢語言都是為此目的開發的,但其中一種成為最流行的:結構化查詢語言,在 20 世紀 70 年代在 IBM 中發明。 它更常見的縮寫為 SQL,並且發音為「es-cue-ell」和「sequel」。。 SQL 於 1986 年成為 ANSI 標準,1987 年成為 ISO 標準;它今天在許多資料庫管理系統中使用。  
  
 儘管 SQL 解決了使用者的臨時需求,但電腦程式對數據訪問的需求並沒有消失。 事實上,大多數資料庫訪問仍然是(並且)以定期計劃的報告和統計分析的形式程式設計,數據輸入程式(如用於訂單輸入的程式)和數據操作程式(如用於對帳和生成工作訂單的程式)。  
  
 這些程式還使用 SQL,使用以下三種技術之一:  
  
-   **嵌入式 SQL**,其中 SQL 語句嵌入在宿主語言(如 C 或 COBOL)中。  
  
-   **SQL 模組**,其中 SQL 語句在 DBMS 上編譯,並從宿主語言調用。  
  
-   **調用級介面**或 CLI,它由調用的函數組成,這些函數用於將 SQL 語句傳遞給 DBMS 並從 DBMS 檢索結果。  
  
> [!NOTE]  
>  使用術語調用級介面而不是應用程式程式設計介面 (API) 是一個歷史事故,這是另一個相同術語的術語。 在資料庫世界中,API 用於描述 SQL 本身:SQL 是 DBMS 的 API。  
  
 在這些選擇中,嵌入式 SQL 是最常用的,儘管大多數主要 DBMS 都支援專有的 CLIs。  
  
 此章節包含下列主題。  
  
-   [處理 SQL 語句](../../odbc/reference/processing-a-sql-statement.md)  
  
-   [內嵌 SQL](../../odbc/reference/embedded-sql.md)  
  
-   [SQL 模組](../../odbc/reference/sql-modules.md)  
  
-   [呼叫層級介面](../../odbc/reference/call-level-interfaces.md)
