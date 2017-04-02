---
title: "參考內建 XML 結構描述集合 (sys) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "sys XML 結構描述集合 [SQL Server]"
  - "結構描述集合 [SQL Server], 預先定義"
  - "預先定義的 XML 結構描述集合 [SQL Server]"
  - "XML 結構描述集合 [SQL Server], 預先定義"
  - "內建 XML 結構描述集合 [SQL Server]"
ms.assetid: 1e118303-5df0-4ee4-bd8d-14ced7544144
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 18
---
# 參考內建 XML 結構描述集合 (sys)
  您建立的每一個資料庫，在 **sys** 關聯式結構描述中，都有一個預先定義的 **sys** XML 結構描述集合。 此集合會保留這些預先定義的結構描述，所以從其他使用者建立的任何 XML 結構描述集合都能存取這些結構描述。 這些預先定義的結構描述中使用的前置詞在 XQuery 中是有意義的。 只有 **xml** 是保留的前置詞。  
  
```  
xml = http://www.w3.org/XML/1998/namespace  
xs = http://www.w3.org/2001/XMLSchema  
xsi = http://www.w3.org/2001/XMLSchema-instance  
fn = http://www.w3.org/2004/07/xpath-functions  
sqltypes = http://schemas.microsoft.com/sqlserver/2004/sqltypes  
xdt = http://www.w3.org/2004/07/xpath-datatypes  
(no prefix) = urn:schemas-microsoft-com:xml-sql  
(no prefix) = http://schemas.microsoft.com/sqlserver/2004/SOAP  
```  
  
 請注意，**sqltypes** 命名空間包含的元件可以從任何使用者建立的 XML 結構描述集合參考。 您可以從 **Microsoft 網站** 下載 [sqltypes](http://go.microsoft.com/fwlink/?linkid=31850)結構描述。 內建的元件包括下列項目：  
  
-   XSD 類型  
  
-   XML 屬性 **lang**, **base**及 **space**  
  
-   **sqltypes** 命名空間的元件  
  
 下列查詢會傳回可以從使用者建立之 XML 結構描述集合參考的內建元件：  
  
```  
SELECT C.name, N.name, C.symbol_space_desc from sys.xml_schema_components C join sys.xml_schema_namespaces N  
on ((C.xml_namespace_id = N.xml_namespace_id) AND (C.xml_collection_id = N.xml_collection_id))  
join sys.xml_schema_collections SC  
on SC.xml_collection_id = C.xml_collection_id  
where ((C.xml_collection_id = 1) AND (C.name is not null) AND (C.scoping_xml_component_id is null)   
AND (SC.schema_id = 4))  
GO  
```  
  
 下列範例顯示這些元件在使用者結構描述中的參考方式。 `CREATE XML SCHEMA COLLECTION` 建立 XML 結構描述集合，其參考 `varchar` 命名空間中所定義的 `sqltypes` 類型。 此範例也會參考 `lang` 命名空間中定義的 `xml` 屬性。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema   
   xmlns="http://www.w3.org/2001/XMLSchema"   
   targetNamespace="myNS"  
   xmlns:ns="myNS"  
   xmlns:s="http://schemas.microsoft.com/sqlserver/2004/sqltypes" >   
   <import namespace="http://www.w3.org/XML/1998/namespace"/>  
   <import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
   <element name="root">  
      <complexType>  
          <sequence>  
             <element name="a" type="string"/>  
             <element name="b" type="string"/>  
             <!-- varchar type is defined in the sys.sys collection and   
                  can be referenced in any user-defined schema -->  
             <element name="c" type="s:varchar"/>  
          </sequence>  
          <attribute name="att" type="int"/>  
          <!-- xml:lang attribute is defined in the sys.sys collection   
               and can be referenced in any user-defined schema -->  
          <attribute ref="xml:lang"/>  
      </complexType>  
    </element>  
 </schema>'  
GO  
 -- Cleanup  
DROP xml schema collection SC   
GO  
```  
  
 您應該注意下列各項：  
  
-   您不能在任何使用者自訂 XML 結構描述集合中，使用這些命名空間來修改 XML 結構描述。 例如，下列的 XML 結構描述集合會失敗，因為它把元件加入到 `sqltypes` 保護的命名空間：  
  
    ```  
    CREATE XML SCHEMA COLLECTION SC AS '  
    <schema xmlns="http://www.w3.org/2001/XMLSchema"   
    targetNamespace    
        ="http://schemas.microsoft.com/sqlserver/2004/sqltypes" >   
          <element name="root" type="string"/>  
    </schema>'  
    GO  
    ```  
  
-   您不能使用 `sys` XML 結構描述集合來鍵入 `xml` 資料行、變數或參數。 例如，下列程式碼會傳回錯誤：  
  
    ```  
    DECLARE @x xml (sys.sys)  
    ```  
  
-   不支援這些內建結構描述的序列化。 例如，下列程式碼會傳回錯誤：  
  
    ```  
    SELECT XML_SCHEMA_NAMESPACE(N'sys',N'sys')  
    GO  
    ```  
  
 下列程式碼是另一個範例，在此您將建立一個 XML 結構描述集合，此結構描述集合會使用 `varchar` 命名空間中定義的 `sqltypes` 類型：  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"   
        targetNamespace="myNS" xmlns:ns="myNS"  
        xmlns:s="http://schemas.microsoft.com/sqlserver/2004/sqltypes">  
   <import     
     namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
      <simpleType name="myType">  
            <restriction base="s:varchar">  
                  <maxLength value="20"/>  
            </restriction>  
      </simpleType>  
      <element name="root" type="ns:myType"/>  
</schema>'  
go  
```  
  
 如下所示，您可以建立 `XML` 類型的變數，將 XML 執行個體指派給這個變數，並確認 <`root`> 元素類型的值是 `varchar` 類型。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xmlns="myNS">My data</root>'  
SELECT @var.query('declare namespace sqltypes = "http://schemas.microsoft.com/sqlserver/2004/sqltypes";  
declare namespace ns="myNS";   
data(/ns:root[1]) instance of sqltypes:varchar?')  
GO  
```  
  
 `instance of sqltypes:varchar?` 運算式會傳回 TRUE，因為 <`root`> 元素值的類型是由 **varchar** 衍生而來 (根據與 `@var` 變數相關的結構描述而衍生)。  
  
## 另請參閱  
 [XML 結構描述集合 &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  