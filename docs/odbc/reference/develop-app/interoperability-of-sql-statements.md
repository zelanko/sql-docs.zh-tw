---
title: SQL 陳述式的互通性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC]
- interoperability of SQL statements [ODBC], about interoperability
ms.assetid: 3b24c499-829c-4e65-90cf-a3a0f6d0a186
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c4ead7cf96ada6d6055bc676ecf4610f2cf4c8f1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62446658"
---
# <a name="interoperability-of-sql-statements"></a>SQL 陳述式的互通性
應用程式的其餘部分，例如 SQL 陳述式可以互通或 DBMS 專屬。 和應用程式的其餘部分，例如選擇的方式可互通的 SQL 陳述式必須為應用程式類型而定。 自訂的應用程式是較不容易使用互通的 SQL 陳述式，因為它們通常設計來利用一或兩個可能的 Dbms 的功能。 泛型應用程式會使用可互通的 SQL 陳述式，因為它們設計來處理各種不同的 Dbms。 和垂直應用程式通常落在位置之間，需要某種程度的功能，但其他方式使用互通的 SQL 陳述式。  
  
 此章節包含下列主題。  
  
-   [選擇 SQL 文法](../../../odbc/reference/develop-app/choosing-an-sql-grammar.md)  
  
-   [建構可互通的 SQL 陳述式](../../../odbc/reference/develop-app/constructing-interoperable-sql-statements.md)
