---
title: SQL 語句的互操作性 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d3d7a76c67096d2e76fe1cd3d4b15f73122699e7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302799"
---
# <a name="interoperability-of-sql-statements"></a>SQL 陳述式的互通性
與應用程式的其餘部分一樣,SQL 語句可以互通或特定於 DBMS。 與應用程式的其餘部分一樣,選擇可互通的 SQL 語句取決於應用程式的類型。 自定義應用程式不太可能使用可互通的 SQL 語句,因為它們通常旨在利用一個或兩個 DBMS 的功能。 通用應用程式使用可互通的 SQL 語句,因為它們旨在處理各種 DBMS。 垂直應用程式通常介於兩者之間,需要一定的功能級別,但使用可互操作的 SQL 語句。  
  
 此章節包含下列主題。  
  
-   [選擇 SQL 文法](../../../odbc/reference/develop-app/choosing-an-sql-grammar.md)  
  
-   [建構可互通的 SQL 陳述式](../../../odbc/reference/develop-app/constructing-interoperable-sql-statements.md)
