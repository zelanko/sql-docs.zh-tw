---
title: 使用基本 JDBC 資料類型
description: Microsoft JDBC Driver for SQL Server 會使用基本 JDBC 資料類型，將 SQL Server 資料類型轉換成 Java 能夠理解的格式。
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d7044936-5b8c-4def-858c-28a11ef70a97
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 97c0d4b269bfda9a9c01bf8b08f93e2b2f5f83d5
ms.sourcegitcommit: 66407a7248118bb3e167fae76bacaa868b134734
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81728377"
---
# <a name="using-basic-data-types"></a>使用基本資料類型

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 使用 JDBC 基本資料類型，將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型和 Java 程式設計語言轉換成彼此理解的格式。 JDBC 驅動程式提供 JDBC 4.0 API 的支援，其中包括 **SQLXML** 資料類型和國家 (Unicode) 資料類型，例如 **NCHAR**、**NVARCHAR**、**LONGNVARCHAR** 和 **NCLOB**。  
  
## <a name="data-type-mappings"></a>資料類型對應

下表列出基本 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、JDBC 及 Java 程式設計語言資料類型之間的預設對應：  
  
| SQL Server 類型   | JDBC 類型 (java.sql.Types)                        | Java 語言類型          |
| ------------------ | -------------------------------------------------- | ---------------------------- |
| BIGINT             | bigint                                             | long                         |
| BINARY             | BINARY                                             | byte[]                       |
| bit                | BIT                                                | boolean                      |
| char               | CHAR                                               | String                       |
| date               | 日期                                               | java.sql.Date                |
| Datetime           | timestamp                                          | java.sql.Timestamp           |
| datetime2          | timestamp                                          | java.sql.Timestamp           |
| datetimeoffset (2) | microsoft.sql.Types.DATETIMEOFFSET                 | microsoft.sql.DateTimeOffset |
| decimal            | DECIMAL                                            | java.math.BigDecimal         |
| FLOAT              | DOUBLE                                             | double                       |
| image              | LONGVARBINARY                                      | byte[]                       |
| int                | INTEGER                                            | int                          |
| money              | DECIMAL                                            | java.math.BigDecimal         |
| NCHAR              | CHAR<br /><br /> NCHAR (Java SE 6.0)               | String                       |
| ntext              | LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0) | String                       |
| NUMERIC            | NUMERIC                                            | java.math.BigDecimal         |
| NVARCHAR           | VARCHAR<br /><br /> NVARCHAR (Java SE 6.0)         | String                       |
| nvarchar(max)      | VARCHAR<br /><br /> NVARCHAR (Java SE 6.0)         | String                       |
| real               | real                                               | FLOAT                        |
| smalldatetime      | timestamp                                          | java.sql.Timestamp           |
| SMALLINT           | SMALLINT                                           | short                        |
| SMALLMONEY         | DECIMAL                                            | java.math.BigDecimal         |
| text               | LONGVARCHAR                                        | String                       |
| time               | TIME (1)                                           | java.sql.Time (1)            |
| timestamp          | BINARY                                             | byte[]                       |
| TINYINT            | TINYINT                                            | short                        |
| udt                | VARBINARY                                          | byte[]                       |
| UNIQUEIDENTIFIER   | CHAR                                               | String                       |
| varbinary          | VARBINARY                                          | byte[]                       |
| varbinary(max)     | VARBINARY                                          | byte[]                       |
| varchar            | VARCHAR                                            | String                       |
| varchar(max)       | VARCHAR                                            | String                       |
| Xml                | LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0) | String<br /><br /> SQLXML    |
| sqlvariant         | SQLVARIANT                                         | Object                       |
| 幾何           | VARBINARY                                          | byte[]                       |
| geography          | VARBINARY                                          | byte[]                       |
  
(1) 若要搭配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 類型 time 使用 java.sql.Time，您必須將 **sendTimeAsDatetime** 連線屬性設為 false。  
  
(2) 您可以使用 [DateTimeOffset 類別](reference/datetimeoffset-class.md)來以程式設計方式存取 **datetimeoffset** 的值。  
  
下列章節會提供如何使用 JDBC Driver 與基本資料類型的範例。 如需如何在 Java 應用程式中使用基本資料類型的更詳細範例，請參閱[基本資料類型範例](basic-data-types-sample.md)。  
  
## <a name="retrieving-data-as-a-string"></a>擷取資料為字串

如果您必須從對應至任何 JDBC 基本資料類型的資料來源擷取資料，以作為字串檢視，或者如果不需要強型別資料，則可以使用 [SQLServerResultSet](reference/sqlserverresultset-class.md) 類別的 [getString](reference/getstring-method-sqlserverresultset.md) 方法，如下所示：  
  
