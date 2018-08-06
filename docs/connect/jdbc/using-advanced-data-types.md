---
title: 使用進階的資料類型 |Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b39461d3-48d6-4048-8300-1a886c00756d
caps.latest.revision: 58
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9ef615f695209cf01c2307c53effc7e84b06eb11
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/27/2018
ms.locfileid: "39278609"
---
# <a name="using-advanced-data-types"></a>使用進階資料類型
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 會使用 JDBC 進階資料類型，將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 資料類型轉換為 Java 程式設計語言可以理解的格式。  
  
## <a name="remarks"></a>Remarks  
 下表列出進階 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]、JDBC 與 Java 程式設計語言資料類型之間的預設對應。  
  
|SQL Server 類型|JDBC 類型 (java.sql.Types)|Java 語言類型|  
|----------------------|-----------------------------------|-------------------------|  
|varbinary(max)<br /><br /> image|LONGVARBINARY|byte[] \(預設值)、Blob、InputStream、String|  
|text<br /><br /> varchar(max)|LONGVARCHAR|String (預設值)、Clob、InputStream|  
|ntext<br /><br /> nvarchar(max)|LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0)|String (預設值)、Clob、NClob (Java SE 6.0)|  
|xml|LONGVARCHAR<br /><br /> SQLXML (Java SE 6.0)|String (預設值)、InputStream、Clob、byte[]、Blob、SQLXML (Java SE 6.0)|  
|Udt<sup>1</sup>|VARBINARY|String (預設值)、byte[]、InputStream|  
  
 <sup>1</sup> [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 支援當成二進位資料傳送和擷取 CLR UDT，但不支援操作 CLR 中繼資料。  
  
 下列各節會提供如何使用 JDBC Driver 和進階資料類型的範例。  
  
## <a name="blob-and-clob-and-nclob-data-types"></a>BLOB、CLOB 和 NCLOB 資料類型  
 JDBC 驅動程式會實作 java.sql.Blob、java.sql.Clob 和 java.sql.NClob 介面的所有方法。  
  
> [!NOTE]  
>  CLOB 值可以與 [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] (或更新版本) 大數值資料類型搭配使用。 明確地說，CLOB 型別可以搭配**varchar （max)** 並**nvarchar （max)** 資料類型、 BLOB 型別可以搭配**varbinary （max)** 並**映像**資料類型，而 NCLOB 型別可以搭配**ntext**並**nvarchar （max)**。  
  
## <a name="large-value-data-types"></a>大數值資料類型  
 在舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 中，使用大數值資料類型需要特別的處理。 大數值資料類型是指最大資料列大小超過 8 KB 的資料類型。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 推出 max 規範，此規範可用於 **varchar**、**nvarchar** 和 **varbinary** 資料類型，以允許儲存最大可達 2^31 個位元組的值。 資料表資料行和 [!INCLUDE[tsql](../../includes/tsql_md.md)] 變數可以指定 **varchar(max)**、**nvarchar(max)** 或 **varbinary(max)** 資料類型。  
  
 使用大數值類型的主要狀況包括從資料庫擷取它們，或將它們加入資料庫中。 下列章節說明完成這些工作的不同方法。  
  
### <a name="retrieving-large-value-types-from-a-database"></a>從資料庫擷取大數值類型  
 從資料庫擷取非二進位的大數值資料類型 (例如 **varchar(max)** 資料類型) 時，有種方法是將該資料當成字元資料流來讀取。 在下列範例中，[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 類別的 [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 方法可用於從資料庫擷取資料，並將該資料當成結果集傳回。 而 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 類別的 [getCharacterStream](../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) 方法可用於從結果集讀取大數值資料。  
  
```java
ResultSet rs = stmt.executeQuery("SELECT TOP 1 * FROM Test1");  
rs.next();  
Reader reader = rs.getCharacterStream(2);  
```  
  
> [!NOTE]  
>  這個方法也會用於**文字**， **ntext**，並**nvarchar （max)** 資料型別。  
  
 從資料庫擷取二進位的大數值資料類型 (例如 **varbinary(max)** 資料類型) 時，有數種方法可供您使用。 最有效的方法就是將資料當作二進位資料流來讀取，如下所示：  
  
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
>  您也可以將資料當作 BLOB 讀取。 不過，比起上面顯示的兩種方法，這個方法比較沒有效率。  
  
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
>  這種方法也可以用於儲存在中的值**文字**， **ntext**，並**nvarchar （max)** 資料行。  
  
 如果您在伺服器上具有影像程式庫，且必須將整個二進位影像檔上傳到 **varbinary(max)** 資料行，則使用 JDBC 驅動程式最有效的方法就是直接使用資料流，如下所示：  
  
