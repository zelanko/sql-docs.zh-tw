---
title: "getTables 方法 (SQLServerDatabaseMetaData) |Microsoft 文件"
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
- SQLServerDatabaseMetaData.getTables
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a7514673-3457-4541-9560-28a8284ad9e3
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9bbf35aeec7b5626b380fc654995d181fe124811
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="gettables-method-sqlserverdatabasemetadata"></a>getTables 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取可依給定目錄、結構描述或資料表名稱模式取得之資料表的描述。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.ResultSet getTables(java.lang.String catalog,  
                                    java.lang.String schema,  
                                    java.lang.String table,  
                                    java.lang.String[] types)  
```  
  
#### <a name="parameters"></a>參數  
 *類別目錄*  
  
 A**字串**，其中包含目錄名稱。 提供 null 給這個參數，將指出不需要使用目錄名稱。  
  
 *結構描述*  
  
 A**字串**，包含結構描述名稱模式。 提供 null 給這個參數，將指出不需要使用結構描述名稱。  
  
 *tableName*  
  
 A**字串**，包含資料表名稱模式。  
  
 *型別*  
  
 字串的陣列，包含要納入的資料表類型。 Null 表示應該納入所有資料表類型。  
  
## <a name="return-value"></a>傳回值  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getTables 方法是由 java.sql.DatabaseMetaData 介面中 getTables 方法指定。  
  
 由 getTables 方法傳回的結果集將包含下列資訊：  
  
|名稱|型別|Description|  
|----------|----------|-----------------|  
|TABLE_CAT|**字串**|指定之資料表所在的資料庫名稱。|  
|TABLE_SCHEM|**字串**|資料表結構描述名稱。|  
|TABLE_NAME|**字串**|資料表名稱。|  
|TABLE_TYPE|**字串**|資料表類型。|  
|REMARKS|**字串**|資料表的描述。<br /><br /> **注意：** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]不會傳回此資料行的值。  |  
|TYPE_CAT|**字串**|JDBC 驅動程式不支援。|  
|TYPE_SCHEM|**字串**|JDBC 驅動程式不支援。|  
|TYPE_NAME|**字串**|JDBC 驅動程式不支援。|  
|SELF_REFERENCING_COL_NAME|**字串**|JDBC 驅動程式不支援。|  
|REF_GENERATION|**字串**|JDBC 驅動程式不支援。|  
  
> [!NOTE]  
>  多個由 getTables 方法傳回之資料的詳細資訊，請參閱"sp_tables (TRANSACT-SQL) 」，在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]線上叢書 》。  
  
## <a name="example"></a>範例  
 下列範例示範如何使用 getTables 方法傳回的 Person.Contact 資料表中的資料表描述資訊[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]範例資料庫。  
  
```  
public static void executeGetTables(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getTables("AdventureWorks", "Person", "Contact", null);  
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
  
  

