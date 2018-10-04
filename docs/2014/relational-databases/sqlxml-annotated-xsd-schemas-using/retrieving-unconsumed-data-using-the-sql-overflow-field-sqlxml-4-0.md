---
title: '擷取未耗用資料使用 sql: overflow-field-欄位 (SQLXML 4.0) |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- unconsumed data
- storing unconsumed data
- retrieving unconsumed data
- annotated XSD schemas, unconsumed data
- overflow data [SQLXML]
- sql:overflow-field
ms.assetid: 8526998d-b47d-4a32-8dc2-7f50a8d11097
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d07153f80cc1b6dfdc8383e33a8668b63364ad8a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48119508"
---
# <a name="retrieving-unconsumed-data-using-the-sqloverflow-field-sqlxml-40"></a>使用 sql:overflow-field 擷取未耗用的資料 (SQLXML 4.0)
  當記錄使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] OPENXML 函數，從 XML 文件的資料庫中插入，可以將來源 XML 文件中所有未耗用的資料儲存在資料行中。 當您使用註解式結構描述擷取資料庫中的資料時，您可以指定 `sql:overflow-field` 屬性來識別儲存溢位資料之資料表中的資料行。 `sql:overflow-field`屬性可以在上指定**\<項目 >**。  
  
 然後以下列方式擷取此資料：  
  
-   儲存在溢位資料行中的屬性會加入到包含 `sql:overflow-field` 註解的元素中。  
  
-   儲存在資料庫之溢位資料行中的子元素及其下階會當做在結構描述中明確指定之內容之後的子元素加入  (不會保留任何順序)。  
  
## <a name="examples"></a>範例  
 若要使用下列範例建立工作範例，您必須符合某些需求。 如需詳細資訊，請參閱 <<c0> [ 如需執行 SQLXML 範例的需求](../sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-specifying-sqloverflow-field-for-an-element"></a>A. 針對元素指定 sql:overflow-field  
 此範例假設已經執行下列指令碼，因此名為 Customers2 的資料表存在於 tempdb 資料庫中：  
  
```  
USE tempdb  
CREATE TABLE Customers2 (  
CustomerID       VARCHAR(10),   
ContactName    VARCHAR(30),   
AddressOverflow    NVARCHAR(500))  
  
GO  
INSERT INTO Customers2 VALUES (  
'ALFKI',   
'Joe',  
'<Address>  
  <Address1>Maple St.</Address1>  
  <Address2>Apt. E105</Address2>  
  <City>Seattle</City>  
  <State>WA</State>  
  <Zip>98147</Zip>  
 </Address>')  
GO  
```  
  
 此外，您必須建立 tempdb 資料庫的虛擬目錄，以及名稱為 "template" 之 `template` 類型的範本虛擬名稱。  
  
 在下列範例中，對應結構描述會擷取儲存在 Customers2 資料表之 AddressOverflow 資料行中的未耗用資料：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:element name="Customers2" sql:overflow-field="AddressOverflow" >  
    <xsd:complexType>  
      <xsd:attribute name="CustomerID"  type="xsd:integer"/>  
      <xsd:attribute name="ContactName"  type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>針對結構描述測試範例 XPath 查詢  
  
1.  複製上述的結構描述程式碼，並將其貼到文字檔中。 將檔案儲存為 Overflow.xml。  
  
2.  複製下列範本，並將其貼到文字檔中。 將檔案儲存為 OverflowT.xml 並放在與儲存 Overflow.xml 相同的目錄中。 範本中的查詢會選取 Customers2 資料表中的記錄。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="Overflow.xml">  
            /Customers2  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     針對對應結構描述 (Overflow.xml) 指定的目錄路徑相對於儲存範本的目錄。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\SqlXmlTest\Overflow.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱 <<c0> [ 使用 ADO 執行 SQLXML 4.0 查詢](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 以下為結果集：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customers2 CustomerID="ALFKI" ContactName="Joe">  
    <Address1>Maple St.</Address1>   
    <Address2>Apt. E105</Address2>   
    <City>Seattle</City>   
    <State>WA</State>   
    <Zip>98147</Zip>   
  </Customers2>  
</ROOT>  
```  
  
  
