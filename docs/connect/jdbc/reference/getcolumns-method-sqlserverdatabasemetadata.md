---
title: "getColumns 方法 (SQLServerDatabaseMetaData) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.getColumns
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f173fa5d-e114-4a37-a5c4-2baad9ff3af1
caps.latest.revision: 39
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 75d9ab3fb70f854e56df0c659275a2983a8487ff
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getcolumns-method-sqlserverdatabasemetadata"></a>getColumns 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取可透過指定目錄提供之資料表資料行的描述。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.ResultSet getColumns(java.lang.String catalog,  
                                     java.lang.String schema,  
                                     java.lang.String table,  
                                     java.lang.String col)  
```  
  
#### <a name="parameters"></a>參數  
 *類別目錄*  
  
 A**字串**，其中包含目錄名稱。  
  
 *結構描述*  
  
 A**字串**，包含結構描述名稱模式。  
  
 *table*  
  
 A**字串**，包含資料表名稱模式。  
  
 *資料行*  
  
 A**字串**，其中包含資料行名稱模式。  
  
## <a name="return-value"></a>傳回值  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetColumns 方法 java.sql.DatabaseMetaData 介面中所指定此 getColumns 方法。  
  
 GetColumns 方法所傳回的結果集將包含下列資訊：  
  
|名稱|型別|Description|  
|----------|----------|-----------------|  
|TABLE_CAT|**字串**|目錄的名稱。|  
|TABLE_SCHEM|**字串**|資料表結構描述名稱。|  
|TABLE_NAME|**字串**|資料表名稱。|  
|COLUMN_NAME|**字串**|資料行名稱。|  
|DATA_TYPE|**smallint**|來自 java.sql.Types 的 SQL 資料型別。|  
|TYPE_NAME|**字串**|資料類型的名稱。|  
|COLUMN_SIZE|**int**|資料行的有效位數。|  
|BUFFER_LENGTH|**smallint**|資料的傳送大小。|  
|DECIMAL_DIGITS|**smallint**|資料行的小數位數。|  
|NUM_PREC_RADIX|**smallint**|資料行的基數。|  
|NULLABLE|**smallint**|指出資料行是否可為 Null。 它可能是下列其中一個值：<br /><br /> columnNoNulls (0)<br /><br /> columnNullable (1)|  
|REMARKS|**字串**|與資料行相關聯的註解。<br /><br /> **注意：** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]一定會傳回 null，此資料行。  |  
|COLUMN_DEF|**字串**|資料行的預設值。|  
|SQL_DATA_TYPE|**smallint**|SQL 資料類型出現在描述子之 TYPE 欄位時的值。 除了 datetime 和 SQL-92 interval 資料類型，這個資料行與 DATA_TYPE 資料行相同。 這個資料行一律會傳回值。|  
|SQL_DATETIME_SUB|**smallint**|datetime 和 SQL-92 interval 資料類型的子類型代碼。 其他資料類型的這個資料行都會傳回 NULL。|  
|CHAR_OCTET_LENGTH|**int**|資料行中的最大位元組數。|  
|ORDINAL_POSITION|**int**|資料表內資料行的索引。|  
|IS_NULLABLE|**字串**|指出資料行是否允許為 Null 值。|  
|SS_IS_SPARSE|**smallint**|如果資料行是疏鬆資料行，這會有值為 1，否則為 0。<sup>1</sup>|  
|SS_IS_COLUMN_SET|**smallint**|如果資料行為疏鬆資料行 column_set，這個值為 1，否則為 0。 <sup>1</sup>|  
|SS_IS_COMPUTED|**smallint**|指出 TABLE_TYPE 中的資料行是否為計算資料行。 <sup>1</sup>|  
|IS_AUTOINCREMENT|**字串**|如果資料行會自動累加則為 "YES"， 如果資料行不會自動累加則為 "NO"。 如果驅動程式無法判斷資料行是否會自動累加，則為 "" (空字串)。 <sup>1</sup>|  
|SS_UDT_CATALOG_NAME|**字串**|包含使用者定義型別 (UDT) 的目錄名稱。 <sup>1</sup>|  
|SS_UDT_SCHEMA_NAME|**字串**|包含使用者定義型別 (UDT) 的結構描述名稱。 <sup>1</sup>|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**字串**|完整名稱的使用者定義型別 (UDT)。 <sup>1</sup>|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**字串**|定義 XML 結構描述集合名稱所在目錄的名稱。 如果找不到目錄名稱，則此變數包含空字串。 <sup>1</sup>|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**字串**|定義 XML 結構描述集合名稱所在結構描述的名稱。 如果找不到結構描述名稱，這就是空字串。 <sup>1</sup>|  
|SS_XML_SCHEMACOLLECTION_NAME|**字串**|XML 結構描述集合的名稱。 如果找不到該名稱，這就是空字串。 <sup>1</sup>|  
|SS_DATA_TYPE|**tinyint**|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料型別，由擴充預存程序。<br /><br /> **請注意**如需有關所傳回的資料型別[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]，請參閱中的 < 資料類型 (TRANSACT-SQL) >[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]線上叢書 》。|  
  
 （1） 這個資料行不會出現，如果您要連接到[!INCLUDE[ssVersion2005](../../../includes/ssversion2005_md.md)]。  
  
> [!NOTE]  
>  多個 getColumns 方法所傳回的資料的詳細資訊，請參閱 「 sp_columns (TRANSACT-SQL) 」，在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]線上叢書 》。  
  
 在[!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0 中，您將看到以下行為變更舊版 JDBC 驅動程式：  
  
 DATA_TYPE 資料行有下列變更：  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料類型|JDBC 驅動程式 2.0 中的傳回類型 (或者，如果連接到[!INCLUDE[ssVersion2005](../../../includes/ssversion2005_md.md)]) 和相關聯的數值常數|當連接到 JDBC 驅動程式 3.0 中的傳回類型[!INCLUDE[ssKatmai](../../../includes/sskatmai_md.md)]或更新版本|  
|-------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|  
|大於 8 kB 的使用者定義型別|LONGVARBINARY (-4)|VARBINARY (-3)|  
|地理位置|LONGVARBINARY (-4)|VARBINARY (-3)|  
|幾何|LONGVARBINARY (-4)|VARBINARY (-3)|  
|varbinary(max)|LONGVARBINARY (-4)|VARBINARY (-3)|  
|nvarchar(max)|LONGVARCHAR (-1) 或 LONGNVARCHAR (JDBC 4) (-16)|VARCHAR (12) 或 NVARCHAR (JDBC 4) (-9)|  
|varchar(max)|LONGVARCHAR (-1)|VARCHAR (12)|  
|time|VARCHAR (12) 或 NVARCHAR (JDBC 4) (-9)|TIME (-154)|  
|date|VARCHAR (12) 或 NVARCHAR (JDBC 4) (-9)|DATE (91)|  
|datetime2|VARCHAR (12) 或 NVARCHAR (JDBC 4) (-9)|TIMESTAMP (93)|  
|datetimeoffset|VARCHAR (12) 或 NVARCHAR (JDBC 4) (-9)|microsoft.sql.Types.DATETIMEOFFSET  (-155)|  
  
 COLUMN_SIZE 資料行有下列變更：  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料類型|JDBC Driver 2.0 中的傳回類型|JDBC Driver 3.0 中的傳回類型|  
|-------------------------------------------------------------------|------------------------------------|------------------------------------|  
|nvarchar(max)|1073741823|2147483647 (資料庫中繼資料)|  
|xml|1073741823|2147483647 (資料庫中繼資料)|  
|小於或等於 8 kB 的使用者定義型別|8 kB (結果集和參數中繼資料)|預存程序傳回的實際大小。|  
|time||該類型的字串表示法長度 (以字元為單位)，假設最大值可以容納分數秒元件的有效位數。|  
|date||與 time 相同|  
|datetime2||與 time 相同|  
|datetimeoffset||與 time 相同|  
  
 BUFFER_LENGTH 資料行有下列變更：  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料類型|JDBC Driver 2.0 中的傳回類型|JDBC Driver 3.0 中的傳回類型|  
|-------------------------------------------------------------------|------------------------------------|------------------------------------|  
|大於 8 kB 的使用者定義型別||2147483647|  
  
 TYPE_NAME 資料行有下列變更：  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料類型|JDBC Driver 2.0 中的傳回類型|JDBC Driver 3.0 中的傳回類型|  
|-------------------------------------------------------------------|------------------------------------|------------------------------------|  
|varchar(max)|text|varchar|  
|varbinary(max)|image|varbinary|  
  
 DECIMAL_DIGITS 資料行有下列變更：  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 類型|JDBC Driver 2.0|JDBC Driver 3.0|  
|--------------------------------------------------------------|---------------------|---------------------|  
|time|null|7 (如果有指定的話，則為更小的值)|  
|date|null|null|  
|datetime2|null|7 (如果有指定的話，則為更小的值)|  
|datetimeoffset|null|7 (如果有指定的話，則為更小的值)|  
  
 SQL_DATA_TYPE 資料行有下列變更：  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料類型|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]2008 JDBC 驅動程式 2.0 中的資料值。|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]2008 JDBC 驅動程式 3.0 中的資料值。|  
|-------------------------------------------------------------------|--------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|  
|varchar(max)|-10|-9|  
|nvarchar(max)|-1|-9|  
|xml|-10|-152|  
|小於或等於 8 kB 的使用者定義型別|-3|-151|  
|大於 8 kB 的使用者定義型別|不適用於 JDBC Driver 2.0|-151|  
|地理位置|-4|-151|  
|幾何|-4|-151|  
|hierarchyid|-4|-151|  
|time|-9|92|  
|date|-9|91|  
|datetime2|-9|93|  
|datetimeoffset|-9|-155|  
  
## <a name="example"></a>範例  
 下列範例示範如何使用 getColumns 方法傳回的 Person.Contact 資料表中的資訊[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]範例資料庫。  
  
```  
import java.sql.*;  
public class c1 {  
   public static void main(String[] args) {  
      String connectionUrl = "jdbc:sqlserver://localhost:1433;databaseName=AdventureWorks;integratedsecurity=true";  
  
      Connection con = null;  
      Statement stmt = null;  
      ResultSet rs = null;  
  
      try {  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         con = DriverManager.getConnection(connectionUrl);  
         DatabaseMetaData dbmd = con.getMetaData();  
         rs = dbmd.getColumns("AdventureWorks", "Person", "Contact", "FirstName");  
  
         ResultSet r = dbmd.getColumns(null, null, "Contact", null);  
         ResultSetMetaData rm = r.getMetaData();   
         int noofcols = rm.getColumnCount();  
  
         if (r.next())  
            for (int i = 0 ; i < noofcols ; i++ )  
            System.out.println(rm.getColumnName( i + 1 ) + ": \t\t" + r.getString( i + 1 ));  
      }  
  
      catch (Exception e) {}  
      finally {}  
   }  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

