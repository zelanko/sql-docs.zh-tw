---
title: getTables 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getTables
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a7514673-3457-4541-9560-28a8284ad9e3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e8dfd7f14d6006f5a41a7cd2a9b0cae4933804fe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67979208"
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
 *catalog*  
  
 包含目錄名稱的 **String**。 提供 null 給這個參數，將指出不需要使用目錄名稱。  
  
 *schema*  
  
 包含結構描述名稱模式的 **String**。 提供 null 給這個參數，將指出不需要使用結構描述名稱。  
  
 *tableName*  
  
 包含資料表名稱模式的**字串**。  
  
 *types*  
  
 字串的陣列，包含要納入的資料表類型。 Null 表示應該納入所有資料表類型。  
  
## <a name="return-value"></a>傳回值  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getTables 方法是由 java.sql.DatabaseMetaData 介面中的 getTables 方法指定。  
  
 透過 getTables 方法所傳回的結果將包含下列資訊：  
  
|[屬性]|類型|Description|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|指定之資料表所在的資料庫名稱。|  
|TABLE_SCHEM|**String**|資料表結構描述名稱。|  
|TABLE_NAME|**String**|資料表名稱。|  
|TABLE_TYPE|**String**|資料表類型。|  
|REMARKS|**String**|資料表的描述。<br /><br /> **注意：** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不會傳回這個資料行的值。|  
|TYPE_CAT|**String**|JDBC 驅動程式不支援。|  
|TYPE_SCHEM|**String**|JDBC 驅動程式不支援。|  
|TYPE_NAME|**String**|JDBC 驅動程式不支援。|  
|SELF_REFERENCING_COL_NAME|**String**|JDBC 驅動程式不支援。|  
|REF_GENERATION|**String**|JDBC 驅動程式不支援。|  
  
> [!NOTE]  
>  如需 getTables 方法所傳回資料的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 線上叢書》中的＜sp_tables (Transact-SQL)＞。  
  
## <a name="example"></a>範例  
 下列範例示範如何使用 getTables 方法來傳回 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 範例資料庫中 Person.Contact 資料表的資料表描述資訊。  
  
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
  
  
