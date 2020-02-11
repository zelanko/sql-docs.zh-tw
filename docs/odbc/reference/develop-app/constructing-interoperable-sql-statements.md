---
title: 建立可互通的 SQL 語句 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 87ad7b8b36c80d86e0c3ac0335dd6f348a30c7bc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68002238"
---
# <a name="constructing-interoperable-sql-statements"></a>建構可互通的 SQL 陳述式
如上一節所述，互通的應用程式應該使用 ODBC SQL 文法。 不過，除了使用此文法以外，還有一些其他問題是由互通的應用程式所面臨。 例如，如果應用程式想要使用不受所有資料來源支援的功能（例如外部聯結），該怎麼辦？  
  
 此時，應用程式撰寫者必須決定哪些語言功能是必要的，哪些是選擇性的。 在大多數情況下，如果特定驅動程式不支援應用程式所需的功能，應用程式就會拒絕使用該驅動程式來執行。 不過，如果這是選擇性的功能，應用程式可以解決此功能。 例如，它可能會停用介面的這些部分，讓使用者能夠使用此功能。  
  
 為了判斷支援哪些功能，應用程式一開始會使用 SQL_SQL_CONFORMANCE 選項來呼叫**SQLGetInfo** 。 SQL 一致性層級會為應用程式提供支援 SQL 的廣泛觀點。 若要精簡此視圖，應用程式會使用其他許多選項來呼叫**SQLGetInfo** 。 如需這些選項的完整清單，請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函數描述。 最後， **SQLGetTypeInfo**會傳回資料來源所支援之資料類型的相關資訊。 下列各節列出當您在建立可互通的 SQL 語句時，應用程式應該監看的一些可能因素。  
  
 此章節包含下列主題。  
  
-   [目錄和結構描述的使用方式](../../../odbc/reference/develop-app/catalog-and-schema-usage.md)  
  
-   [目錄位置](../../../odbc/reference/develop-app/catalog-position.md)  
  
-   [引號識別碼](../../../odbc/reference/develop-app/quoted-identifiers.md)  
  
-   [識別碼大小寫](../../../odbc/reference/develop-app/identifier-case.md)  
  
-   [逸出序列](../../../odbc/reference/develop-app/escape-sequences.md)  
  
-   [常值首碼及尾碼](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)  
  
-   [程序呼叫中的參數標記](../../../odbc/reference/develop-app/parameter-markers-in-procedure-calls.md)  
  
-   [DDL 陳述式](../../../odbc/reference/develop-app/ddl-statements.md)
