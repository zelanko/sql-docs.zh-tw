---
title: "getPrimaryKeys 方法 (SQLServerDatabaseMetaData) |Microsoft 文件"
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
- SQLServerDatabaseMetaData.getPrimaryKeys
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ebfe236a-dc02-493e-a3ab-5353d3769e36
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eea9de761a2c7efb4b47c4032ae3f6ac6814cdc0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getprimarykeys-method-sqlserverdatabasemetadata"></a>getPrimaryKeys 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取給定資料表中的主索引鍵資料行的描述。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.ResultSet getPrimaryKeys(java.lang.String cat,  
                                         java.lang.String schema,  
                                         java.lang.String table)  
```  
  
#### <a name="parameters"></a>參數  
 *cat*  
  
 A**字串**，其中包含目錄名稱。  
  
 *結構描述*  
  
 A**字串**，其中包含結構描述名稱。  
  
 *table*  
  
 A**字串**，其中包含資料表名稱。  
  
## <a name="return-value"></a>傳回值  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getPrimaryKeys 方法是由 java.sql.DatabaseMetaData 介面中 getPrimaryKeys 方法指定。  
  
 GetPrimaryKeys 方法所傳回的結果集將包含下列資訊：  
  
|名稱|型別|Description|  
|----------|----------|-----------------|  
|TABLE_CAT|字串|指定之資料表所在的資料庫名稱。|  
|TABLE_SCHEM|字串|資料表的結構描述。|  
|TABLE_NAME|字串|資料表的名稱。|  
|COLUMN_NAME|字串|資料行的名稱。|  
|KEY_SEQ|short|資料行在多重資料行主索引鍵中的序號。|  
|PK_NAME|字串|主索引鍵的名稱。|  
  
> [!NOTE]  
>  多個 getPrimaryKeys 方法所傳回的資料的詳細資訊，請參閱 「 sp_pkeys (TRANSACT-SQL) 」，在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]線上叢書 》。  
  
## <a name="example"></a>範例  
 下列範例示範如何傳回有關的 Person.Contact 資料表中的主索引鍵使用 getPrimaryKeys 方法[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]範例資料庫。  
  
```  
public static void executeGetPrimaryKeys(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getPrimaryKeys("AdventureWorks", "Person", "Contact");  
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
  
  
