---
title: 建構可互通的 SQL 陳述式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], constructing statements
ms.assetid: dee6f7e2-bcc4-4c74-8c7c-12aeda8a90eb
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 257440b78a466178d09e954e9aed5b9385325b8a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32909953"
---
# <a name="constructing-interoperable-sql-statements"></a>建構可互通的 SQL 陳述式
如先前章節中所述，互通的應用程式應使用 ODBC SQL 文法。 不過，超過使用此文法，產生了一些額外的問題正面臨互通的應用程式。 例如，應用程式的作用為何想要使用的功能，例如外部聯結中，不支援的所有資料來源？  
  
 此時，應用程式寫入器必須進行決策所需的語言功能，而這是選擇性。 在大部分情況下，如果特定的驅動程式不支援應用程式時，所需要的功能的應用程式只要拒絕該驅動程式執行。 不過，如果是選擇性功能，應用程式可以解決功能。 例如，它可能會停用這些部分的介面，讓使用者在使用的功能。  
  
 若要判斷支援哪些功能，應用程式啟動藉由呼叫**SQLGetInfo** SQL_SQL_CONFORMANCE 選項。 SQL 一致性層級可讓應用程式都支援 SQL 廣泛檢視。 若要精簡這個檢視中，應用程式會呼叫**SQLGetInfo**與任何數量的其他選項。 如需這些選項的完整清單，請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函式描述。 最後， **SQLGetTypeInfo**傳回的資料來源所支援的資料類型的相關資訊。 下列各節列出許多可能的應用程式應該監看建構可互通的 SQL 陳述式時的因素。  
  
 此章節包含下列主題。  
  
-   [目錄和結構描述的使用方式](../../../odbc/reference/develop-app/catalog-and-schema-usage.md)  
  
-   [目錄位置](../../../odbc/reference/develop-app/catalog-position.md)  
  
-   [引號識別碼](../../../odbc/reference/develop-app/quoted-identifiers.md)  
  
-   [識別碼大小寫](../../../odbc/reference/develop-app/identifier-case.md)  
  
-   [逸出序列](../../../odbc/reference/develop-app/escape-sequences.md)  
  
-   [常值首碼及尾碼](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)  
  
-   [程序呼叫中的參數標記](../../../odbc/reference/develop-app/parameter-markers-in-procedure-calls.md)  
  
-   [DDL 陳述式](../../../odbc/reference/develop-app/ddl-statements.md)
