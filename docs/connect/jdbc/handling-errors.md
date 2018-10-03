---
title: 處理錯誤 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8fd5b5ef-d939-4b78-b900-5b7b6ddb3eb9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 066aa64a529d2066c0dcce50cd2f2aff12dcf948
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47758986"
---
# <a name="handling-errors"></a>處理錯誤
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 時，所有資料庫錯誤狀況都會使用 [SQLServerException](../../connect/jdbc/reference/sqlserverexception-class.md) 類別，當作例外狀況傳回至 Java 應用程式。 SQLServerException 類別的下列方法是繼承自 java.sql.SQLException 和 java.lang.Throwable；它們可以用來傳回有關所發生 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤的特定資訊：  
  
-   getSQLState 傳回例外狀況的標準 X/Open 或 SQL99 狀態碼。  
  
-   getErrorCode 傳回特定的資料庫錯誤號碼。  
  
-   getMessage 傳回例外狀況的全文。 錯誤訊息文字會描述問題，而且通常包括顯示錯誤訊息時會插入其中的資訊之預留位置，例如物件名稱。  
  
-   如果不有任何其他的例外狀況物件来傳回，getNextException 便會傳回下一個 SQLServerException 物件或 null。  
  
 在下列範例中，連至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 範例資料庫的開啟連線會傳入函式，並會建構一個格式錯誤的 SQL 陳述式，它不含 FROM 子句。 然後，會執行此陳述式，並處理 SQL 例外狀況。  
  
 [!code[JDBC#HandlingErrors1](../../connect/jdbc/codesnippet/Java/handling-errors_1.java)]  
  
## <a name="see-also"></a>另請參閱  
 [診斷 JDBC Driver 問題](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
