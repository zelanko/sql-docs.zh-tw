---
title: "getBestRowIdentifier 方法 (SQLServerDatabaseMetaData) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.getBestRowIdentifier
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c19e9ca6-2a53-4a0c-91ab-80090c3f7229
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 09dee13a9a71b606aa630aac1716d43f6d38a1f2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getbestrowidentifier-method-sqlserverdatabasemetadata"></a>getBestRowIdentifier 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取資料表中最佳資料行集的描述，此資料行集可唯一識別資料列。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.ResultSet getBestRowIdentifier(java.lang.String catalog,  
                                               java.lang.String schema,  
                                               java.lang.String table,  
                                               int scope,  
                                               boolean nullable)  
```  
  
#### <a name="parameters"></a>參數  
 *類別目錄*  
  
 A**字串**，其中包含目錄名稱。  
  
 *結構描述*  
  
 A**字串**，其中包含結構描述名稱。  
  
 *table*  
  
 A**字串**，其中包含資料表名稱。  
  
 *範圍 (scope)*  
  
 **Int** ，指出感興趣的範圍。 可能的值如下：  
  
 bestRowTemporary (0)  
  
 bestRowTransaction (1)  
  
 bestRowSession (2)  
  
 *可為 null*  
  
 **true**包含可為 null 的資料行。 否則為 **false**。  
  
## <a name="return-value"></a>傳回值  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getBestRowIdentifier 方法是由 java.sql.DatabaseMetaData 介面中 getBestRowIdentifier 方法指定。  
  
 GetBestRowIdentifier 方法所傳回的結果集將包含下列資訊：  
  
|名稱|型別|Description|  
|----------|----------|-----------------|  
|SCOPE|short|傳回之結果的範圍。 它可能是下列其中一個值：<br /><br /> bestRowTemporary (0)<br /><br /> bestRowTransaction (1)<br /><br /> bestRowSession (2)|  
|COLUMN_NAME|字串|資料行的名稱。|  
|DATA_TYPE|short|來自 java.sql.Types 的 SQL 資料型別。|  
|TYPE_NAME|字串|資料類型的名稱。|  
|COLUMN_SIZE|int|資料行的有效位數。|  
|BUFFER_LENGTH|int|緩衝區長度。|  
|DECIMAL_DIGITS|short|資料行的小數位數。|  
|PSEUDO_COLUMN|short|指出資料行是否為虛擬資料行。 它可能是下列其中一個值：<br /><br /> bestRowUnknown (0)<br /><br /> bestRowNotPseudo (1)<br /><br /> bestRowPseudo (2)|  
  
## <a name="example"></a>範例  
 下列範例示範如何使用 getBestRowIdentifier 方法傳回的 Person.Contact 資料表中的最佳資料列識別碼的相關資訊[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]範例資料庫。  
  
```  
public static void executeGetBestRowIdentifier(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getBestRowIdentifier(null, "Person", "Contact", 0, true);  
      ResultSetMetaData rsmd = rs.getMetaData();  
  
      // Display the result set data.  
      int cols = rsmd.getColumnCount();  
      while(rs.next()) {  
         for (int i = 1; i <= cols; i++) {  
            System.out.println(rs.getString(i));  
         }  
      }  
      rs.close();  
   }  
  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

