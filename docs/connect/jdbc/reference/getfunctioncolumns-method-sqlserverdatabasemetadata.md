---
title: getFunctionColumns 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e2b0e0f7-717c-48e6-bcd2-a325d938a833
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e6c25349d6fbf9495647ae73773d984dfcd269f8
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67982966"
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
 *catalog*  
  
 包含目錄名稱的 **String**。 如果它是空字串 ""，結果就會包含函數而不包含目錄。 如果它是 **null**，目錄名稱就不會用於搜尋。  
  
 *schemaPattern*  
  
 包含結構描述名稱模式的 **String**。 如果它是空字串 ""，結果就會包含函數而不包含結構描述。 如果它是 **null**，結構描述名稱就不會用於搜尋。  
  
 *functionNamePattern*  
  
 包含函式名稱的 **String**。  
  
 *columnNamePattern*  
  
 包含參數名稱的 **String**。  
  
## <a name="return-value"></a>傳回值  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getFunctionColumns 方法是由 java.sql.DatabaseMetaData 介面中的 getFunctionColumns 方法指定。  
  
 這個方法只會傳回符合指定目錄中之指定結構描述、函數名稱和參數名稱的函數和參數。  
  
 結果集中的每一個資料列，都會針對參數描述、資料行描述或傳回類型包括下列資料行：  
  
|名稱|類型|描述|  
|----------|----------|-----------------|  
|FUNCTION_CAT|**String**|函數所在之資料庫的名稱。|  
|FUNCTION_SCHEM|**String**|函數的結構描述。|  
|FUNCTION_NAME|**String**|函數的名稱。|  
|COLUMN_NAME|**String**|參數或資料行的名稱。|  
|COLUMN_TYPE|**short**|**資料行的類型。它可以是下列值之一：**<br /><br /> unctionColumnUnknown (0)：未知的類型。<br /><br /> functionColumnIn (1)：輸入參數。<br /><br /> functionColumnInOut (2)：輸入/輸出參數。<br /><br /> functionColumnOut (3)：輸出參數。<br /><br /> functionReturn (4)：函式傳回值。<br /><br /> functionColumnResult (5)：參數或資料行是結果集中的資料行。|  
|DATA_TYPE|**smallint**|來自 Java.sql.Types 的 SQL 資料類型值。|  
|TYPE_NAME|**String**|資料類型的名稱。|  
|PRECISION|**int**|有效位數的總數。|  
|LENGTH|**int**|資料長度 (以位元組為單位)。|  
|SCALE|**short**|小數點右側的位數。|  
|RADIX|**short**|數值類型的基底。|  
|NULLABLE|**short**|指出參數或傳回值是否可以包含 **null** 值。<br /><br /> **它可以是下列值之一：**<br /><br /> functionNoNulls (0)：不允許 NULL 值。<br /><br /> functionNullable (1)：允許 NULL 值。<br /><br /> functionNullableUnknown (2)：未知。|  
|REMARKS|**String**|資料行或參數的相關註解。|  
|COLUMN_DEF|**String**|資料行的預設值。<br /><br /> **注意：** 此資訊由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 提供，且為 JDBC 驅動程式特定。|  
|SQL_DATA_TYPE|**smallint**|除了 **datetime** 和 **ISO interval** 資料類型，這個資料行與 **DATA_TYPE** 資料行相同。<br /><br /> **注意：** 此資訊由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 提供，且為 JDBC 驅動程式特定。|  
|SQL_DATETIME_SUB|**smallint**|**datetime** ISO **interval** 子代碼 (如果 **SQL_DATA_TYPE** 的值是 **SQL_DATETIME** 或 **SQL_INTERVAL**)。 針對 **datetime** 和 ISO **interval** 以外的資料類型，這個資料行會是 NULL。<br /><br /> **注意：** 這項資訊可由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 提供，而且是 JDBC 驅動程式的特定資訊。|  
|CHAR_OCTET_LENGTH|**int**|針對以字元為基礎的參數或資料行之最大二進位長度。 如果是其他資料類型，則為 NULL。|  
|ORDINAL_POSITION|**int**|針對輸入和輸出參數，這代表從位置 1 開始。<br /><br /> 針對結果集資料行，這是結果集中從 1 開始的資料行位置。<br /><br /> 針對傳回值，這個值是 0。|  
|IS_NULLABLE|**String**|決定參數或資料行的 Null 屬性。<br /><br /> 它可能是下列其中一個值：<br /><br /> **YES**：參數或資料行可以包含 NULL 值。<br /><br /> **NO**：參數或資料行不可以包含 NULL 值。<br /><br /> 空字串 ("")：未知。|  
|SS_TYPE_CATALOG_NAME|**String**|包含使用者定義型別 (UDT) 的目錄名稱。|  
|SS_TYPE_SCHEMA_NAME|**String**|包含使用者定義型別 (UDT) 的結構描述名稱。|  
|SS_UDT_CATALOG_NAME|**String**|完整名稱的使用者定義型別 (UDT)。|  
|SS_UDT_SCHEMA_NAME|**String**|定義 XML 結構描述集合名稱所在目錄的名稱。 如果找不到目錄名稱，則此變數包含空字串。|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**String**|定義 XML 結構描述集合名稱所在結構描述的名稱。 如果找不到結構描述名稱，這就是空字串。|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**String**|XML 結構描述集合的名稱。 如果找不到該名稱，這就是空字串。|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**String**|包含使用者定義型別 (UDT) 的目錄名稱。|  
|SS_XML_SCHEMACOLLECTION_NAME|**String**|包含使用者定義型別 (UDT) 的結構描述名稱。|  
|SS_DATA_TYPE|**tinyint**|擴充預存程序所使用的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。<br /><br /> **注意：** 如需 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 所傳回資料類型的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 線上叢書》中的＜資料類型 (Transact-SQL)＞。|  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
