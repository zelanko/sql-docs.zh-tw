---
title: "getFunctionColumns 方法 (SQLServerDatabaseMetaData) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e2b0e0f7-717c-48e6-bcd2-a325d938a833
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1508d70610c47116a4aaf58063b0f4196459d3e4
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getfunctioncolumns-method-sqlserverdatabasemetadata"></a>getFunctionColumns 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取所指定目錄的系統函數或使用者函數之參數和傳回類型的描述。  
  
## <a name="syntax"></a>語法  
  
```  
  
public ResultSet getFunctionColumns(java.lang.String catalog,  
                       java.lang.String schemaPattern,  
                       java.lang.String functionNamePattern  
                       java.lang.String columnNamePattern)  
```  
  
#### <a name="parameters"></a>參數  
 *類別目錄*  
  
 A**字串**，其中包含目錄名稱。 如果它是空字串 ""，結果就會包含函數而不包含目錄。 如果是**null**，目錄名稱不會用於搜尋。  
  
 *schemaPattern*  
  
 A**字串**，包含結構描述名稱模式。 如果它是空字串 ""，結果就會包含函數而不包含結構描述。 如果是**null**，結構描述名稱不會用於搜尋。  
  
 *functionNamePattern*  
  
 A**字串**包含函式的名稱。  
  
 *columnNamePattern*  
  
 A**字串**，其中包含參數的名稱。  
  
## <a name="return-value"></a>傳回值  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getFunctionColumns 方法是由 java.sql.DatabaseMetaData 介面中 getFunctionColumns 方法指定。  
  
 這個方法只會傳回符合指定目錄中之指定結構描述、函數名稱和參數名稱的函數和參數。  
  
 結果集中的每一個資料列，都會針對參數描述、資料行描述或傳回類型包括下列資料行：  
  
|名稱|型別|Description|  
|----------|----------|-----------------|  
|FUNCTION_CAT|**字串**|函數所在之資料庫的名稱。|  
|FUNCTION_SCHEM|**字串**|函數的結構描述。|  
|FUNCTION_NAME|**字串**|函數的名稱。|  
|COLUMN_NAME|**字串**|參數或資料行的名稱。|  
|COLUMN_TYPE|**短**|**資料行的類型。它可以是下列值之一：**<br /><br /> functionColumnUnknown (0)：未知的類型。<br /><br /> functionColumnIn (1)：輸入參數。<br /><br /> functionColumnInOut (2)：輸入/輸出參數。<br /><br /> functionColumnOut (3)：輸出參數。<br /><br /> functionReturn (4)：函數傳回值。<br /><br /> functionColumnResult (5)：參數或資料行是結果集中的資料行。|  
|DATA_TYPE|**smallint**|SQL 資料類型從 Java.sql.Types 的值。|  
|TYPE_NAME|**字串**|資料類型的名稱。|  
|PRECISION|**int**|有效位數的總數。|  
|LENGTH|**int**|資料長度 (以位元組為單位)。|  
|SCALE|**短**|小數點右側的位數。|  
|RADIX|**短**|數值類型的基底。|  
|NULLABLE|**短**|指出是否可以包含參數或傳回值**null**值。<br /><br /> **它可以是下列值之一：**<br /><br /> functionNoNulls (0)：不允許 NULL 值。<br /><br /> functionNullable (1)：允許 NULL 值。<br /><br /> functionNullableUnknown (2)：未知。|  
|REMARKS|**字串**|資料行或參數的相關註解。|  
|COLUMN_DEF|**字串**|資料行的預設值。<br /><br /> **注意：**這項資訊適用於[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]和是 JDBC 驅動程式專屬。|  
|SQL_DATA_TYPE|**smallint**|此資料行等同於**DATA_TYPE**資料行，除了**datetime**和 ISO**間隔**資料型別。<br /><br /> **注意：**這項資訊適用於[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]和是 JDBC 驅動程式專屬。|  
|SQL_DATETIME_SUB|**smallint**|**Datetime** ISO**間隔**子代碼，如果值**SQL_DATA_TYPE**是**SQL_DATETIME**或**SQL_INTERVAL**. 資料類型以外**datetime**和 ISO**間隔**，此資料行為 unll。<br /><br /> **注意：**這項資訊適用於[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]和是 JDBC 驅動程式專屬。|  
|CHAR_OCTET_LENGTH|**int**|針對以字元為基礎的參數或資料行之最大二進位長度。 如果是其他資料類型，則為 NULL。|  
|ORDINAL_POSITION|**int**|針對輸入和輸出參數，這代表從位置 1 開始。<br /><br /> 針對結果集資料行，這是結果集中從 1 開始的資料行位置。<br /><br /> 針對傳回值，這個值是 0。|  
|IS_NULLABLE|**字串**|決定參數或資料行的 Null 屬性。<br /><br /> 它可能是下列其中一個值：<br /><br /> **[是]**： 參數或資料行可以包含 NULL 值。<br /><br /> **否**： 參數或資料行不能包含 NULL 值。<br /><br /> 空字串 ("")：未知。|  
|SS_TYPE_CATALOG_NAME|**字串**|包含使用者定義型別 (UDT) 的目錄名稱。|  
|SS_TYPE_SCHEMA_NAME|**字串**|包含使用者定義型別 (UDT) 的結構描述名稱。|  
|SS_UDT_CATALOG_NAME|**字串**|完整名稱的使用者定義型別 (UDT)。|  
|SS_UDT_SCHEMA_NAME|**字串**|定義 XML 結構描述集合名稱所在目錄的名稱。 如果找不到目錄名稱，則此變數包含空字串。|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**字串**|定義 XML 結構描述集合名稱所在結構描述的名稱。 如果找不到結構描述名稱，這就是空字串。|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**字串**|XML 結構描述集合的名稱。 如果找不到該名稱，這就是空字串。|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**字串**|包含使用者定義型別 (UDT) 的目錄名稱。|  
|SS_XML_SCHEMACOLLECTION_NAME|**字串**|包含使用者定義型別 (UDT) 的結構描述名稱。|  
|SS_DATA_TYPE|**tinyint**|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料型別，由擴充預存程序。<br /><br /> **請注意**如需有關所傳回的資料型別[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]，請參閱中的 < 資料類型 (TRANSACT-SQL) >[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]線上叢書 》。|  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

