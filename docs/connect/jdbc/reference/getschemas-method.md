---
title: "getSchemas 方法 （) |Microsoft 文件"
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
- SQLServerDatabaseMetaData.getSchemas
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: adba0ee6-ff6d-4215-b646-62c735be3fe9
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6a66767527b1fb7bfe2c3b3f03414ef643676b4e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getschemas-method-"></a>getSchemas 方法 ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取目前資料庫中所提供的結構描述名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.ResultSet getSchemas()  
```  
  
## <a name="return-value"></a>傳回值  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetSchemas 方法 java.sql.DatabaseMetaData 介面中所指定此 getSchemas 方法。  
  
 GetSchemas 方法所傳回的結果集包含下列資訊：  
  
|名稱|型別|Description|  
|----------|----------|-----------------|  
|TABLE_SCHEM|**字串**|結構描述的名稱。|  
|TABLE_CATALOG|**字串**|結構描述的目錄名稱。|  
  
 這些結果會依據 TABLE_CATALOG 排列，接著再依據 TABLE_SCHEM 排列。 每個資料列都是以 TABLE_SCHEM 做為第一個資料列，以 TABLE_CATALOG 做為第二個資料列。  
  
> [!NOTE]  
>  GetSchemas 方法所傳回的資料的詳細資訊，請參閱 < sys.schemas (TRANSACT-SQL) 」 中,[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]線上叢書 》。  
  
## <a name="example"></a>範例  
 下列範例示範如何使用 getSchemas 方法來傳回目錄，並在其相關聯的結構描述名稱的相關資訊[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]當連接引數指定要使用的資料庫。  
  
```  
public static void executeGetSchemas(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getSchemas();  
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
  
  

