---
title: 建構可互通的 SQL 陳述式 |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002238"
---
# <a name="constructing-interoperable-sql-statements"></a>建構可互通的 SQL 陳述式
如先前章節中所述，互通的應用程式應該使用 ODBC SQL 文法。 超過使用此文法，不過，許多其他問題所面對互通的應用程式。 例如，應用程式的作用為何想要使用的功能，例如外部聯結中，不支援的所有資料來源？  
  
 此時，應用程式撰寫者必須先決定所需的語言功能，以及何者為選擇性。 在大部分情況下，如果特定的驅動程式不支援的功能所需的應用程式，應用程式只會拒絕以該驅動程式來執行。 不過，如果是選擇性的功能，應用程式可以解決此功能。 比方說，它可能會停用這些介面中的部分，讓使用者在使用該功能。  
  
 若要判斷支援哪些功能，應用程式會開始藉由呼叫**SQLGetInfo** SQL_SQL_CONFORMANCE 選項。 SQL 一致性層級可讓應用程式都支援 SQL 廣泛檢視。 若要改善此檢視中，應用程式會呼叫**SQLGetInfo**任何數目的其他選項。 如需這些選項的完整清單，請參閱 < [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函式描述。 最後， **SQLGetTypeInfo**傳回資料來源所支援的資料類型的相關資訊。 下列各節列出許多可能建構可互通的 SQL 陳述式時，應用程式必須留意的因素。  
  
 此章節包含下列主題。  
  
-   [目錄和結構描述的使用方式](../../../odbc/reference/develop-app/catalog-and-schema-usage.md)  
  
-   [目錄位置](../../../odbc/reference/develop-app/catalog-position.md)  
  
-   [引號識別碼](../../../odbc/reference/develop-app/quoted-identifiers.md)  
  
-   [識別碼大小寫](../../../odbc/reference/develop-app/identifier-case.md)  
  
-   [逸出序列](../../../odbc/reference/develop-app/escape-sequences.md)  
  
-   [常值首碼及尾碼](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)  
  
-   [程序呼叫中的參數標記](../../../odbc/reference/develop-app/parameter-markers-in-procedure-calls.md)  
  
-   [DDL 陳述式](../../../odbc/reference/develop-app/ddl-statements.md)
