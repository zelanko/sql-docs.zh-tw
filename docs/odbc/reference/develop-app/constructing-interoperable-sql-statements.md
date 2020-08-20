---
description: 建構可互通的 SQL 陳述式
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: acdb0f360242c4c9953804cb768214b0a78251dd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465880"
---
# <a name="constructing-interoperable-sql-statements"></a>建構可互通的 SQL 陳述式
如上一節所述，互通的應用程式應該使用 ODBC SQL 文法。 不過，除了使用此文法之外，還有一些其他問題是由互通的應用程式所面臨的。 例如，如果應用程式想要使用不受所有資料來源支援的功能（例如外部聯結），該應用程式會執行什麼作業？  
  
 此時，應用程式撰寫者必須針對需要哪些語言功能以及哪些是選擇性的，做出一些決定。 在大部分情況下，如果特定的驅動程式不支援應用程式所需的功能，應用程式就會拒絕使用該驅動程式來執行。 但是，如果此功能是選擇性的，則應用程式可以解決此功能。 例如，它可能會停用允許使用者使用此功能的介面部分。  
  
 為了判斷支援的功能，應用程式會從使用 SQL_SQL_CONFORMANCE 選項呼叫 **SQLGetInfo** 開始。 SQL 一致性層級可讓應用程式廣泛地瞭解支援的 SQL。 若要精簡此視圖，應用程式會使用其他許多選項來呼叫 **SQLGetInfo** 。 如需這些選項的完整清單，請參閱 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 函數描述。 最後， **SQLGetTypeInfo** 會傳回資料來源所支援資料類型的相關資訊。 下列各節列出應用程式在建立可互通的 SQL 語句時，應注意的一些可能因素。  
  
 此章節包含下列主題。  
  
-   [目錄和結構描述的使用方式](../../../odbc/reference/develop-app/catalog-and-schema-usage.md)  
  
-   [目錄位置](../../../odbc/reference/develop-app/catalog-position.md)  
  
-   [引號識別碼](../../../odbc/reference/develop-app/quoted-identifiers.md)  
  
-   [識別碼大小寫](../../../odbc/reference/develop-app/identifier-case.md)  
  
-   [Escape 序列](../../../odbc/reference/develop-app/escape-sequences.md)  
  
-   [常值首碼及尾碼](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)  
  
-   [程序呼叫中的參數標記](../../../odbc/reference/develop-app/parameter-markers-in-procedure-calls.md)  
  
-   [DDL 陳述式](../../../odbc/reference/develop-app/ddl-statements.md)
