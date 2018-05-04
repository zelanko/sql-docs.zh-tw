---
title: 處理複雜陳述式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6b807a45-a8b5-4b1c-8b7b-d8175c710ce0
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8dc009ed538571d5b66a1240adc8b4c41cbab0a6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="handling-complex-statements"></a>處理複雜陳述式
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  當您使用[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，您可能必須處理複雜陳述式，包括在執行階段動態產生的陳述式。 複雜陳述式通常執行各種不同的工作，包括更新、插入與刪除。 這些類型的陳述式也可能傳回多個結果集和輸出參數。 在這些情況下，執行陳述式的 Java 程式碼事先可能不知道傳回的物件和資料的類型和數目。  
  
 為了有效處理複雜陳述式，JDBC 驅動程式提供一些方法來查詢傳回的物件和資料，使應用程式可以正確處理它們。 處理複雜陳述式的關鍵在於[執行](../../connect/jdbc/reference/execute-method-sqlserverstatement.md)方法[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)類別。 這個方法會傳回**布林**值。 若此值為 true，則從陳述式傳回的第一個結果是結果集。 當此值為 false，則傳回的第一個結果是更新計數。  
  
 當您知道的物件或傳回的資料類型時，您可以使用[getResultSet](../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md)或[getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md)方法來處理該資料。 若要繼續進行下一個物件或從複雜陳述式傳回的資料，您可以呼叫[getMoreResults](../../connect/jdbc/reference/getmoreresults-method.md)方法。  
  
 在下列範例中，開啟連接[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]範例資料庫會傳遞至函式、 複雜的陳述式會建構一個結合預存程序呼叫與 SQL 陳述式、 陳述式會執行，然後`do`迴圈用來處理所有結果集和更新的傳回計數。  
  
 [!code[JDBC#HandlingComplexStatements1](../../connect/jdbc/codesnippet/Java/handling-complex-statements_1.java)]  
  
## <a name="see-also"></a>另請參閱  
 [搭配使用陳述式與 JDBC Driver](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
