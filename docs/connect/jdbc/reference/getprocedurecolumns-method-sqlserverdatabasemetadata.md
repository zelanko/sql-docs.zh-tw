---
title: getProcedureColumns 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getProcedureColumns
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4f0df8fe-3cd6-46e4-ae3c-dc23c35676b2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c239a16728538acece726c1d0b4722d9c2977765
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47734696"
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
  
 包含目錄名稱的 **String**。 提供 null 給這個參數，將指出不需要使用目錄名稱。  
  
 *s*  
  
 包含結構描述名稱模式的 **String**。 提供 null 給這個參數，將指出不需要使用結構描述名稱。  
  
 *proc*  
  
 包含程序名稱模式的**字串**。  
  
 *col*  
  
 包含資料表名稱模式的 **String**。 提供 null 給這個參數，將針對每個資料行傳回資料列。  
  
## <a name="return-value"></a>傳回值  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getProcedureColumns 方法是由 java.sql.DatabaseMetaData 介面中 getProcedureColumns 方法指定。  
  
 透過 getProcedureColumns 方法所傳回的結果集將包含下列資訊：  
  
|[屬性]|類型|Description|  
|----------|----------|-----------------|  
|PROCEDURE_CAT|**String**|指定之預存程序所在之資料庫的名稱。|  
|PROCEDURE_SCHEM|**String**|預存程序的結構描述。|  
|PROCEDURE_NAME|**String**|預存程序的名稱。|  
|COLUMN_NAME|**String**|資料行的名稱。|  
|COLUMN_TYPE|**short**|資料行的類型。 它可能是下列其中一個值：<br /><br /> procedureColumnUnknown (0)<br /><br /> procedureColumnIn (1)<br /><br /> procedureColumnInOut (2)<br /><br /> procedureColumnOut (4)<br /><br /> procedureColumnReturn (5)<br /><br /> procedureColumnResult (3)|  
|DATA_TYPE|**smallint**|來自 java.sql.Types 的 SQL 資料型別。|  
|TYPE_NAME|**String**|資料類型的名稱。|  
|PRECISION|**int**|有效位數的總數。|  
|LENGTH|**int**|資料長度 (以位元組為單位)。|  
|SCALE|**short**|小數點右側的位數。|  
|RADIX|**short**|數值類型的基底。|  
|NULLABLE|**short**|指出資料行是否能包含 null 值。 它可能是下列其中一個值：<br /><br /> procedureNoNulls (0)<br /><br /> procedureNullable (1)<br /><br /> procedureNullableUnknown (2)|  
|REMARKS|**String**|程序資料行的描述。<br /><br /> <br /><br /> **注意：**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不會傳回這個資料行的值。|  
|COLUMN_DEF|**String**|資料行的預設值。|  
|SQL_DATA_TYPE|**smallint**|除了 **datetime** 和 **ISO interval** 資料類型，這個資料行與 **DATA_TYPE** 資料行相同。|  
|SQL_DATETIME_SUB|**smallint**|**datetime** ISO **interval** 子代碼 (如果 **SQL_DATA_TYPE** 的值是 **SQL_DATETIME** 或 **SQL_INTERVAL**)。 資料類型以外**datetime**和 ISO**間隔**，此資料行是 NULL。|  
|CHAR_OCTET_LENGTH|**int**|資料行中的最大位元組數。|  
|ORDINAL_POSITION|**int**|資料表內資料行的索引。|  
|IS_NULLABLE|**String**|指出資料行是否允許為 Null 值。|  
|SS_TYPE_CATALOG_NAME|**String**|包含使用者定義型別 (UDT) 的目錄名稱。|  
|SS_TYPE_SCHEMA_NAME|**String**|包含使用者定義型別 (UDT) 的結構描述名稱。|  
|SS_UDT_CATALOG_NAME|**String**|完整名稱的使用者定義型別 (UDT)。|  
|SS_UDT_SCHEMA_NAME|**String**|定義 XML 結構描述集合名稱所在目錄的名稱。 如果找不到目錄名稱，則此變數包含空字串。|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**String**|定義 XML 結構描述集合名稱所在結構描述的名稱。 如果找不到結構描述名稱，這就是空字串。|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**String**|XML 結構描述集合的名稱。 如果找不到該名稱，這就是空字串。|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**String**|包含使用者定義型別 (UDT) 的目錄名稱。|  
|SS_XML_SCHEMACOLLECTION_NAME|**String**|包含使用者定義型別 (UDT) 的結構描述名稱。|  
|SS_DATA_TYPE|**tinyint**|擴充預存程序所使用的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。<br /><br /> <br /><br /> **注意：** 如需 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 傳回之資料類型的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 線上叢書》中的＜資料類型 (Transact-SQL)＞。|  
  
> [!NOTE]  
>  如需由 getProcedureColumns 方法所傳回資料的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 線上叢書》中的＜sp_sproc_columns (Transact-SQL)＞。  
  
## <a name="example"></a>範例  
 下列範例會示範如何使用 getProcedureColumns 方法來傳回 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 範例資料庫中 uspGetBillOfMaterials 預存程序的相關資訊。  
  
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
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
