---
title: "使用 SQL 陳述式搭配參數 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3202b88f-ce13-44dd-982c-c6a3b0260378
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8475ea4917ffcc0d9226933b29e81b99f89345c2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="using-an-sql-statement-with-parameters"></a>搭配參數使用 SQL 陳述式
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  若要使用中的資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫使用 SQL 陳述式包含 IN 參數，您可以使用[executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md)方法[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)類別，以傳回[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) ，就會包含所要求的資料。 若要這樣做，您必須先建立 SQLServerPreparedStatement 物件，使用[prepareStatement](../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md)方法[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)類別。  
  
 當建構 SQL 陳述式時，請使用 ? (問號) 字元來指定 IN 參數，這個問號是作為預留位置，代表稍後將傳遞至 SQL 陳述式的參數值。 若要指定參數的值，您可以使用 SQLServerPreparedStatement 類別的 setter 方法的其中一個。 您使用的 setter 方法，是由要傳遞至 SQL 陳述式的值資料類型所決定。  
  
 當您將值傳遞至 setter 方法時，您不但要指定用於 SQL 陳述式的實際值，也要指定 SQL 陳述式中參數的序數位置。 例如，如果您的 SQL 陳述式包含單一參數，其序數值將會是 1。 如果陳述式包含兩個參數，第一個序數值將會是 1，而第二個序數值將會是 2。  
  
 在下列範例中，開啟連接[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]範例資料庫會傳遞至函式、 建構及執行以單一字串參數值，SQL 準備陳述式，然後會從結果集中讀取結果。  
  
 [!code[JDBC#UsingSQLWithParams1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-w_1_1.java)]  
  
## <a name="see-also"></a>另請參閱  
 [使用 SQL 陳述式](../../connect/jdbc/using-statements-with-sql.md)  
  
  

