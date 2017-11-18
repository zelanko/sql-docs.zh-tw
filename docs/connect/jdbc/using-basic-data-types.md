---
title: "使用基本資料型別 |Microsoft 文件"
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
ms.assetid: d7044936-5b8c-4def-858c-28a11ef70a97
caps.latest.revision: 73
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e7333b711d828981a93c51b98b7e84fb62a7749b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="using-basic-data-types"></a>使用基本資料類型
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]使用 JDBC 基本資料類型，將轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料類型轉換成可在 Java 程式語言，反之亦然理解的格式。 JDBC 驅動程式提供 JDBC 4.0 API，其中包含支援**SQLXML**資料類型和 National (Unicode) 資料類型，例如**NCHAR**， **NVARCHAR**， **LONGNVARCHAR**，和**NCLOB**。  
  
## <a name="data-type-mappings"></a>資料類型對應  
 下表列出之間的預設對應基本[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]、 JDBC 及 Java 程式語言資料類型：  
  
|SQL Server 類型|JDBC 類型 (java.sql.Types)|Java 語言類型|  
|----------------------|-----------------------------------|-------------------------|  
|bigint|bigint|long|  
|binary|BINARY|byte[]|  
|bit|BIT|boolean|  
|char|CHAR|字串|  
|date|DATE|java.sql.Date|  
|datetime|timestamp|java.sql.Timestamp|  
|datetime2|timestamp|java.sql.Timestamp|  
|datetimeoffset (2)|microsoft.sql.Types.DATETIMEOFFSET|microsoft.sql.DateTimeOffset|  
|decimal|DECIMAL|java.math.BigDecimal|  
|float|DOUBLE|double|  
|image|LONGVARBINARY|byte[]|  
|int|INTEGER|int|  
|money|DECIMAL|java.math.BigDecimal|  
|nchar|CHAR<br /><br /> NCHAR (Java SE 6.0)|字串|  
|ntext|LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0)|字串|  
|numeric|NUMERIC|java.math.BigDecimal|  
|nvarchar|VARCHAR<br /><br /> NVARCHAR (Java SE 6.0)|字串|  
|nvarchar(max)|VARCHAR<br /><br /> NVARCHAR (Java SE 6.0)|字串|  
|real|REAL|float|  
|smalldatetime|timestamp|java.sql.Timestamp|  
|smallint|SMALLINT|short|  
|smallmoney|DECIMAL|java.math.BigDecimal|  
|text|LONGVARCHAR|字串|  
|time|TIME (1)|java.sql.Time (1)|  
|timestamp|BINARY|byte[]|  
|tinyint|TINYINT|short|  
|udt|VARBINARY|byte[]|  
|uniqueidentifier|CHAR|字串|  
|varbinary|VARBINARY|byte[]|  
|varbinary(max)|VARBINARY|byte[]|  
|varchar|VARCHAR|字串|  
|varchar(max)|VARCHAR|字串|  
|xml|LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0)|字串<br /><br /> SQLXML|  
  
 （1） 若要使用 java.sql.Time 的時間[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]類型，您必須設定**sendTimeAsDatetime**連接屬性設定為 false。  
  
 （2） 您可以程式設計方式存取值**datetimeoffset**與[DateTimeOffset 類別](../../connect/jdbc/reference/datetimeoffset-class.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] JDBC 驅動程式目前不支援 sqlvariant 資料類型。 如果使用查詢以擷取資料表 (包含 sqlvariant 資料類型的資料行) 的資料，會發生例外狀況。  
  
 下列章節會提供如何使用 JDBC Driver 與基本資料類型的範例。 如何在 Java 應用程式中使用的基本資料類型的更詳細範例，請參閱[基本資料類型範例](../../connect/jdbc/basic-data-types-sample.md)。  
  
