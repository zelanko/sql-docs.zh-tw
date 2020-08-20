---
description: SQL 陳述式的互通性
title: SQL 語句的互通性 |Microsoft Docs
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
ms.openlocfilehash: 64127e97adf08c3de9f391810a259a3b7045bdc1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476620"
---
# <a name="interoperability-of-sql-statements"></a>SQL 陳述式的互通性
和應用程式的其餘部分一樣，SQL 語句可以是互通或 DBMS 特定的。 和應用程式的其餘部分一樣，選擇可互通的 SQL 語句如何取決於應用程式的類型。 自訂應用程式比較不可能使用可互通的 SQL 語句，因為它們通常是設計來利用一或多個 Dbms 的功能。 泛型應用程式使用可互通的 SQL 語句，因為它們是設計用來搭配各種 Dbms。 和垂直的應用程式通常會落在其間的某個位置，要求特定層級的功能，但使用可互通的 SQL 語句。  
  
 此章節包含下列主題。  
  
-   [選擇 SQL 文法](../../../odbc/reference/develop-app/choosing-an-sql-grammar.md)  
  
-   [建構可互通的 SQL 陳述式](../../../odbc/reference/develop-app/constructing-interoperable-sql-statements.md)
