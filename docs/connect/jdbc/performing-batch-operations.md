---
title: 執行批次作業 |Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1a576d95-7da6-4b7b-8b32-59e5b4d354c4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 244c20b2fb7721d117557581068791e1a2d99d14
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67956228"
---
# <a name="performing-batch-operations"></a>執行批次作業
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  在對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫執行多重更新時，為了改善效能，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供以單一工作單位提交多重更新的功能，這也稱為批次。  
  
 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)、[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 和 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 類別都可以用來提交批次更新。 [addBatch](../../connect/jdbc/reference/addbatch-method-sqlserverpreparedstatement.md) 方法用來新增命令。 [clearBatch](../../connect/jdbc/reference/clearbatch-method-sqlserverpreparedstatement.md) 方法用來清除命令清單。 [executeBatch](../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md) 方法用來提交所有命令以供處理。 只有傳回簡單更新計數的資料定義語言 (DDL) 和資料操作語言 (DML) 陳述式可以當作批次的一部份來執行。  
  
 executeBatch 方法會傳回對應到每個命令之更新計數的 **int** 值陣列。 如果其中一個命令失敗, 則會擲回 BatchUpdateException, 而且您應該使用 BatchUpdateException 類別的 getUpdateCounts 方法來取出更新計數陣列。 如果某命令失敗，驅動程式會繼續處理其餘命令。 不過，如果命令有語法錯誤，批次中的陳述式會失敗。  
  
> [!NOTE]  
>  如果不必使用更新計數，可以先對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發出 SET NOCOUNT ON 陳述式。 這將會減少網路流量，而且還會加強應用程式的效能。  
  
 例如，在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 範例資料庫中建立下列資料表：  
  
```sql
CREATE TABLE TestTable   
   (Col1 int IDENTITY,   
    Col2 varchar(50),   
    Col3 int);  
```  
  
 在下列範例中，連至 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 範例資料庫的開啟連線會傳遞至函式、addBatch 方法用來建立要執行的陳述式，並呼叫 executeBatch 方法將批次提交至資料庫。  
  
```java
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
 [搭配使用陳述式與 JDBC Driver](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
