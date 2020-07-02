---
title: 使用 sql：最大深度設定遞迴深度關聯性
description: 瞭解如何使用 XQuery 中的 sql： max 深度注釋，在查詢具有遞迴關聯性的資料表時指定深度。
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- max-depth annotation
- XPath queries [SQLXML], recursive relationships
- depth in recursive relationships [SQLXML]
- annotated XSD schemas, recursive relationships
- relationships [SQLXML], recursive relationships
- self joins
- recursive relationships [SQLXML]
- recursion [SQLXML]
- sql:max-depth
- recursive joins [SQLXML]
ms.assetid: 0ffdd57d-dc30-44d9-a8a0-f21cadedb327
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d2d11ac386a822a6e6c0d6630fcc83ba2cf61486
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85764892"
---
# <a name="specifying-depth-in-recursive-relationships-by-using-sqlmax-depth"></a>使用 sql:max-depth 來指定遞迴關聯性的深度
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  在關聯式資料庫中，當某份資料表與本身具有關聯性時，它就稱為遞迴關聯性。 例如，在監督者-被監督者的關聯性中，儲存員工記錄的資料表會與本身具有關聯。 在此情況下，員工資料表在關聯性的一端扮演監督者的角色，而同一份資料表在另一端則扮演被監督者的角色。  
  
 對應結構描述可能包含遞迴關聯性，其中某個元素及其上階屬於相同的類型。  
  
## <a name="example-a"></a>範例 A  
 請考慮下列資料表：  
  
```  
Emp (EmployeeID, FirstName, LastName, ReportsTo)  
```  
  
 在這份資料表中，ReportsTo 資料行會儲存經理的員工識別碼。  
  
 假設您想要產生一種員工的 XML 階層，其中經理員工位於階層頂端，而且向經理報告的員工顯示在對應的階層中，如下列範例 XML 片段所示。 此片段顯示的內容是 employee 1 的*遞迴樹狀結構*。  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <Emp FirstName="Nancy" EmployeeID="1" LastName="Devolio">  
     <Emp FirstName="Andrew" EmployeeID="2" LastName="Fuller" />   
     <Emp FirstName="Janet" EmployeeID="3" LastName="Leverling">  
        <Emp FirstName="Margaret" EmployeeID="4" LastName="Peacock">  
          <Emp FirstName="Steven" EmployeeID="5" LastName="Devolio">  
...  
...  
</root>  
```  
  
 在這個片段中，員工 5 會向員工 4 報告、員工 4 會向員工 3 報告，而員工 3 和 2 會向員工 1 報告。  
  
 若要產生這種結果，您可以使用下列 XSD 結構描述並針對它指定 XPath 查詢。 架構會描述 **\<Emp>** EmployeeType 類型的元素，其中包含 **\<Emp>** 相同類型的子項目 EmployeeType。 這就是遞迴關聯性 (元素及其上階屬於相同的類型)。 此外，架構會使用 **\<sql:relationship>** 來描述監督員和被監督者之間的父子式關聯性。 請注意，在此中 **\<sql:relationship>** ，Emp 同時是父系和子資料工作表。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:dt="urn:schemas-microsoft-com:datatypes"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:appinfo>  
      <sql:relationship name="SupervisorSupervisee"  
                                  parent="Emp"  
                                  parent-key="EmployeeID"  
                                  child="Emp"  
                                  child-key="ReportsTo" />  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="Emp" type="EmployeeType"   
                          sql:relation="Emp"   
                          sql:key-fields="EmployeeID"   
                          sql:limit-field="ReportsTo" />  
  <xsd:complexType name="EmployeeType">  
    <xsd:sequence>  
      <xsd:element name="Emp" type="EmployeeType"   
                              sql:relation="Emp"   
                              sql:key-fields="EmployeeID"  
                              sql:relationship="SupervisorSupervisee"  
                              sql:max-depth="6" />  
    </xsd:sequence>   
    <xsd:attribute name="EmployeeID" type="xsd:ID" />  
    <xsd:attribute name="FirstName" type="xsd:string"/>  
    <xsd:attribute name="LastName" type="xsd:string"/>  
  </xsd:complexType>  
</xsd:schema>  
```  
  
 由於此關聯性是遞迴的，所以您需要某種方式來指定結構描述中的遞迴深度。 否則，結果將是無止盡的遞迴 (員工向員工報告，依此類推)。 [ **Sql：最大深度**] 注釋可讓您指定遞迴要前往的深度。 在此特定範例中，若要指定**sql：最大深度**的值，您必須知道管理階層在公司中的深度。  
  
