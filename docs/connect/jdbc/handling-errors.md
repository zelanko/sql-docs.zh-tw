---
title: 錯誤處理 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8fd5b5ef-d939-4b78-b900-5b7b6ddb3eb9
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7ac872fa0c59b285de97494874099e6235a8332d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="handling-errors"></a>處理錯誤
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  當使用[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，所有資料庫錯誤狀況都會都傳回至 Java 應用程式使用當做例外狀況[SQLServerException](../../connect/jdbc/reference/sqlserverexception-class.md)類別。 SQLServerException 類別的下列方法被繼承自 java.sql.SQLException 和 java.lang.Throwable;它們可以用來傳回相關特定資訊和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]已發生的錯誤：  
  
-   getSQLState 傳回的標準 X / Open 或 SQL99 狀態碼的例外狀況。  
  
-   getErrorCode 傳回特定的資料庫錯誤號碼。  
  
-   getMessage 傳回例外狀況的完整文字。 錯誤訊息文字會描述問題，而且通常包括顯示錯誤訊息時會插入其中的資訊之預留位置，例如物件名稱。  
  
-   如果沒有其他例外狀況物件来傳回，getNextException 傳回的下一個 SQLServerException 物件或為 null。  
  
 在下列範例中，開啟連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)][!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]範例資料庫會傳遞至函式和格式不正確的 SQL 陳述式會建構不含 FROM 子句。 然後，會執行此陳述式，並處理 SQL 例外狀況。  
  
 [!code[JDBC#HandlingErrors1](../../connect/jdbc/codesnippet/Java/handling-errors_1.java)]  
  
## <a name="see-also"></a>另請參閱  
 [診斷 JDBC Driver 問題](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