```java
PreparedStatement pstmt = con.prepareStatement("INSERT INTO test1 (Col1, Col2) VALUES(?,?)");  
File inputFile = new File("CLOBFile20mb.jpg");  
FileInputStream inStream = new FileInputStream(inputFile);  
int id = 1;  
pstmt.setInt(1,id);  
pstmt.setBinaryStream(2, inStream);  
pstmt.executeUpdate();  
inStream.close();  
```  
  
> [!NOTE]  
>  使用 CLOB 或 BLOB 方法並不是上載大型資料的最有效方法。  
  
### <a name="modifying-large-value-types-in-a-database"></a>修改資料庫中的大數值類型  
 在多數情況下，在資料庫上更新或修改大數值的建議方法是使用 UPDATE、WRITE 和 SUBSTRING 這類 [!INCLUDE[tsql](../../includes/tsql_md.md)] 命令，透過 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 和 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 類別傳遞參數。  
  
 如果您必須在大型文字檔 (例如封存的 HTML 檔案) 中取代文字的執行個體，則可以使用 Clob 物件，如下所示：  
  
```java
String SQL = "SELECT * FROM test1;";  
Statement stmt = con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE);  
ResultSet rs = stmt.executeQuery(SQL);  
rs.next();  
  
Clob clob = rs.getClob(2);  
long pos = clob.position("dog", 1);  
clob.setString(pos, "cat");  
rs.updateClob(2, clob);  
rs.updateRow();  
```  
  
 此外，您可以在伺服器上執行所有工作，而只將參數傳遞至準備好的 UPDATE 陳述式。  
  
 如需有關大數值類型的詳細資訊，請參閱《SQL Server 線上叢書》中的＜使用大數值類型＞。  
  
## <a name="xml-data-type"></a>XML 資料類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 提供的 **xml** 資料類型，可讓您在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 資料庫中儲存 XML 文件和片段。 **xml** 資料類型是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 中的內建資料類型，而且在某些狀況下類似於其他內建類型，例如 **int** 和 **varchar**。 如同其他內建類型，您可以將 **xml** 資料類型當成建立資料表時的資料行類型；當成變數類型、參數類型或函式傳回類型使用；或者在 [!INCLUDE[tsql](../../includes/tsql_md.md)] CAST 和 CONVERT 函式中使用。  
  
 在 JDBC 驅動程式中，**xml** 資料類型可以對應為字串、位元組陣列、資料流、CLOB、BLOB 或 SQLXML 物件。 字串為預設值。 從 JDBC Driver 2.0 版開始，JDBC Driver 提供了 JDBC 4.0 API 的支援，其中導入 SQLXML 介面。 SQLXML 介面會定義與 XML 資料互動和進行操作的方法。 **SQLXML**資料類型會對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **xml**資料型別。 如需如何在具有 **SQLXML** Java 資料類型的關聯式資料庫中讀取和寫入 XML 資料的詳細資訊，請參閱[支援 XML 資料](../../connect/jdbc/supporting-xml-data.md)。  
  
 JDBC 驅動程式中 **xml** 資料類型的實作提供下列項目的支援：  
  
-   在大多數的一般程式設計案例中，存取 XML 作為標準 Java UTF-16 字串  
  
-   UTF-8 和其他 8 位元編碼 XML 的輸入  
  
-   採用 UTF-16 編碼以與其他 XML 處理器和磁碟檔案進行交換時，存取 XML 作為具有開頭 BOM 的位元組陣列  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 在 UTF-16 編碼的 XML 中需要開頭 BOM。 提供 XML 參數值作為位元組陣列時，應用程式必須提供此項。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 一定會將 XML 值輸出為不含 BOM 或內嵌編碼宣告的 UTF-16 字串。 擷取 XML 值當做 byte[]、BinaryStream 或 Blob 時，會將 UTF-16 BOM 附加至值的開頭。  
  
 如需 **xml** 資料類型的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 線上叢書》中的＜xml 資料類型＞。  
  
## <a name="user-defined-data-type"></a>使用者定義資料類型  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] 中導入使用者定義類型 (UDT)，可讓您在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 資料庫中儲存物件和自訂資料結構，因而擴充 SQL 類型系統的功能。 UDT 可以包含多個資料類型並可以具有行為，使其有別於由單一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 系統資料類型組成的傳統別名資料類型。 使用能產生可驗證程式碼並由 Microsoft .NET Common Language Runtime (CLR) 支援的任何語言，即可定義 UDT。 這包括 Microsoft Visual C# 和 Visual Basic .NET。 資料會公開為 .NET Framework 類別或結構的欄位和屬性，而行為則是由類別或結構的方法所定義。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 中，UDT 可以用作資料表的資料行定義、[!INCLUDE[tsql](../../includes/tsql_md.md)] 批次中的變數，或是 [!INCLUDE[tsql](../../includes/tsql_md.md)] 函式或預存程序的引數。  
  
 如需使用者定義資料類型的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 線上叢書》中的＜使用和修改使用者定義類型的執行個體＞。  
  
## <a name="see-also"></a>另請參閱  
 [了解 JDBC Driver 資料類型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
