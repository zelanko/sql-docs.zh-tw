---
title: 建構可互操作的 SQL 語句 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], constructing statements
ms.assetid: dee6f7e2-bcc4-4c74-8c7c-12aeda8a90eb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1eccdef63b7d06a456a07f5f1a9ccad987d2de29
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282510"
---
# <a name="constructing-interoperable-sql-statements"></a>建構可互通的 SQL 陳述式
如前一節所述,可互通的應用程式應使用ODBC SQL語法。 但是,除了使用此語法之外,可互操作的應用程式還面臨著許多其他問題。 例如,如果應用程式想要使用並非所有數據源都支援的功能(如外部聯接),它該怎麼辦?  
  
 此時,應用程式編寫器必須做出一些決定,確定哪些語言功能是必需的,哪些是可選的。 在大多數情況下,如果特定驅動程式不支援應用程式所需的功能,則應用程式只是拒絕使用該驅動程式運行。 但是,如果該功能是可選的,則應用程式可以圍繞該功能進行處理。 例如,它可能會禁用允許使用者使用該功能的介面部分。  
  
 要確定支援哪些功能,應用程式首先使用SQL_SQL_CONFORMANCE選項調用**SQLGetInfo。** SQL 一致性級別為應用程式提供了支援 SQL 的廣泛檢視。 要優化此檢視,應用程式使用許多其他選項中的任何一個調用**SQLGetInfo。** 有關這些選項的完整清單,請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函數說明。 最後 **,SQLGetTypeInfo**返回有關數據源支援的數據類型的資訊。 以下各節列出了應用程式在建構可互操作 SQL 語句時應注意的一些可能因素。  
  
 此章節包含下列主題。  
  
-   [目錄和結構描述的使用方式](../../../odbc/reference/develop-app/catalog-and-schema-usage.md)  
  
-   [目錄位置](../../../odbc/reference/develop-app/catalog-position.md)  
  
-   [引號識別碼](../../../odbc/reference/develop-app/quoted-identifiers.md)  
  
-   [識別碼大小寫](../../../odbc/reference/develop-app/identifier-case.md)  
  
-   [逸出序列](../../../odbc/reference/develop-app/escape-sequences.md)  
  
-   [常值首碼及尾碼](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)  
  
-   [程序呼叫中的參數標記](../../../odbc/reference/develop-app/parameter-markers-in-procedure-calls.md)  
  
-   [DDL 陳述式](../../../odbc/reference/develop-app/ddl-statements.md)