> [!NOTE]  
>  此架構會指定**sql： limit 欄位**注釋，但不會指定**sql： limit-value**注釋。 這會將產生之階層中的最上層節點限制為不向任何人報告的員工  （上級為 Null）。指定**sql： limit-field** ，而不指定**sql： limit-value** （預設為 Null）注釋可完成此動作。 如果您想要產生的 XML 包含每個可能的報告樹狀目錄（資料表中每個員工的報告樹狀結構），請從架構中移除**sql： limit 欄位**注釋。  
  
> [!NOTE]  
>  下列程序會使用 tempdb 資料庫。  
  
#### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>針對結構描述測試範例 XPath 查詢  
  
1.  在虛擬根目錄指向的 tempdb 資料庫中建立名為 Emp 的範例資料表。  
  
    ```  
    USE tempdb  
    CREATE TABLE Emp (  
           EmployeeID int primary key,   
           FirstName  varchar(20),   
           LastName   varchar(20),   
           ReportsTo int)  
    ```  
  
2.  加入這個範例資料：  
  
    ```  
    INSERT INTO Emp values (1, 'Nancy', 'Devolio',NULL)  
    INSERT INTO Emp values (2, 'Andrew', 'Fuller',1)  
    INSERT INTO Emp values (3, 'Janet', 'Leverling',1)  
    INSERT INTO Emp values (4, 'Margaret', 'Peacock',3)  
    INSERT INTO Emp values (5, 'Steven', 'Devolio',4)  
    INSERT INTO Emp values (6, 'Nancy', 'Buchanan',5)  
    INSERT INTO Emp values (7, 'Michael', 'Suyama',6)  
    ```  
  
3.  複製上述的結構描述程式碼，並將其貼到文字檔中。 將檔案儲存為 maxDepth.xml。  
  
4.  複製下列範本，並將其貼到文字檔中。 將檔案儲存為 maxDepthT.xml，並放在與儲存 maxDepth.xml 相同的目錄中。 此範本中的查詢會傳回 Emp 資料表中的所有員工。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="maxDepth.xml">  
        /Emp  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     針對對應結構描述 (maxDepth.xml) 指定的目錄路徑，相對於儲存範本的目錄。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\MyDir\maxDepth.xml"  
    ```  
  
5.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。 如需詳細資訊，請參閱[使用 ADO 執行 SQLXML 4.0 查詢](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  

 以下是結果：  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <Emp FirstName="Nancy" EmployeeID="1" LastName="Devolio">  
  <Emp FirstName="Andrew" EmployeeID="2" LastName="Fuller" />   
    <Emp FirstName="Janet" EmployeeID="3" LastName="Leverling">  
      <Emp FirstName="Margaret" EmployeeID="4" LastName="Peacock">  
        <Emp FirstName="Steven" EmployeeID="5" LastName="Devolio">  
          <Emp FirstName="Nancy" EmployeeID="6" LastName="Buchanan">  
            <Emp FirstName="Michael" EmployeeID="7" LastName="Suyama" />   
          </Emp>  
        </Emp>  
      </Emp>  
    </Emp>  
  </Emp>  
</root>  
```  
  
> [!NOTE]  
>  若要在結果中產生不同的階層深度，請在架構中變更**sql： max 深度**注釋的值，然後在每次變更後再次執行範本。  
  
 在先前的架構中，所有 **\<Emp>** 元素都有完全相同的屬性集（[**員工**]、[ **FirstName**] 和 [ **LastName**]）。 下列架構已稍微修改，以針對向管理員報告的所有元素傳回額外的 [**上級**] 屬性 **\<Emp>** 。  
  
 例如，這個 XML 片段會顯示員工 1 的部屬：  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
<Emp FirstName="Nancy" EmployeeID="1" LastName="Devolio">  
  <Emp FirstName="Andrew" EmployeeID="2"   
       ReportsTo="1" LastName="Fuller" />   
  <Emp FirstName="Janet" EmployeeID="3"   
       ReportsTo="1" LastName="Leverling">  
