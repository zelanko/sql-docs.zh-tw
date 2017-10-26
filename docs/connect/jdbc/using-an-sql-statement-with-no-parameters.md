---
title: "使用不含任何參數的 SQL 陳述式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4b0728bd-059b-4b71-895c-999335bc7427
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1e7e97fa030c2efd499aebfa054c0e4827d590dc
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="using-an-sql-statement-with-no-parameters"></a>使用不含參數的 SQL 陳述式
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  若要使用中的資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫使用不含任何參數的 SQL 陳述式，您可以使用[executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md)方法[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)類別，以傳回[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) ，就會包含所要求的資料。 若要這樣做，您必須先建立 SQLServerStatement 物件使用[createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)方法[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)類別。  
  
 在下列範例中，開啟連接[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]範例資料庫會傳遞至函式中建構及執行，SQL 陳述式，然後從結果集讀取結果。  
  
 [!code[JDBC#UsingSQLWithNoParams1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-w_0_1.java)]  
  
 如需有關如何使用結果集的詳細資訊，請參閱[JDBC 驅動程式管理結果集](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用 SQL 陳述式](../../connect/jdbc/using-statements-with-sql.md)  
  
  

