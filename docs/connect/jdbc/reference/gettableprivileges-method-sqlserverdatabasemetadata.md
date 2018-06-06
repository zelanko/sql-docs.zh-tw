---
title: getTablePrivileges 方法 (SQLServerDatabaseMetaData) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getTablePrivileges
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0610d667-a16d-4201-a14b-0a40048911e1
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 06a7bcc60d73aba7e0939d70224a765168738b64
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="gettableprivileges-method-sqlserverdatabasemetadata"></a>getTablePrivileges 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取各個資料表之存取權限的描述，這些資料表會透過給定的目錄、結構描述或資料表名稱模式提供。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.ResultSet getTablePrivileges(java.lang.String catalog,  
                                             java.lang.String schema,  
                                             java.lang.String table)  
```  
  
#### <a name="parameters"></a>參數  
 *catalog*  
  
 A**字串**，其中包含目錄名稱。 提供 null 給這個參數，將指出不需要使用目錄名稱。  
  
 *schema*  
  
 A**字串**，包含結構描述名稱模式。 提供 null 給這個參數，將指出不需要使用結構描述名稱。  
  
 *table*  
  
 A**字串**，包含資料表名稱模式。  
  
## <a name="return-value"></a>傳回值  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getTablePrivileges 方法是由 java.sql.DatabaseMetaData 介面中 getTablePrivileges 方法指定。  
  
 GetTablePrivileges 方法所傳回的結果集將包含下列資訊：  
  
|名稱|型別|Description|  
|----------|----------|-----------------|  
|TABLE_CAT|**字串**|目錄的名稱。|  
|TABLE_SCHEM|**字串**|資料表結構描述名稱。|  
|TABLE_NAME|**字串**|資料表名稱。|  
|GRANTOR|**字串**|授與存取權的物件。|  
|GRANTEE|**字串**|接收存取權的物件。|  
|PRIVILEGE|**字串**|授與的存取類型。|  
|IS_GRANTABLE|**字串**|指出是否允許被授與者授與存取權給其他使用者。|  
  
> [!NOTE]  
>  多個 getTablePrivileges 方法所傳回的資料的詳細資訊，請參閱 「 sp_table_privileges (TRANSACT-SQL) 」，在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]線上叢書 》。  
  
## <a name="example"></a>範例  
 下列範例示範如何使用 getTablePrivileges 方法傳回的 Person.Contact 資料表中的存取權限[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]範例資料庫。  
  
```  
public static void executeGetTablePrivileges(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getTablePrivileges("AdventureWorks", "Person", "Contact");  
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
  
  
