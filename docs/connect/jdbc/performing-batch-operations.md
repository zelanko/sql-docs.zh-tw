---
title: "執行批次作業 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1a576d95-7da6-4b7b-8b32-59e5b4d354c4
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 01a355319eb7c65bd87e25137e013b14406048c4
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="performing-batch-operations"></a>執行批次作業
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  若要改善效能，多重更新時[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫進行[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]可讓您以單一單位的工作，也稱為批次提交多重更新。  
  
 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)， [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)，和[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)類別所有用來提交批次更新。 [AddBatch](../../connect/jdbc/reference/addbatch-method-sqlserverpreparedstatement.md)方法用來加入命令。 [ClearBatch](../../connect/jdbc/reference/clearbatch-method-sqlserverpreparedstatement.md)方法用來清除命令清單。 [ExecuteBatch](../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md)方法用來提交所有命令以供處理。 只有傳回簡單更新計數的資料定義語言 (DDL) 和資料操作語言 (DML) 陳述式可以當作批次的一部份來執行。  
  
 ExecuteBatch 方法傳回的陣列**int**對應到每個命令之更新計數的值。 如果其中一個命令失敗，BatchUpdateException 擲回，且您必須使用 BatchUpdateException 類別 getUpdateCounts 方法來擷取更新計數陣列。 如果某命令失敗，驅動程式會繼續處理其餘命令。 不過，如果命令有語法錯誤，批次中的陳述式會失敗。  
  
> [!NOTE]  
>  如果您不需要使用更新計數，您可以先對發出 SET NOCOUNT ON 陳述式，以[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 這將會減少網路流量，而且還會加強應用程式的效能。  
  
 例如，建立下的表中[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]範例資料庫：  
  
```  
CREATE TABLE TestTable   
   (Col1 int IDENTITY,   
    Col2 varchar(50),   
    Col3 int);  
```  
  
 在下列範例中，開啟連接[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]範例資料庫會傳遞至函式、 addBatch 方法用來建立可執行的陳述式和 executeBatch 方法呼叫提交至資料庫的批次。  
  
```  
public static void executeBatchUpdate(Connection con) {  
   try {  
      Statement stmt = con.createStatement();  
      stmt.addBatch("INSERT INTO TestTable (Col2, Col3) VALUES ('X', 100)");  
      stmt.addBatch("INSERT INTO TestTable (Col2, Col3) VALUES ('Y', 200)");  
      stmt.addBatch("INSERT INTO TestTable (Col2, Col3) VALUES ('Z', 300)");  
      int[] updateCounts = stmt.executeBatch();  
      stmt.close();  
   }  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [JDBC 驅動程式搭配使用陳述式](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