## <a name="retrieving-data-as-a-string"></a>擷取資料為字串  
 如果您必須從對應至任何 JDBC 基本資料類型為字串時，檢視資料來源擷取資料，或者如果不需要強類型的資料，您可以使用[getString](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md)方法[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)類別，如下所示：  
  
 [!code[JDBC#UsingBasicDataTypes1](../../connect/jdbc/codesnippet/Java/using-basic-data-types_1.java)]  
  
## <a name="retrieving-data-by-data-type"></a>依資料類型擷取資料  
 如果您有資料來源擷取資料，而且您知道正在擷取的資料類型，使用其中一種 get\<類型 > SQLServerResultSet 的方法類別，也稱為*getter 方法*。 您可以使用資料行名稱或資料行索引 get\<類型 > 方法，如下所示：  
  
 [!code[JDBC#UsingBasicDataTypes2](../../connect/jdbc/codesnippet/Java/using-basic-data-types_2.java)]  
  
> [!NOTE]  
>  GetUnicodeStream 和 getBigDecimal 與小數位數的方法已被取代，並不會受到 JDBC 驅動程式。  
  
## <a name="updating-data-by-data-type"></a>依資料類型更新資料  
 如果您有更新的資料來源中的欄位值，請使用其中一種更新\<類型 > SQLServerResultSet 類別的方法。 在下列範例中， [updateInt](../../connect/jdbc/reference/updateint-method-sqlserverresultset.md)方法用於搭配[updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md)方法，以更新資料來源中的資料：  
  
 [!code[JDBC#UsingBasicDataTypes3](../../connect/jdbc/codesnippet/Java/using-basic-data-types_3.java)]  
  
> [!NOTE]  
>  JDBC Driver 無法更新資料行名稱長度超過 127 個字元的 SQL Server 資料行。 如果嘗試更新名稱超過 127 個字元的資料行，就會擲回例外狀況。  
  
## <a name="updating-data-by-parameterized-query"></a>依參數化查詢更新資料  
 如果您有使用參數化的查詢更新資料來源中的資料，您可以使用一組設定參數的資料型別\<類型 > 的方法[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)類別，也稱為*setter 方法*。 在下列範例中， [prepareStatement](../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md)方法用來預先編譯參數化的查詢，然後[setString](../../connect/jdbc/reference/setstring-method-sqlserverpreparedstatement.md)方法用來設定之前參數的字串值[executeUpdate](../../connect/jdbc/reference/executeupdate-method.md)方法呼叫。  
  
 [!code[JDBC#UsingBasicDataTypes4](../../connect/jdbc/codesnippet/Java/using-basic-data-types_4.java)]  
  
 如需參數化查詢的詳細資訊，請參閱[搭配參數使用 SQL 陳述式](../../connect/jdbc/using-an-sql-statement-with-parameters.md)。  
  
## <a name="passing-parameters-to-a-stored-procedure"></a>傳遞參數至預存程序  
 如果您有將具型別的參數傳遞至預存程序，您可以透過一組設定的參數，依索引或名稱\<類型 > 的方法[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)類別。 在下列範例中， [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)方法用來設定預存程序呼叫，然後[setString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md)方法用來將之前呼叫的參數設定[executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md)方法呼叫。  
  
 [!code[JDBC#UsingBasicDataTypes5](../../connect/jdbc/codesnippet/Java/using-basic-data-types_5.java)]  
  
> [!NOTE]  
>  在此範例中，結果集會傳回執行預存程序的結果。  
  
 如需以預存程序和輸入的參數使用 JDBC 驅動程式的詳細資訊，請參閱[使用輸入參數的預存程序](../../connect/jdbc/using-a-stored-procedure-with-input-parameters.md)。  
  
## <a name="retrieving-parameters-from-a-stored-procedure"></a>從預存程序中擷取參數  
 如果您必須從預存程序擷取參數，您必須先註冊 out 參數的名稱或索引使用[registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) SQLServerCallableStatement 類別，然後將指派的方法執行預存程序呼叫之後傳回 out 參數的適當的變數。 在下列範例中，prepareCall 方法用來設定預存程序的呼叫、 registerOutParameter 方法用來設定 out 參數，然後[setString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md)方法用來設定的參數在呼叫 executeQuery 方法之前呼叫。 擷取預存程序的 out 參數傳回值是使用[getShort](../../connect/jdbc/reference/getshort-method-sqlservercallablestatement.md)方法。  
  
 [!code[JDBC#UsingBasicDataTypes6](../../connect/jdbc/codesnippet/Java/using-basic-data-types_6.java)]  
  
> [!NOTE]  
>  除了傳回的 out 參數之外，結果集也會傳回執行預存程序的結果。  
  
 如需如何搭配預存程序和輸出參數使用 JDBC 驅動程式的詳細資訊，請參閱[使用輸出參數的預存程序](../../connect/jdbc/using-a-stored-procedure-with-output-parameters.md)。  
  
## <a name="see-also"></a>另請參閱  
 [了解 JDBC Driver 資料類型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  

