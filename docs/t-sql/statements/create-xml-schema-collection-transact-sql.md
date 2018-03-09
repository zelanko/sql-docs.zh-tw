---
title: "建立 XML 結構描述集合 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 11/25/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE XML SCHEMA COLLECTION
- CREATE_XML_SCHEMA_COLLECTION_TSQL
- CREATE XML SCHEMA
- CREATE_XML_SCHEMA_TSQL
- COLLECTION
- COLLECTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE XML SCHEMA COLLECTION statement
- importing schema components
- schema collections [SQL Server], creating
- multiple schema namespaces
- XML schema collections [SQL Server], creating
ms.assetid: 350684e8-b3f6-4b58-9dbc-0f05cc776ebb
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6941e48f344db354902d6475382fa39e5541bd9e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="create-xml-schema-collection-transact-sql"></a>CREATE XML SCHEMA COLLECTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  將結構描述元件匯入資料庫中。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
CREATE XML SCHEMA COLLECTION [ <relational_schema>. ]sql_identifier AS Expression  
```  
  
## <a name="arguments"></a>引數  
 *relational_schema*  
 識別關聯式結構描述名稱。 若未指定，則會假設使用預設的關聯式結構描述。  
  
 *sql_identifier*  
 這是 XML 結構描述集合的 SQL 識別碼。  
  
 *[運算式]*  
 這是字串常數或純量變數。 是**varchar**， **varbinary**， **nvarchar**，或**xml**型別。  
  
## <a name="remarks"></a>備註  
 您也可以將新的命名空間加入至集合，或使用，將新元件加入至集合中的現有命名空間[ALTER XML SCHEMA COLLECTION](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md)。  
  
 若要移除集合，請使用[DROP XML SCHEMA COLLECTION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-xml-schema-collection-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 若要建立 XML SCHEMA COLLECTION，至少需要下列權限集合之一：  
  
-   伺服器的 CONTROL 權限  
  
-   伺服器的 ALTER ANY DATABASE 權限  
  
-   資料庫的 ALTER 權限  
  
-   資料庫的 CONTROL 權限  
  
-   資料庫的 ALTER ANY SCHEMA 權限和 CREATE XML SCHEMA COLLECTION 權限  
  
-   關聯式結構描述的 ALTER 或 CONTROL 權限和資料庫的 CREATE XML SCHEMA COLLECTION 權限  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-xml-schema-collection-in-the-database"></a>A. 在資料庫中建立 XML 結構描述集合  
 下列範例會建立 XML 結構描述集合 `ManuInstructionsSchemaCollection`。 這個集合只有一個結構描述命名空間。  
  
```  
-- Create a sample database in which to load the XML schema collection.  
CREATE DATABASE SampleDB;  
GO  
USE SampleDB;  
GO  
CREATE XML SCHEMA COLLECTION ManuInstructionsSchemaCollection AS  
N'<?xml version="1.0" encoding="UTF-16"?>  
<xsd:schema targetNamespace="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"   
   xmlns          ="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"   
   elementFormDefault="qualified"   
   attributeFormDefault="unqualified"  
   xmlns:xsd="http://www.w3.org/2001/XMLSchema" >  
  
    <xsd:complexType name="StepType" mixed="true" >  
        <xsd:choice  minOccurs="0" maxOccurs="unbounded" >   
            <xsd:element name="tool" type="xsd:string" />  
            <xsd:element name="material" type="xsd:string" />  
            <xsd:element name="blueprint" type="xsd:string" />  
            <xsd:element name="specs" type="xsd:string" />  
            <xsd:element name="diag" type="xsd:string" />  
        </xsd:choice>   
    </xsd:complexType>  
  
    <xsd:element  name="root">  
        <xsd:complexType mixed="true">  
            <xsd:sequence>  
                <xsd:element name="Location" minOccurs="1" maxOccurs="unbounded">  
                    <xsd:complexType mixed="true">  
                        <xsd:sequence>  
                            <xsd:element name="step" type="StepType" minOccurs="1" maxOccurs="unbounded" />  
                        </xsd:sequence>  
                        <xsd:attribute name="LocationID" type="xsd:integer" use="required"/>  
                        <xsd:attribute name="SetupHours" type="xsd:decimal" use="optional"/>  
                        <xsd:attribute name="MachineHours" type="xsd:decimal" use="optional"/>  
                        <xsd:attribute name="LaborHours" type="xsd:decimal" use="optional"/>  
                        <xsd:attribute name="LotSize" type="xsd:decimal" use="optional"/>  
                    </xsd:complexType>  
                </xsd:element>  
            </xsd:sequence>  
        </xsd:complexType>  
    </xsd:element>  
</xsd:schema>' ;  
GO  
-- Verify - list of collections in the database.  
SELECT *  
FROM sys.xml_schema_collections;  
-- Verify - list of namespaces in the database.  
SELECT name  
FROM sys.xml_schema_namespaces;  
  
-- Use it. Create a typed xml variable. Note collection name specified.  
DECLARE @x xml (ManuInstructionsSchemaCollection);  
GO  
--Or create a typed xml column.  
CREATE TABLE T (  
        i int primary key,   
        x xml (ManuInstructionsSchemaCollection));  
