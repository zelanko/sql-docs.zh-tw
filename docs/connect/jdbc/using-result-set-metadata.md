---
title: "使用結果集的中繼資料 |Microsoft 文件"
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
ms.assetid: 5e37529a-30db-48c8-b90a-ae9657d0f6b0
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 98d595320ae164690712f1a5541ec304488e0ca0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="using-result-set-metadata"></a>使用結果集中繼資料
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  若要查詢的結果集有關它所包含的資料行[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]實作[SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)類別。 此類別包含數種以單一值形式傳回資訊的方法。  
  
 若要建立 SQLServerResultSetMetaData 物件時，您可以使用[getMetaData](../../connect/jdbc/reference/getmetadata-method-sqlserverresultset.md)方法[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)類別。  
  
 在下列範例中，開啟連接[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]範例資料庫會傳遞至函式、 SQLServerResultSet 類別的 getMetaData 方法用來傳回一個 SQLServerResultSetMetaData 物件，然後的各種方法SQLServerResultSetMetaData 物件可用來顯示結果集內包含資料行的名稱和資料類型的相關資訊。  
  
 [!code[JDBC#UsingResultSetMetaData1](../../connect/jdbc/codesnippet/Java/using-result-set-metadata_1.java)]  
  
## <a name="see-also"></a>另請參閱  
 [JDBC driver 處理中繼資料](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)  
  
  

