---
title: 使用進階資料類型 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b39461d3-48d6-4048-8300-1a886c00756d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 066a56a3c9556ff6e89478a9deeda3716b7d2aac
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924078"
---
# <a name="using-advanced-data-types"></a>使用進階資料類型

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 會使用 JDBC 進階資料類型，將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型轉換為 Java 程式設計語言可以理解的格式。  
  
## <a name="remarks"></a>備註

下表列出進階 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、JDBC 與 Java 程式設計語言資料類型之間的預設對應。  
  
|SQL Server 類型|JDBC 類型 (java.sql.Types)|Java 語言類型|  
|----------------------|-----------------------------------|-------------------------|  
|varbinary(max)<br /><br /> image|LONGVARBINARY|byte[] \(預設值)、Blob、InputStream、String|  
|text<br /><br /> varchar(max)|LONGVARCHAR|String (預設值)、Clob、InputStream|  
|ntext<br /><br /> nvarchar(max)|LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0)|String (default), Clob, NClob|  
|Xml|LONGVARCHAR<br /><br /> SQLXML|String (default), InputStream, Clob, byte[], Blob, SQLXML|  
|Udt<sup>1</sup>|VARBINARY|String (預設值)、byte[]、InputStream|  
|sqlvariant|SQLVARIANT|Object|  
|幾何<br /><br /> geography|VARBINARY|byte[]|  