GO  
-- Clean up  
DROP TABLE T;  
GO  
DROP XML SCHEMA COLLECTION ManuInstructionsSchemaCollection;  
Go  
USE master;  
GO  
DROP DATABASE SampleDB;  
```  
  
 或者，您可以指派結構描述集合到變數中，並在 `CREATE XML SCHEMA COLLECTION` 陳述式中指定變數，如下所示：  
  
```  
DECLARE @MySchemaCollection nvarchar(max)  
Set @MySchemaCollection  = N' copy the schema collection here'  
CREATE XML SCHEMA COLLECTION MyCollection AS @MySchemaCollection   
```  
  
 範例中的變數屬於 `nvarchar(max)` 類型。 變數也可以是**xml**資料類型，在此情況下，它會隱含地轉換成字串。  
  
 如需詳細資訊，請參閱 [檢視儲存的 XML 結構描述集合](../../relational-databases/xml/view-a-stored-xml-schema-collection.md)。  
  
 您可能會儲存在結構描述集合**xml**類型資料行。 在這個情況下，若要建立 XML 結構描述集合，請執行下列動作：  
  
1.  使用 SELECT 陳述式來擷取資料行的結構描述集合，並將它指派給變數的**xml**型別，或**varchar**型別。  
  
2.  在 CREATE XML SCHEMA COLLECTION 陳述式中指定變數名稱。  
  
 CREATE XML SCHEMA COLLECTION 只會儲存 SQL Server 暸解的結構描述元件；XML 結構描述中的所有項目都不會儲存在資料庫中。 因此，如果您想要 XML 結構描述集合回復成和原來所提供的完全相同，建議您將 XML 結構描述儲存於資料庫資料行或電腦的其他資料夾中。  
  
### <a name="b-specifying-multiple-schema-namespaces-in-a-schema-collection"></a>B. 在結構描述集合中指定多個結構描述命名空間  
 建立 XML 結構描述集合時，您也可以指定多個 XML 結構描述。 例如：  
  
```  
CREATE XML SCHEMA COLLECTION MyCollection AS N'  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
<!-- Contents of schema here -->    
</xsd:schema>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
<!-- Contents of schema here -->  
</xsd:schema>';  
```  
  
 下列範例會建立包括兩個 XML 結構描述命名空間的 XML 結構描述集合 `ProductDescriptionSchemaCollection`。  
  
```  
CREATE XML SCHEMA COLLECTION ProductDescriptionSchemaCollection AS   
'<xsd:schema targetNamespace="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"  
    xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"   
    elementFormDefault="qualified"   
    xmlns:xsd="http://www.w3.org/2001/XMLSchema" >  
    <xsd:element name="Warranty"  >  
        <xsd:complexType>  
            <xsd:sequence>  
                <xsd:element name="WarrantyPeriod" type="xsd:string"  />  
                <xsd:element name="Description" type="xsd:string"  />  
            </xsd:sequence>  
        </xsd:complexType>  
    </xsd:element>  
</xsd:schema>  
 <xs:schema targetNamespace="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
    xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
    elementFormDefault="qualified"   
    xmlns:mstns="http://tempuri.org/XMLSchema.xsd"   
    xmlns:xs="http://www.w3.org/2001/XMLSchema"  
    xmlns:wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain" >  
    <xs:import   
namespace="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain" />  
    <xs:element name="ProductDescription" type="ProductDescription" />  
        <xs:complexType name="ProductDescription">  
            <xs:sequence>  
                <xs:element name="Summary" type="Summary" minOccurs="0" />  
            </xs:sequence>  
            <xs:attribute name="ProductModelID" type="xs:string" />  
            <xs:attribute name="ProductModelName" type="xs:string" />  
        </xs:complexType>  
        <xs:complexType name="Summary" mixed="true" >  
            <xs:sequence>  
                <xs:any processContents="skip" namespace="http://www.w3.org/1999/xhtml" minOccurs="0" maxOccurs="unbounded" />  
            </xs:sequence>  
        </xs:complexType>  
</xs:schema>'  
;  
GO -- Clean up  
DROP XML SCHEMA COLLECTION ProductDescriptionSchemaCollection;  
GO  
```  
  
### <a name="c-importing-a-schema-that-does-not-specify-a-target-namespace"></a>C. 匯入不指定目標命名空間的結構描述  
 如果結構描述不包含**targetNamespace**屬性匯入的集合，其元件會與空字串目標命名空間相關聯，如下列範例所示。 請注意，不對匯入集合之一或多個結構描述進行關聯，會造成多個結構描述元件 (可能無關) 與預設空字串命名空間相關聯。  
  
```  
-- Create a collection that contains a schema with no target namespace.  
CREATE XML SCHEMA COLLECTION MySampleCollection AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  xmlns:ns="http://ns">  
<element name="e" type="dateTime"/>  
</schema>';  
go  
-- Query will return the names of all the collections that   
--contain a schema with no target namespace.  
SELECT sys.xml_schema_collections.name   
FROM   sys.xml_schema_collections   
JOIN   sys.xml_schema_namespaces   
ON     sys.xml_schema_collections.xml_collection_id =   
       sys.xml_schema_namespaces.xml_collection_id   
WHERE  sys.xml_schema_namespaces.name='';  
```  
  
### <a name="d-using-an-xml-schema-collection-and-batches"></a>D. 使用 XML 結構描述集合和批次  
 在建立結構描述集合所在的同一批次中，不可以參考該結構描述集合。 如果您嘗試在建立集合之同一批次中參考該集合，您會看到錯誤訊息，告訴您集合不存在。 下列範例是有效的；然而，如果您移除 `GO` 而因此嘗試參考 XML 結構描述集合在同一批次中輸入 `xml` 變數，則會傳回錯誤。  
  
```  
CREATE XML SCHEMA COLLECTION mySC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" type="string"/>  
</schema>  
';  
GO  
CREATE TABLE T (Col1 xml (mySC));  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER XML SCHEMA COLLECTION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md)   
 [卸除 XML 結構描述集合 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-xml-schema-collection-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [比較具類型的 XML 與不具類型的 XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [卸除 XML 結構描述集合 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-xml-schema-collection-transact-sql.md)   
 [伺服器上 XML 結構描述集合的需求與限制](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
