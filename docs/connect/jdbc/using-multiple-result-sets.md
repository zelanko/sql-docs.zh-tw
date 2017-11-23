---
title: "使用多個結果集 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ab6a3cfa-073b-44e9-afca-a8675cfe5fd1
caps.latest.revision: "33"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e76f30f5c6b7eb16351749086173bdceaa49f938
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="using-multiple-result-sets"></a>使用多個結果集
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  當使用內嵌 SQL 或[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]預存程序傳回一個以上的結果集，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]提供[getResultSet](../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md)方法中的[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)類別擷取每個傳回的資料集。 此外，當執行陳述式傳回多個結果集時，您可以使用[執行](../../connect/jdbc/reference/execute-method-sqlserverstatement.md)方法 SQLServerStatement 類別，因為它會傳回**布林**值，指出如果傳回值是結果集還是更新計數。  
  
 如果 execute 方法傳回**true**，已執行的陳述式傳回一個或多個結果集。 您可以存取第一個結果集藉由呼叫 getResultSet 方法。 若要判斷使用多個結果集時，您可以呼叫[getMoreResults](../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)方法，這個方法會傳回**布林**值**true**如果有多個結果集可用。 如果使用多個結果集，您可以呼叫 getResultSet 方法進行存取，繼續處理序，直到處理完所有結果集。 如果 getMoreResults 方法傳回**false**，沒有任何多個結果集要處理。  
  
 如果 execute 方法傳回**false**，已執行的陳述式傳回更新計數值，您可以藉由呼叫擷取[getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md)方法。  
  
> [!NOTE]  
>  如需有關更新計數的詳細資訊，請參閱[使用更新計數的預存程序](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md)。  
  
 在下列範例中，開啟連接[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]範例資料庫會傳遞至函式，並會建構 SQL 陳述式執行時，會傳回兩個結果集：  
  
 [!code[JDBC#UsingMultipleResultSets1](../../connect/jdbc/codesnippet/Java/using-multiple-result-sets_1.java)]  
  
 在此例中，已知傳回的結果集數量為二。 不過，即使傳回未知數量的結果集 (例如呼叫預存程序時)，此程式碼的撰寫方式仍可處理所有的結果集。 若要查看呼叫會傳回多個結果集與更新值的預存程序的範例，請參閱[處理複雜陳述式](../../connect/jdbc/handling-complex-statements.md)。  
  
> [!NOTE]  
>  當您呼叫 getMoreResults 方法 SQLServerStatement 類別，會隱含地關閉先前傳回的結果集。  
  
## <a name="see-also"></a>請參閱＜  
 [搭配使用陳述式與 JDBC Driver](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