...  
...  
```  
  
 這是已修訂的結構描述：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:dt="urn:schemas-microsoft-com:datatypes"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:documentation>  
      Customer-Order-Order Details Schema  
      Copyright 2000 Microsoft. All rights reserved.  
    </xsd:documentation>  
    <xsd:appinfo>  
      <sql:relationship name="SupervisorSupervisee"   
                  parent="Emp"  
                  parent-key="EmployeeID"  
                  child="Emp"  
                  child-key="ReportsTo" />  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="Emp"   
                   type="EmpType"   
                   sql:relation="Emp"   
                   sql:key-fields="EmployeeID"   
                   sql:limit-field="ReportsTo" />  
  <xsd:complexType name="EmpType">  
    <xsd:sequence>  
       <xsd:element name="Emp"   
                    type="EmpType"   
                    sql:relation="Emp"   
                    sql:key-fields="EmployeeID"  
                    sql:relationship="SupervisorSupervisee"  
                    sql:max-depth="6"/>  
    </xsd:sequence>   
    <xsd:attribute name="EmployeeID" type="xsd:int" />  
    <xsd:attribute name="FirstName" type="xsd:string"/>  
    <xsd:attribute name="LastName" type="xsd:string"/>  
    <xsd:attribute name="ReportsTo" type="xsd:int" />  
  </xsd:complexType>  
</xsd:schema>  
```  
  
## <a name="sqlmax-depth-annotation"></a>sql:max-depth 註解  
 在包含遞迴關聯性的結構描述中，遞迴的深度必須明確指定於結構描述中。 這是成功產生可傳回要求結果之對應 FOR XML EXPLICIT 查詢的必要條件。  
  
 在架構中使用**sql： max-depth**注釋，以指定架構中所述遞迴關聯性的遞迴深度。 「 **Sql：最大深度**」注釋的值是一個正整數（1到50），表示遞迴的數目：1的值會停止已指定「 **sql： max-深度**」注釋之元素的遞迴;值為2時，會從指定**sql： max 深度**的元素停止下一個層級的遞迴。以此類推。  
  
> [!NOTE]  
>  在基礎實作中，針對對應結構描述所指定的 XPath 查詢會轉換成 SELECT ... FOR XML EXPLICIT 查詢。 這個查詢會要求您指定有限的遞迴深度。 您為**sql：最大深度**指定的值愈高，產生的 FOR XML EXPLICIT 查詢就越大。 這可能會降低擷取速度。  
  
> [!NOTE]  
>  Updategram 和 XML 大量載入會忽略 max-depth 註解。 這表示，不論您針對 max-depth 指定的值為何，都會進行遞迴更新或插入。  
  
## <a name="specifying-sqlmax-depth-on-complex-elements"></a>在複雜元素上指定 sql:max-depth  
 您可以在任何複雜的 content 元素上指定**sql： max-depth**注釋。  
  
### <a name="recursive-elements"></a>遞迴元素  
 如果在遞迴關聯性中的父元素和子專案上指定了 **[sql： max-深度**]，則會優先使用父系上指定的 [ **sql：最大深度**] 注釋。 例如，在下列架構中，父系和子 employee 元素都指定了**sql： max 深度**注釋。 在此情況下，會優先使用在父元素（扮演監督員的角色）上指定的**sql： max-depth = 4** **\<Emp>** 。 已忽略子項目（扮演被監督者的角色）上指定的**sql： max 深度** **\<Emp>** 。  
  
#### <a name="example-b"></a>範例 B  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:dt="urn:schemas-microsoft-com:datatypes"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:appinfo>  
      <sql:relationship name="SupervisorSupervisee"  
                                  parent="Emp"  
                                  parent-key="EmployeeID"  
                                  child="Emp"  
                                  child-key="ReportsTo" />  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="Emp" type="EmployeeType"   
                          sql:relation="Emp"   
                          sql:key-fields="EmployeeID"   
                          sql:limit-field="ReportsTo"   
                          sql:max-depth="3" />  
  <xsd:complexType name="EmployeeType">  
    <xsd:sequence>  
      <xsd:element name="Emp" type="EmployeeType"   
                              sql:relation="Emp"   
                              sql:key-fields="EmployeeID"  
                              sql:relationship="SupervisorSupervisee"  
                              sql:max-depth="2" />  
    </xsd:sequence>   
    <xsd:attribute name="EmployeeID" type="xsd:ID" />  
    <xsd:attribute name="FirstName" type="xsd:string"/>  
    <xsd:attribute name="LastName" type="xsd:string"/>  
  </xsd:complexType>  
