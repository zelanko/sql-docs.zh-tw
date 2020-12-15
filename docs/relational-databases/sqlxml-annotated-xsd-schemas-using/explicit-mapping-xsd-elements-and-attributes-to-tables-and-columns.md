---
title: '資料表/資料行的自訂 XSD 對應 (SQLXML) '
description: 瞭解如何在 SQLXML XPath 查詢中，建立 XSD 架構的元素和屬性與關係資料庫的資料表和資料行之間的自訂對應。
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- explicit schema mapping [SQLXML]
- XPath queries [SQLXML], annotated XSD schemas in queries
- sql:field
- row mapping [SQLXML]
- attribute mapping [SQLXML], explicit mapping
- field annotation
- XSD schemas [SQLXML], mapping attributes and elements
- names [SQLXML]
- relation annotation
- table/view mapping [SQLXML], explicit mapping
- sql:relation
- mapping schema [SQLXML], explicit mapping
- annotated XSD schemas, mapping attributes and elements
- column mapping [SQLXML]
- element mapping [SQLXML], explicit mapping
- table mapping [SQLXML], explicit mapping
- element/attribute mapping [SQLXML]
ms.assetid: 7a5ebeb6-7322-4141-a307-ebcf95976146
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 988a15524f4d0fdbdd3174ba1017dfd85562e3a6
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97415838"
---
# <a name="custom-xsd-mappings-to-tablescolumns-sqlxml"></a>資料表/資料行的自訂 XSD 對應 (SQLXML) 
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  使用 XSD 結構描述提供關聯式資料庫的 XML 檢視表時，必須將結構描述的元素但屬性對應到資料庫的資料表和資料行。 資料庫資料表/檢視表中的資料列將會對應到 XML 文件中的元素。 資料庫中的資料行值會對應到屬性或元素。  
  
 針對註解式 XSD 結構描述指定 XPath 查詢時，結構描述中元素和屬性的資料會從所對應的資料表和資料行對應。 若要從資料庫取得單一值，在 XSD 結構描述中指定的對應必須同時擁有關聯和欄位規格。 如果元素/屬性的名稱與其所對應的資料表/視圖或資料行名稱不同，則會使用 **sql： relation** 和 **sql： field** 批註來指定 XML 檔中的專案或屬性與資料表 (view) 或資料庫中的資料行之間的對應。  
  
## <a name="sql-relation"></a>sql-relation  
 系統會加入 **sql：關聯** 注釋，以將 XSD 架構中的 XML 節點對應至資料庫資料表。 資料表 (view) 的名稱會指定為 **sql： relation** 注釋的值。  
  
 在元素上指定 **sql：關聯** 時，這個批註的範圍會套用到該專案的複雜類型定義中所描述的所有屬性和子項目，因此提供撰寫批註的快捷方式。  
  
 當中有效的識別碼在 XML 中無效時， **sql：關聯** 注釋也相當有用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 例如，"Order Details" 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中是有效的資料表名稱，但是在 XML 中是無效的。 在這種情況下，您可以使用 **sql： relation** 注釋來指定對應，例如：  
  
```  
<xsd:element name="OD" sql:relation="[Order Details]">  
```  
  
## <a name="sql-field"></a>sql-field  
 **Sql 欄位** 批註會將元素或屬性對應到資料庫資料行。 加入 **sql： field** 注釋，以將架構中的 XML 節點對應至資料庫資料行。 您無法在空白內容元素上指定 **sql： field** 。  
  
## <a name="examples"></a>範例  
 若要使用下列範例建立工作範例，您必須符合某些需求。 如需詳細資訊，請參閱 [執行 SQLXML 範例的需求](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-specifying-the-sqlrelation-and-sqlfield-annotations"></a>A. 指定 sql:relation 和 sql:field 註解  
 在此範例中，XSD 架構是由 **\<Contact>** 具有 **\<FName>** 和 **\<LName>** 子項目和 **ContactID** 屬性之複雜類型的元素所組成。  
  
 **Sql： relation** 注釋會將專案對應 **\<Contact>** 至 AdventureWorks 資料庫中的 Contact 資料表。 **Sql： field** 批註會將 **\<FName>** 元素對應到 FirstName 資料行，並將專案對應 **\<LName>** 至 LastName 資料行。  
  
 未針對 **ContactID** 屬性指定批註。 這會導致將屬性預設對應到具有相同名稱的資料行。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Contact" sql:relation="Person.Contact" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="FName"  
                     sql:field="FirstName"   
                     type="xsd:string" />   
        <xsd:element name="LName"    
                     sql:field="LastName"    
                     type="xsd:string" />  
     </xsd:sequence>  
        <xsd:attribute name="ContactID"   
                       type="xsd:integer" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>針對結構描述測試範例 XPath 查詢  
  
1.  複製上述的結構描述程式碼，並將其貼到文字檔中。 將檔案儲存為 MySchema-annotated.xml。  
  
2.  複製下列範本，並將其貼到文字檔中。 將檔案儲存為 MySchema-annotatedT.xml 並放在與儲存 MySchema-annotated.xml 相同的目錄中。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="MySchema-annotated.xml">  
        /Contact  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     針對對應結構描述 (MySchema-annotated.xml) 指定的目錄路徑，與儲存範本之目錄相關。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\SqlXmlTest\MySchema-annotated.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱 [使用 ADO 執行 SQLXML 查詢](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 部分結果集如下：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
 <Contact ContactID="1">   
    <FName>Gustavo</FName>   
    <LName>Achong</LName>   
 </Contact>   
  .....  
</ROOT>  
```  
  
  
