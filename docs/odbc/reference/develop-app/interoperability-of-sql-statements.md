---
title: SQL 陳述式的互通性 |Microsoft 文件
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
- interoperability of SQL statements [ODBC]
- interoperability of SQL statements [ODBC], about interoperability
ms.assetid: 3b24c499-829c-4e65-90cf-a3a0f6d0a186
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 205fd667e8891ba0bab0283c1d112af9d608423b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="interoperability-of-sql-statements"></a>SQL 陳述式的互通性
應用程式的其餘部分，如同互通或 DBMS 專屬，可以是 SQL 陳述式。 和應用程式的其餘部分，例如選擇的方式可互通的 SQL 陳述式必須為應用程式類型而定。 自訂應用程式不太可能使用互通的 SQL 陳述式，因為它們通常設計為利用一個或兩個可能的 Dbms 功能。 泛型應用程式使用互通的 SQL 陳述式，因為它們設計來搭配各種不同的 Dbms。 和垂直應用程式通常落在某處之間，要求特定層級的功能，但其他方式使用互通的 SQL 陳述式。  
  
 此章節包含下列主題。  
  
-   [選擇 SQL 文法](../../../odbc/reference/develop-app/choosing-an-sql-grammar.md)  
  
-   [建構可互通的 SQL 陳述式](../../../odbc/reference/develop-app/constructing-interoperable-sql-statements.md)
