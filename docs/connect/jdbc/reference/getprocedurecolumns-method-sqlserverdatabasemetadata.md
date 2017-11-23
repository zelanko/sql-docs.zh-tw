---
title: "getProcedureColumns 方法 (SQLServerDatabaseMetaData) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerDatabaseMetaData.getProcedureColumns
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 4f0df8fe-3cd6-46e4-ae3c-dc23c35676b2
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2d8fa1fbb84392dba636c8aa5649f45cd54e397d
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="getprocedurecolumns-method-sqlserverdatabasemetadata"></a>getProcedureColumns 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取預存程序參數和結果資料行的描述。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.ResultSet getProcedureColumns(java.lang.String sCatalog,  
                                              java.lang.String sSchema,  
                                              java.lang.String proc,  
                                              java.lang.String col)  
```  
  
#### <a name="parameters"></a>參數  
 *sCatalog*  
  
 A**字串**，其中包含目錄名稱。 提供 null 給這個參數，將指出不需要使用目錄名稱。  
  
 *s*  
  
 A**字串**，包含結構描述名稱模式。 提供 null 給這個參數，將指出不需要使用結構描述名稱。  
  
 *程序*  
  
 A**字串**，包含程序名稱模式。  
  
 *資料行*  
  
 A**字串**，其中包含資料行名稱模式。 提供 null 給這個參數，將針對每個資料行傳回資料列。  
  
## <a name="return-value"></a>傳回值  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getProcedureColumns 方法是由 java.sql.DatabaseMetaData 介面中 getProcedureColumns 方法指定。  
  
 GetProcedureColumns 方法所傳回的結果集將包含下列資訊：  
  
|名稱|型別|Description|  
|----------|----------|-----------------|  
|PROCEDURE_CAT|**字串**|指定之預存程序所在之資料庫的名稱。|  
|PROCEDURE_SCHEM|**字串**|預存程序的結構描述。|  
|PROCEDURE_NAME|**字串**|預存程序的名稱。|  
|COLUMN_NAME|**字串**|資料行的名稱。|  
|COLUMN_TYPE|**短**|資料行的類型。 它可能是下列其中一個值：<br /><br /> procedureColumnUnknown (0)<br /><br /> procedureColumnIn (1)<br /><br /> procedureColumnInOut (2)<br /><br /> procedureColumnOut (4)<br /><br /> procedureColumnReturn (5)<br /><br /> procedureColumnResult (3)|  
|DATA_TYPE|**smallint**|來自 java.sql.Types 的 SQL 資料型別。|  
|TYPE_NAME|**字串**|資料類型的名稱。|  
|PRECISION|**int**|有效位數的總數。|  
|LENGTH|**int**|資料長度 (以位元組為單位)。|  
|SCALE|**短**|小數點右側的位數。|  
|RADIX|**短**|數值類型的基底。|  
|NULLABLE|**短**|指出資料行是否能包含 null 值。 它可能是下列其中一個值：<br /><br /> procedureNoNulls (0)<br /><br /> procedureNullable (1)<br /><br /> procedureNullableUnknown (2)|  
|REMARKS|**字串**|程序資料行的描述。<br /><br /> <br /><br /> **注意：** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]不會傳回此資料行的值。|  
|COLUMN_DEF|**字串**|資料行的預設值。|  
|SQL_DATA_TYPE|**smallint**|此資料行等同於**DATA_TYPE**資料行，除了**datetime**和 ISO**間隔**資料型別。|  
|SQL_DATETIME_SUB|**smallint**|**Datetime** ISO**間隔**子代碼，如果值**SQL_DATA_TYPE**是**SQL_DATETIME**或**SQL_INTERVAL**. 資料類型以外**datetime**和 ISO**間隔**，此資料行為 unll。|  
|CHAR_OCTET_LENGTH|**int**|資料行中的最大位元組數。|  
|ORDINAL_POSITION|**int**|資料表內資料行的索引。|  
|IS_NULLABLE|**字串**|指出資料行是否允許為 Null 值。|  
|SS_TYPE_CATALOG_NAME|**字串**|包含使用者定義型別 (UDT) 的目錄名稱。|  
|SS_TYPE_SCHEMA_NAME|**字串**|包含使用者定義型別 (UDT) 的結構描述名稱。|  
|SS_UDT_CATALOG_NAME|**字串**|完整名稱的使用者定義型別 (UDT)。|  
|SS_UDT_SCHEMA_NAME|**字串**|定義 XML 結構描述集合名稱所在目錄的名稱。 如果找不到目錄名稱，則此變數包含空字串。|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**字串**|定義 XML 結構描述集合名稱所在結構描述的名稱。 如果找不到結構描述名稱，這就是空字串。|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**字串**|XML 結構描述集合的名稱。 如果找不到該名稱，這就是空字串。|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**字串**|包含使用者定義型別 (UDT) 的目錄名稱。|  
|SS_XML_SCHEMACOLLECTION_NAME|**字串**|包含使用者定義型別 (UDT) 的結構描述名稱。|  
|SS_DATA_TYPE|**tinyint**|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料型別，由擴充預存程序。<br /><br /> <br /><br /> **注意：**如需有關所傳回的資料型別[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]，請參閱中的 < 資料類型 (TRANSACT-SQL) >[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]線上叢書 》。|  
  
> [!NOTE]  
>  GetProcedureColumns 方法所傳回之資料的相關詳細資訊，請參閱 < sp_sproc_columns (TRANSACT-SQL) 」 中,[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]線上叢書 》。  
  
## <a name="example"></a>範例  
 下列範例示範如何使用 getProcedureColumns 方法來傳回中的 uspGetBillOfMaterials 預存程序的相關資訊[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]範例資料庫。  
  
```  
public static void executeGetProcedureColumns(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getProcedureColumns(null, null, "uspGetBillOfMaterials", null);  
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
  
## <a name="see-also"></a>請參閱＜  
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
