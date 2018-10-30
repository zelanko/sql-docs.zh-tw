---
title: 處理複雜陳述式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6b807a45-a8b5-4b1c-8b7b-d8175c710ce0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d44f2c229755c742d5481f3ca427f11fb5586c2c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47623926"
---
# <a name="handling-complex-statements"></a>處理複雜陳述式
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 時，您可能必須處理複雜陳述式，包括在執行階段動態產生的陳述式。 複雜陳述式通常執行各種不同的工作，包括更新、插入與刪除。 這些類型的陳述式也可能傳回多個結果集和輸出參數。 在這些情況下，執行陳述式的 Java 程式碼事先可能不知道傳回的物件和資料的類型和數目。  
  
 為了有效處理複雜陳述式，JDBC 驅動程式提供一些方法來查詢傳回的物件和資料，使應用程式可以正確處理它們。 處理複雜陳述式的關鍵在於 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 類別的 [execute](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 方法。 這個方法會傳回**布林**值。 若此值為 true，則從陳述式傳回的第一個結果是結果集。 當此值為 false，則傳回的第一個結果是更新計數。  
  
 當您知道所傳回物件或資料的類型時，可使用 [getResultSet](../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md) 或 [getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md) 方法來處理該資料。 若要處理從複雜陳述式傳回的下一個物件或資料，您可以呼叫 [getMoreResults](../../connect/jdbc/reference/getmoreresults-method.md) 方法。  
  
 在下列範例中，連至 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 範例資料庫的開啟連接會傳遞至函式中，建構一個結合預存程序呼叫與 SQL 陳述式的複雜陳述式，接著執行陳述式，然後使用 `do` 迴圈來處理傳回的所有結果集和更新計數。  
  
 [!code[JDBC#HandlingComplexStatements1](../../connect/jdbc/codesnippet/Java/handling-complex-statements_1.java)]  
  
## <a name="see-also"></a>另請參閱  
 [搭配使用陳述式與 JDBC Driver](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
