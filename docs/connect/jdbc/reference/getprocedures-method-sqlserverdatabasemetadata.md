---
title: getProcedures 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getProcedures
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 66c9a8b0-dc4c-4cbb-8004-c7157368cab4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 054ce4f6f646f873d4aff05fbe1d31aa9903ded9
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67980746"
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
  
 包含目錄名稱的 **String**。 提供 null 給這個參數，將指出不需要使用目錄名稱。  
  
 *sSchema*  
  
 包含結構描述名稱模式的 **String**。 提供 null 給這個參數，將指出不需要使用結構描述名稱。  
  
 *proc*  
  
 包含程序名稱模式的**字串**。  
  
## <a name="return-value"></a>傳回值  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getProcedures 方法是由 java.sql.DatabaseMetaData 介面中的 getProcedures 方法所指定。  
  
 透過 getProcedures 方法所傳回的結果將包含下列資訊：  
  
|名稱|類型|描述|  
|----------|----------|-----------------|  
|PROCEDURE_CAT|**String**|指定之預存程序所在之資料庫的名稱。|  
|PROCEDURE_SCHEM|**String**|預存程序的結構描述。|  
|PROCEDURE_NAME|**String**|預存程序的名稱。|  
|NUM_INPUT_PARAMS|**int**|保留供日後使用，目前會傳回值 -1。|  
|NUM_OUTPUT_PARAMS|**int**|保留供日後使用，目前會傳回值 -1。|  
|NUM_RESULT_SETS|**int**|保留供日後使用，目前會傳回值 -1。|  
|REMARKS|**String**|程序資料行的描述。<br /><br /> <br /><br /> **注意：** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不會傳回這個資料行的值。|  
|PROCEDURE_TYPE|**smallint**|預存程序的類型。 它可能是下列其中一個值：<br /><br /> SQL_PT_UNKNOWN (0)<br /><br /> SQL_PT_PROCEDURE (1)<br /><br /> SQL_PT_FUNCTION (2)|  
  
> [!NOTE]  
>  如需 getProcedures 方法所傳回資料的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 線上叢書》中的＜sp_stored_procedures (Transact-SQL)＞。  
  
## <a name="example"></a>範例  
 下列範例會示範如何使用 getProcedures 方法來傳回 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 範例資料庫中 uspGetBillOfMaterials 預存程序的相關資訊。  
  
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
  
  