</xsd:schema>  
```  
  
 若要測試這個結構描述，請遵循本主題前面針對「範例 A」所提供的步驟。  
  
### <a name="nonrecursive-elements"></a>非遞迴元素  
 如果在架構中的元素上指定**sql： max-depth**注釋，而不會造成任何遞迴，則會忽略它。 在下列架構中， **\<Emp>** 元素是由子專案所組成，而 **\<Constant>** 該子項目又會有 **\<Emp>** 子專案。  
  
 在此架構中，會忽略在元素上指定的**sql： max 深度**注釋， **\<Constant>** 因為 **\<Emp>** 父元素和子專案之間沒有遞迴 **\<Constant>** 。 但是上階 **\<Emp>** 和子系之間有遞迴 **\<Emp>** 。 架構會在兩者上指定**sql： max 深度**注釋。 因此，在上階（在監督員角色中）指定的**sql： max 深度**注釋 **\<Emp>** 會優先使用。  
  
#### <a name="example-c"></a>範例 C  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:appinfo>  
      <sql:relationship name="SupervisorSupervisee"   
                  parent="Emp"   
                  child="Emp"   
                  parent-key="EmployeeID"   
                  child-key="ReportsTo"/>  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="Emp"   
               sql:relation="Emp"   
               type="EmpType"  
               sql:limit-field="ReportsTo"  
               sql:max-depth="1" />  
    <xsd:complexType name="EmpType" >  
      <xsd:sequence>  
       <xsd:element name="Constant"   
                    sql:is-constant="1"   
                    sql:max-depth="20" >  
         <xsd:complexType >  
           <xsd:sequence>  
            <xsd:element name="Emp"   
                         sql:relation="Emp" type="EmpType"  
                         sql:relationship="SupervisorSupervisee"   
                         sql:max-depth="3" />  
         </xsd:sequence>  
         </xsd:complexType>  
         </xsd:element>  
      </xsd:sequence>  
      <xsd:attribute name="EmployeeID" type="xsd:int" />  
    </xsd:complexType>  
</xsd:schema>  
```  
  
 若要測試這個結構描述，請遵循本主題前面針對「範例 A」所提供的步驟。  
  
## <a name="complex-types-derived-by-restriction"></a>限制所衍生的複雜類型  
 如果您有衍生的複雜類型 **\<restriction>** ，對應之基底複雜類型的元素就無法指定**sql： max 深度**注釋。 在這些情況下，可以將**sql： max 深度**注釋加入至衍生類型的元素。  
  
 另一方面，如果您有所衍生的複雜型別，則 **\<extension>** 對應之基底複雜型別的元素可以指定**sql： max 深度**注釋。  
  
 例如，下列 XSD 架構會產生錯誤，因為在基底類型上指定了**sql： max 深度**注釋。 從另一個型別衍生的型別不支援這個注釋 **\<restriction>** 。 若要修正這個問題，您必須變更架構，並在衍生類型的專案上指定**sql： max 深度**注釋。  
  
#### <a name="example-d"></a>範例 D  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:dt="urn:schemas-microsoft-com:datatypes"  
            xmlns:msdata="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:complexType name="CustomerBaseType">   
    <xsd:sequence>  
       <xsd:element name="CID" msdata:field="CustomerID" />  
       <xsd:element name="CompanyName"/>  
       <xsd:element name="Customers" msdata:max-depth="3">  
         <xsd:annotation>  
           <xsd:appinfo>  
             <msdata:relationship  
                     parent="Customers"  
                     parent-key="CustomerID"  
                     child-key="CustomerID"  
                     child="Customers" />  
           </xsd:appinfo>  
         </xsd:annotation>  
       </xsd:element>  
    </xsd:sequence>  
  </xsd:complexType>  
  <xsd:element name="Customers" type="CustomerType"/>  
  <xsd:complexType name="CustomerType">  
    <xsd:complexContent>  
       <xsd:restriction base="CustomerBaseType">  
          <xsd:sequence>  
            <xsd:element name="CID"   
                         type="xsd:string"/>  
            <xsd:element name="CompanyName"   
                         type="xsd:string"  
                         msdata:field="CName" />  
            <xsd:element name="Customers"   
                         type="CustomerType" />  
          </xsd:sequence>  
       </xsd:restriction>  
    </xsd:complexContent>  
  </xsd:complexType>  
</xsd:schema>   
```  
  
 在架構中，會在**CustomerBaseType**複雜類型上指定**sql： max 深度**。 此架構也會指定 **\<Customer>** **CustomerType**類型的元素，此專案衍生自**CustomerBaseType**。 在這類架構上指定的 XPath 查詢會產生錯誤，因為在限制基底類型中定義的元素上不支援**sql： max 深度**。  
  
## <a name="schemas-with-a-deep-hierarchy"></a>具有深度階層的結構描述  
 您可能會擁有一個包括深度階層的結構描述，其中某個元素包含子元素，而後者又包含其他子元素，依此類推。 如果在這類架構中指定的**sql： max 深度**注釋產生的 XML 檔中包含超過500層級的階層（具有層級1的最上層元素、在層級2的子系，依此類推），則會傳回錯誤。  
  
  