<sup>1</sup>[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 支援當成二進位資料傳送和擷取 CLR UDT，但不支援操作 CLR 中繼資料。  
  
下列各節會提供如何使用 JDBC Driver 和進階資料類型的範例。  
  
## <a name="blob-and-clob-and-nclob-data-types"></a>BLOB、CLOB 和 NCLOB 資料類型

JDBC 驅動程式會實作 java.sql.Blob、java.sql.Clob 和 java.sql.NClob 介面的所有方法。  
  
> [!NOTE]  
> CLOB 值可以與 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (或更新版本) 大數值資料類型搭配使用。 具體而言，CLOB 類型可以搭配 **varchar(max)** 和 **nvarchar(max)** 資料類型使用、BLOB 類型可以搭配 **varbinary(max)** 和 **image** 資料類型使用，而 NCLOB 類型則可以搭配 **ntext** 和 **nvarchar(max)** 使用。  

## <a name="large-value-data-types"></a>大數值資料類型

在舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，使用大數值資料類型需要特別的處理。 大數值資料類型是指最大資料列大小超過 8 KB 的資料類型。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 推出 max 規範，此規範可用於 **varchar**、**nvarchar** 和 **varbinary** 資料類型，以允許儲存最大可達 2^31 個位元組的值。 資料表資料行和 [!INCLUDE[tsql](../../includes/tsql-md.md)] 變數可以指定 **varchar(max)** 、**nvarchar(max)** 或 **varbinary(max)** 資料類型。  

使用大數值類型的主要狀況包括從資料庫擷取它們，或將它們加入資料庫中。 下列章節說明完成這些工作的不同方法。  

### <a name="retrieving-large-value-types-from-a-database"></a>從資料庫擷取大數值類型

當您從資料庫擷取非二進位大型數值的資料類型 (例如 **varchar(max)** 資料類型) 時，方法之一就是以字元串流的形式讀取資料。 在下列範例中，[SQLServerStatement](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 類別的 [executeQuery](../../connect/jdbc/reference/sqlserverstatement-class.md) 方法可用於從資料庫擷取資料，並將該資料當成結果集傳回。 而 [SQLServerResultSet](../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) 類別的 [getCharacterStream](../../connect/jdbc/reference/sqlserverresultset-class.md) 方法可用於從結果集讀取大數值資料。  

```java
ResultSet rs = stmt.executeQuery("SELECT TOP 1 * FROM Test1");  
rs.next();  
Reader reader = rs.getCharacterStream(2);  
```

> [!NOTE]
> 這個相同的方法也可以用於 **text**、**ntext** 和 **nvarchar(max)** 資料類型。  

當您從資料庫擷取二進位大型數值的資料類型 (例如 **varbinary(max)** 資料類型) 時，有幾種方法可以使用。 最有效的方法就是將資料當作二進位資料流來讀取，如下所示：  

```java
ResultSet rs = stmt.executeQuery("SELECT photo FROM mypics");  
rs.next();  
InputStream is = rs.getBinaryStream(2);  
```

您也可以使用 [getBytes](../../connect/jdbc/reference/getbytes-method-sqlserverresultset.md) 方法，將資料當成位元組陣列來讀取，如下所示：  

```java
ResultSet rs = stmt.executeQuery("SELECT photo FROM mypics");  
rs.next();  
byte [] b = rs.getBytes(2);  
```

> [!NOTE]  
> 您也可以將資料當作 BLOB 讀取。 不過，比起上面顯示的兩種方法，這個方法比較沒有效率。  

### <a name="adding-large-value-types-to-a-database"></a>將大數值類型加入資料庫

以 JDBC 驅動程式上傳大型資料非常適合記憶體大小的情況，至於大於記憶體的情況，資料流則是最佳的選項。 不過，上傳大型資料的最有效方式，其實是透過資料流介面。  

也可以選擇使用字串或位元組，如下所示：  

```java
PreparedStatement pstmt = con.prepareStatement("INSERT INTO test1 (c1_id, c2_vcmax) VALUES (?, ?)");  
pstmt.setInt(1, 1);  
pstmt.setString(2, htmlStr);  
pstmt.executeUpdate();  
```

> [!NOTE]  
> 此方法也可用於儲存在 **text**、**ntext** 和 **nvarchar(max)** 資料行中的值。  

如果您在伺服器上具有影像程式庫，且必須將整個二進位影像檔上傳到 **varbinary(max)** 資料行，則使用 JDBC 驅動程式最有效的方法就是直接使用資料流，如下所示：  

```java
try (PreparedStatement pstmt = con.prepareStatement("INSERT INTO test1 (Col1, Col2) VALUES(?,?)")) { 
  File inputFile = new File("CLOBFile20mb.jpg");  
  try (FileInputStream inStream = new FileInputStream(inputFile)) {
    int id = 1;  
    pstmt.setInt(1,id);  
    pstmt.setBinaryStream(2, inStream);  
    pstmt.executeUpdate();
  }
}
```

> [!NOTE]  
> 使用 CLOB 或 BLOB 方法並不是上載大型資料的最有效方法。  

### <a name="modifying-large-value-types-in-a-database"></a>修改資料庫中的大數值類型

在多數情況下，在資料庫上更新或修改大數值的建議方法是使用 [、](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 和 [ 這類 ](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 命令，透過 [!INCLUDE[tsql](../../includes/tsql-md.md)]SQLServerPreparedStatement`UPDATE` 和 `WRITE`SQLServerCallableStatement`SUBSTRING` 類別來傳遞參數。  

如果您必須在大型文字檔 (例如封存的 HTML 檔案) 中取代文字的執行個體，則可以使用 Clob 物件，如下所示：  

```java
String SQL = "SELECT * FROM test1;";  
try (Statement stmt = con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE)
     ResultSet rs = stmt.executeQuery(SQL)) {
  rs.next();

  Clob clob = rs.getClob(2);  
  long pos = clob.position("dog", 1);  
  clob.setString(pos, "cat");  
  rs.updateClob(2, clob);  
  rs.updateRow();  
}
```

此外，您可以在伺服器上執行所有工作，而只將參數傳遞至準備好的 UPDATE 陳述式。  

如需有關大數值類型的詳細資訊，請參閱《SQL Server 線上叢書》中的＜使用大數值類型＞。  

## <a name="xml-data-type"></a>XML 資料類型

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供的 **xml** 資料類型，可讓您在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中儲存 XML 文件和片段。 **xml** 資料類型是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的內建資料類型，而且在某些狀況下類似於其他內建類型，例如 **int** 和 **varchar**。 如同其他內建類型，您可以將 **xml** 資料類型當成建立資料表時的資料行類型；當成變數類型、參數類型或函式傳回類型使用；或者在 [!INCLUDE[tsql](../../includes/tsql-md.md)] CAST 和 CONVERT 函式中使用。  
  
在 JDBC 驅動程式中，**xml** 資料類型可以對應為字串、位元組陣列、資料流、CLOB、BLOB 或 SQLXML 物件。 字串為預設值。 從 JDBC Driver 2.0 版開始，JDBC Driver 提供了 JDBC 4.0 API 的支援，其中導入 SQLXML 介面。 SQLXML 介面會定義與 XML 資料互動和進行操作的方法。 **SQLXML** 資料類型會對應到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **xml** 資料類型。 如需如何在具有 **SQLXML** Java 資料類型的關聯式資料庫中讀取和寫入 XML 資料的詳細資訊，請參閱[支援 XML 資料](../../connect/jdbc/supporting-xml-data.md)。  
  
JDBC 驅動程式中 **xml** 資料類型的實作提供下列項目的支援：  
  
- 在大多數的一般程式設計案例中，存取 XML 作為標準 Java UTF-16 字串  
  
- UTF-8 和其他 8 位元編碼 XML 的輸入  
  
- 採用 UTF-16 編碼以與其他 XML 處理器和磁碟檔案進行交換時，存取 XML 作為具有開頭 BOM 的位元組陣列  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在 UTF-16 編碼的 XML 中需要開頭 BOM。 提供 XML 參數值作為位元組陣列時，應用程式必須提供此項。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一定會將 XML 值輸出為不含 BOM 或內嵌編碼宣告的 UTF-16 字串。 擷取 XML 值當做 byte[]、BinaryStream 或 Blob 時，會將 UTF-16 BOM 附加至值的開頭。  
  
如需 **xml** 資料類型的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜xml 資料類型＞。  
  
## <a name="user-defined-data-type"></a>使用者定義資料類型  

[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中導入使用者定義類型 (UDT)，可讓您在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中儲存物件和自訂資料結構，因而擴充 SQL 類型系統的功能。 UDT 可以包含多個資料類型並可以具有行為，使其有別於由單一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料類型組成的傳統別名資料類型。 使用能產生可驗證程式碼並由 Microsoft .NET Common Language Runtime (CLR) 支援的任何語言，即可定義 UDT。 這包括 Microsoft Visual C# 和 Visual Basic .NET。 資料會公開為 .NET Framework 類別或結構的欄位和屬性，而行為則是由類別或結構的方法所定義。  
  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，UDT 可以用作資料表的資料行定義、[!INCLUDE[tsql](../../includes/tsql-md.md)] 批次中的變數，或是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函式或預存程序的引數。  
  
如需使用者定義資料類型的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜使用和修改使用者定義類型的執行個體＞。  
  
## <a name="sql_variant-data-type"></a>Sql_variant 資料類型

如需有關 sql_variant 資料類型的詳細資訊，請參閱[使用 Sql_variant 資料類型](../../connect/jdbc/using-sql-variant-datatype.md)。  

## <a name="spatial-data-types"></a>空間資料類型

如需有關空間資料類型的詳細資訊，請參閱[使用空間資料類型](../../connect/jdbc/use-spatial-datatypes.md)。  

## <a name="see-also"></a>另請參閱

[了解 JDBC 驅動程式資料類型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
