---
title: "getProcedures 方法 (SQLServerDatabaseMetaData) |Microsoft 文件"
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
- SQLServerDatabaseMetaData.getProcedures
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 66c9a8b0-dc4c-4cbb-8004-c7157368cab4
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3b1fb6671ac6f223b4e3dcc620f5f7144432abe8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getprocedures-method-sqlserverdatabasemetadata"></a>getProcedures 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取可依給定目錄、結構描述或預存程序名稱模式取得之預存程序的描述。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.ResultSet getProcedures(java.lang.String sCatalog,  
                                        java.lang.String sSchema,  
                                        java.lang.String proc)  
```  
  
#### <a name="parameters"></a>參數  
 *sCatalog*  
  
 A**字串**，其中包含目錄名稱。 提供 null 給這個參數，將指出不需要使用目錄名稱。  
  
 *s*  
  
 A**字串**，包含結構描述名稱模式。 提供 null 給這個參數，將指出不需要使用結構描述名稱。  
  
 *程序*  
  
 A**字串**，包含程序名稱模式。  
  
## <a name="return-value"></a>傳回值  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getProcedures 方法是由 java.sql.DatabaseMetaData 介面中 getProcedures 方法指定。  
  
 由 getProcedures 方法傳回的結果集將包含下列資訊：  
  
|名稱|型別|Description|  
|----------|----------|-----------------|  
|PROCEDURE_CAT|**字串**|指定之預存程序所在之資料庫的名稱。|  
|PROCEDURE_SCHEM|**字串**|預存程序的結構描述。|  
|PROCEDURE_NAME|**字串**|預存程序的名稱。|  
|NUM_INPUT_PARAMS|**int**|保留供日後使用，目前會傳回值 -1。|  
|NUM_OUTPUT_PARAMS|**int**|保留供日後使用，目前會傳回值 -1。|  
|NUM_RESULT_SETS|**int**|保留供日後使用，目前會傳回值 -1。|  
|REMARKS|**字串**|程序資料行的描述。<br /><br /> <br /><br /> **注意：** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]不會傳回此資料行的值。|  
|PROCEDURE_TYPE|**smallint**|預存程序的類型。 它可能是下列其中一個值：<br /><br /> SQL_PT_UNKNOWN (0)<br /><br /> SQL_PT_PROCEDURE (1)<br /><br /> SQL_PT_FUNCTION (2)|  
  
> [!NOTE]  
>  多個由 getProcedures 方法傳回之資料的詳細資訊，請參閱 < sp_stored_procedures (TRANSACT-SQL) 」，在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]線上叢書 》。  
  
## <a name="example"></a>範例  
 下列範例示範如何使用 getProcedures 方法傳回的資訊中的 uspGetBillOfMaterials 預存程序[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]範例資料庫。  
  
```  
public static void executeGetProcedures(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getProcedures(null, null, "uspGetBillOfMaterials");  
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
  
  