[!code[JDBC#UsingBasicDataTypes1](codesnippet/Java/using-basic-data-types_1.java)]  
  
## <a name="retrieving-data-by-data-type"></a>依資料類型擷取資料

如果您必須從資料來源擷取資料，且您知道正在擷取的資料類型，請使用 SQLServerResultSet 類別的其中一個 get\<Type> 方法，也稱為「getter 方法」  。 您可使用資料行名稱或資料行索引搭配 get\<Type> 方法，如下所示：  
  
[!code[JDBC#UsingBasicDataTypes2](codesnippet/Java/using-basic-data-types_2.java)]  
  
> [!NOTE]  
> 搭配 scale 方法的 getUnicodeStream 與 getBigDecimal 皆已淘汰，JDBC 驅動程式並不支援。

## <a name="updating-data-by-data-type"></a>依資料類型更新資料

如果您必須更新資料來源中的欄位值，請使用 SQLServerResultSet 類別的其中一個 update\<Type> 方法。 在下列範例中，[updateInt](reference/updateint-method-sqlserverresultset.md) 方法會結合 [updateRow](reference/updaterow-method-sqlserverresultset.md) 方法使用，以更新資料來源中的資料：  
  
[!code[JDBC#UsingBasicDataTypes3](codesnippet/Java/using-basic-data-types_3.java)]  
  
> [!NOTE]  
> JDBC Driver 無法更新資料行名稱長度超過 127 個字元的 SQL Server 資料行。 如果嘗試更新名稱超過 127 個字元的資料行，就會擲回例外狀況。  
  
## <a name="updating-data-by-parameterized-query"></a>依參數化查詢更新資料

如果您必須使用參數化查詢更新資料來源中的資料，可以使用 [SQLServerPreparedStatement](reference/sqlserverpreparedstatement-class.md) 類別的其中一個 set\<Type> 方法 (也稱為「setter 方法」  )，來設定參數的資料類型。 在下列範例中，[prepareStatement](reference/preparestatement-method-sqlserverconnection.md) 方法用來預先編譯參數化查詢，然後在呼叫 [executeUpdate](reference/executeupdate-method.md) 方法之前，使用 [setString](reference/setstring-method-sqlserverpreparedstatement.md) 方法設定參數的字串值。  
  
[!code[JDBC#UsingBasicDataTypes4](codesnippet/Java/using-basic-data-types_4.java)]  
  
如需參數化查詢的詳細資訊，請參閱[使用含參數的 SQL 陳述式](using-an-sql-statement-with-parameters.md)。  

## <a name="passing-parameters-to-a-stored-procedure"></a>傳遞參數至預存程序

如果您必須將具類型的參數傳遞至預存程序，可使用 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 類別的其中一個 set\<Type> 方法，依索引或名稱設定參數。 在下列範例中，[prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) 方法用來設定發送給預存程序的呼叫，然後在呼叫 [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 方法之前，使用 [setString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md) 方法設定呼叫的參數。  
  
[!code[JDBC#UsingBasicDataTypes5](codesnippet/Java/using-basic-data-types_5.java)]  
  
> [!NOTE]  
> 在此範例中，結果集會傳回執行預存程序的結果。

如需搭配預存程序和輸入參數使用 JDBC 驅動程式的詳細資訊，請參閱[使用含輸入參數的預存程序](using-a-stored-procedure-with-input-parameters.md)。  

## <a name="retrieving-parameters-from-a-stored-procedure"></a>從預存程序中擷取參數

如果您必須從預存程序擷取參數，必須先使用 SQLServerCallableStatement 類別的 [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) 方法，依據名稱或索引註冊 out 參數，然後在執行發送給預存程序的呼叫之後，將傳回的 out 參數指定給適當的變數。 在下列範例中，prepareCall 方法用來設定發送給預存程序的呼叫，registerOutParameter 方法用來設定 out 參數，，而 [setString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md) 方法則用來在呼叫 executeQuery 方法之前，設定呼叫的參數。 預存程序 out 參數所傳回的值使用 [getShort](../../connect/jdbc/reference/getshort-method-sqlservercallablestatement.md) 方法予以擷取。  
  
[!code[JDBC#UsingBasicDataTypes6](../../connect/jdbc/codesnippet/Java/using-basic-data-types_6.java)]  
  
> [!NOTE]  
> 除了傳回的 out 參數之外，結果集也會傳回執行預存程序的結果。  
  
如需如何搭配預存程序和輸出參數使用 JDBC 驅動程式的詳細資訊，請參閱[使用含輸出參數的預存程序](../../connect/jdbc/using-a-stored-procedure-with-output-parameters.md)。  

## <a name="see-also"></a>另請參閱

[了解 JDBC 驅動程式資料類型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
