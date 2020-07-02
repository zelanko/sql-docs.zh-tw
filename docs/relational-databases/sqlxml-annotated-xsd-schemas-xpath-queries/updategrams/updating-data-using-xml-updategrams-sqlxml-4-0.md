---
title: 使用 XML Updategram 更新資料（SQLXML）
description: 瞭解如何使用 SQLXML 4.0 中的 XML updategram 來更新現有資料。
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- IDREF type attribute [SQLXML]
- before attribute
- <sync> block
- <after> block
- id attribute
- <before> block
- updg:after attribute
- mapping-schema attribute
- IDREFS type attribute [SQLXML]
- updg:id attribute
- multiple record updates
- after attribute
- updategrams [SQLXML], updating data
- updg:before attribute
- record updates [SQLXML]
ms.assetid: 90ef8a33-5ae3-4984-8259-608d2f1d727f
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 01fd8e99d6eb770c2f5680ead1e2c4d9b9ec98b8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85733660"
---
# <a name="updating-data-using-xml-updategrams-sqlxml-40"></a>使用 XML Updategram 更新資料 (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  當您更新現有的資料時，您必須同時指定 **\<before>** 和 **\<after>** 區塊。 和區塊中指定的元素會 **\<before>** **\<after>** 描述所需的變更。 Updategram 會使用區塊中指定的元素， **\<before>** 來識別資料庫中的現有記錄。 區塊中的對應元素 **\<after>** 會指出在執行更新作業之後，記錄的外觀。 在此資訊中，updategram 會建立符合區塊的 SQL 語句 **\<after>** 。 接著，Updategram 會使用此陳述式來更新資料庫。  
  
 下列是更新作業的 Updategram 格式：  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync [mapping-schema="SampleSchema.xml"]  >  
   <updg:before>  
      <ElementName [updg:id="value"] .../>  
      [<ElementName [updg:id="value"] .../> ... ]  
   </updg:before>  
   <updg:after>  
      <ElementName [updg:id="value"] ... />  
      [<ElementName [updg:id="value"] .../> ...]  
   </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
 **\<updg:before>**  
 區塊中的元素 **\<before>** 可識別資料庫資料表中的現有記錄。  
  
 **\<updg:after>**  
 區塊中的元素 **\<after>** 會描述在套用更新之後，區塊中指定的記錄 **\<before>** 應如何查看。  
  
 **對應架構**屬性會識別 updategram 所使用的對應架構。 如果 updategram 指定對應架構，則在和區塊中指定的元素和屬性 **\<before>** 名稱 **\<after>** 必須符合架構中的名稱。 對應的結構描述會將這些元素或屬性名稱對應到資料庫資料表和資料行名稱。  
  
 如果 Updategram 沒有指定結構描述，Updategram 會使用預設的對應。 在預設的對應中， **\<ElementName>** updategram 中指定的會對應至資料庫資料表，而子項目或屬性則會對應至資料庫資料行。  
  
 區塊中的元素 **\<before>** 必須與資料庫中只有一個資料表資料列相符。 如果元素符合多個資料表資料列，或不符合任何資料表資料列，則 updategram 會傳回錯誤並取消整個 **\<sync>** 區塊。  
  
 Updategram 可以包含多個 **\<sync>** 區塊。 **\<sync>** 會將每個區塊視為一筆交易。 每個 **\<sync>** 區塊可以有多個 **\<before>** 和 **\<after>** 區塊。 例如，如果您要更新兩個現有的記錄，您可以指定兩個 **\<before>** 和 **\<after>** 配對，每個更新的記錄一個。  
  
## <a name="using-the-updgid-attribute"></a>使用 updg:id 屬性  
 在和區塊中指定多個元素時 **\<before>** **\<after>** ，請使用**updg： id**屬性來標記 **\<before>** 和區塊中的 **\<after>** 資料列。 處理邏輯會使用這項資訊來判斷區塊中的哪個記錄 **\<before>** 與區塊中的哪一筆記錄 **\<after>** 。  
  
 如果下列其中一項存在，則不需要**updg： id**屬性（雖然建議）：  
  
-   指定之對應架構中的專案已定義**sql：索引鍵欄位**屬性。  
  
-   在 Updategram 中有一或多個針對索引鍵欄位提供的特定值。  
  
 如果是這種情況，updategram 會使用**sql：索引鍵欄位**中所指定的索引鍵資料行來配對和區塊中的 **\<before>** 元素 **\<after>** 。  
  
 如果對應架構未識別索引鍵資料行（藉由使用**sql：索引鍵-欄位**），或 updategram 正在更新索引鍵資料行值，則您必須指定**updg： id**。  
  
 在和區塊中識別的記錄 **\<before>** **\<after>** 不一定要有相同的順序。 **Updg： id**屬性會強制在和區塊中指定的元素之間產生關聯 **\<before>** **\<after>** 。  
  
 如果您在區塊中指定一個元素， **\<before>** 而且在區塊中只有一個對應的元素 **\<after>** ，則不需要使用**updg： id** 。 不過，建議您仍要指定**updg： id** ，以避免混淆。  
  
## <a name="examples"></a>範例  
 使用 Updategram 範例之前，請注意下列事項：  
  
-   大部分的範例都會使用預設對應 (也就是說，Updategram 中不會指定任何對應結構描述)。 如需使用對應架構之 updategram 的更多範例，請參閱[在 Updategram 中指定批註式對應架構 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)。  
  
-   大部分的範例會使用 AdventureWorks 範例資料庫。 所有的更新都會套用到此資料庫內的資料表。 您可以還原 AdventureWorks 資料庫。  
  
### <a name="a-updating-a-record"></a>A. 更新記錄  
 下列 Updategram 會在 AdventureWorks 資料庫的 Person.Contact 資料表中，將員工姓氏更新為 Fuller。 Updategram 沒有指定任何對應結構描述，因此，Updategam 會使用預設的對應。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
   <Person.Contact ContactID="1" />  
</updg:before>  
<updg:after>  
   <Person.Contact LastName="Abel-Achong" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
 區塊中所述的記錄 **\<before>** 代表資料庫中的目前記錄。 Updategram 會使用區塊中指定的所有資料行值 **\<before>** 來搜尋記錄。 在此 updategram 中， **\<before>** 區塊僅提供 ContactID 資料行，因此，updategram 只會使用值來搜尋記錄。 如果您要將 LastName 值加入到此區塊中，Updategram 會同時使用 ContactID 和 LastName 值進行搜尋。  
  
 在此 updategram 中， **\<after>** 區塊只會提供 LastName 資料行值，因為這是唯一變更的值。  
  
##### <a name="to-test-the-updategram"></a>若要測試 Updategram  
  
1.  複製上述的 updategram 範本，並將其貼到文字檔中。 將檔案儲存為 UpdateLastName.xml。  
  
2.  建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行 Updategram。  

     如需詳細資訊，請參閱[使用 ADO 執行 SQLXML 4.0 查詢](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
### <a name="b-updating-multiple-records-by-using-the-updgid-attribute"></a>B. 使用 updg:id 屬性更新多筆記錄  
 在此範例中，updategram 會在 AdventureWorks 資料庫的 HumanResources.Shift 資料表上執行兩個變更：  
  
-   它會將早上七點起的原始日班名稱從 "Day" 變更為 "Early Morning"。  
  
-   它會插入名稱為 "Late Morning" 的新輪班，從早上十點開始。  
  
 在 updategram 中， **updg： id**屬性會在和區塊中的元素之間建立關聯 **\<before>** **\<after>** 。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Shift updg:id="x" Name="Day" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift updg:id="y" Name="Late Morning"   
                            StartTime="1900-01-01 10:00:00.000"  
                            EndTime="1900-01-01 18:00:00.000"  
                            ModifiedDate="2004-06-01 00:00:00.000"/>  
      <HumanResources.Shift updg:id="x" Name="Early Morning" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 請注意**updg： id**屬性如何將區塊中元素的第一個實例 \<HumanResources.Shift> **\<before>** 與區塊中專案的第二個實例配對 \<HumanResources.Shift> **\<after>** 。  
  
##### <a name="to-test-the-updategram"></a>若要測試 Updategram  
  
1.  複製上述的 updategram 範本，並將其貼到文字檔中。 將檔案儲存為 UpdateMultipleRecords.xml。  
  
2.  建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行 Updategram。  
  
     如需詳細資訊，請參閱[使用 ADO 執行 SQLXML 4.0 查詢](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
### <a name="c-specifying-multiple-before-and-after-blocks"></a>C. 指定多個 \<before> 和 \<after> 區塊  
 若要避免不明確，您可以使用多個 **\<before>** 和區塊配對，在範例 B 中撰寫 updategram **\<after>** 。 指定 **\<before>** 和 **\<after>** 配對是一種指定多個更新的方式，最小的混淆。 此外，如果 **\<before>** 和 **\<after>** 區塊最多指定一個元素，您就不需要使用**updg： id**屬性。  
  
> [!NOTE]  
>  若要形成一組配對， **\<after>** 標記必須緊接在其對應的 **\<before>** 標記之後。  
  
 在下列 updategram 中，第一個 **\<before>** 和 **\<after>** 配對會更新 day shift 的 shift 名稱。 第二個配對會插入新的輪班記錄。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Shift ShiftID="1" Name="Day" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift Name="Early Morning" />  
    </updg:after>  
    <updg:before>  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift Name="Late Morning"   
                            StartTime="1900-01-01 10:00:00.000"  
                            EndTime="1900-01-01 18:00:00.000"  
                            ModifiedDate="2004-06-01 00:00:00.000"/>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>若要測試 Updategram  
  
1.  複製上述的 updategram 範本，並將其貼到文字檔中。 將檔案儲存為 UpdateMultipleBeforeAfter.xml。  
  
2.  建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行 Updategram。  
  
     如需詳細資訊，請參閱[使用 ADO 執行 SQLXML 4.0 查詢](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
### <a name="d-specifying-multiple-sync-blocks"></a>D. 指定多個 \<sync> 區塊  
 您可以 **\<sync>** 在 updategram 中指定多個區塊。 所指定的每個 **\<sync>** 區塊都是獨立的交易。  
  
 在下列 updategram 中，第一個 **\<sync>** 區塊會更新 Sales. Customer 資料表中的記錄。 為了簡單起見，Updategram 僅會指定所需的資料行值；識別值 (CustomerID) 以及要更新的值 (SalesPersonID)。  
  
 第二個 **\<sync>** 區塊會將兩筆記錄加入 SalesOrderHeader 資料表。 針對這個資料表，SalesOrderID 是 IDENTITY 類型的資料行。 因此，updategram 不會在每個元素中指定 SalesOrderID 的值 \<Sales.SalesOrderHeader> 。  
  
 指定多個 **\<sync>** 區塊很有用，因為如果第二個 **\<sync>** 區塊（交易）無法將記錄新增至 SalesOrderHeader 資料表，第一個 **\<sync>** 區塊仍然可以更新 sales. customer 資料表中的客戶記錄。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
      <Sales.Customer CustomerID="1" SalesPersonID="280" />  
    </updg:before>  
    <updg:after>  
      <Sales.Customer CustomerID="1" SalesPersonID="283" />  
    </updg:after>  
  </updg:sync>  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
   <Sales.SalesOrderHeader   
             CustomerID="1"  
             RevisionNumber="1"  
             OrderDate="2004-07-01 00:00:00.000"  
             DueDate="2004-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="24643.9362"  
             TaxAmt="1971.5149"  
             Freight="616.0984"  
             rowguid="01010101-2222-3333-4444-556677889900"  
             ModifiedDate="2004-07-08 00:00:00.000" />  
   <Sales.SalesOrderHeader  
             CustomerID="1"  
             RevisionNumber="1"  
             OrderDate="2004-07-01 00:00:00.000"  
             DueDate="2004-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="1000.0000"  
             TaxAmt="0.0000"  
             Freight="0.0000"  
             rowguid="10101010-2222-3333-4444-556677889900"  
             ModifiedDate="2004-07-09 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>若要測試 Updategram  
  
1.  複製上述的 updategram 範本，並將其貼到文字檔中。 將檔案儲存為 UpdateMultipleSyncs.xml。  
  
2.  建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行 Updategram。  
  
     如需詳細資訊，請參閱[使用 ADO 執行 SQLXML 4.0 查詢](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
### <a name="e-using-a-mapping-schema"></a>E. 使用對應的結構描述  
 在此範例中，updategram 會使用**對應架構**屬性來指定對應架構。 (沒有預設的對應，也就是說，對應結構描述會在 Updategram 中提供所需的元素和屬性對應給資料庫資料表與資料行)。  
  
 在 Updategram 中指定的元素和屬性指的是對應結構描述中的元素和屬性。  
  
 下列 XSD 對應架構具有 **\<Customer>** 、和專案， **\<Order>** 這些專案 **\<OD>** 會對應至資料庫中的 Customer、SalesOrderHeader 和 sales. SalesOrderDetail 資料表。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustomerOrder"  
          parent="Sales.Customer"  
          parent-key="CustomerID"  
          child="Sales.SalesOrderHeader"  
          child-key="CustomerID" />  
  
    <sql:relationship name="OrderOD"  
          parent="Sales.SalesOrderHeader"  
          parent-key="SalesOrderID"  
          child="Sales.SalesOrderDetail"  
          child-key="SalesOrderID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"  
                     sql:relationship="CustomerOrder" >  
           <xsd:complexType>  
              <xsd:sequence>  
                <xsd:element name="OD"   
                             sql:relation="Sales.SalesOrderDetail"  
                             sql:relationship="OrderOD" >  
                 <xsd:complexType>  
                  <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
                  <xsd:attribute name="ProductID" type="xsd:integer" />  
                  <xsd:attribute name="UnitPrice" type="xsd:decimal" />  
                  <xsd:attribute name="OrderQty" type="xsd:integer" />  
                  <xsd:attribute name="UnitPriceDiscount" type="xsd:decimal" />   
                 </xsd:complexType>  
                </xsd:element>  
              </xsd:sequence>  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="OrderDate" type="xsd:date" />  
           </xsd:complexType>  
        </xsd:element>  
      </xsd:sequence>  
      <xsd:attribute name="CustomerID"   type="xsd:string" />   
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 此對應結構描述 (UpdategramMappingSchema.xml) 會在下列的 Updategram 中指定。 Updategram 會針對特定的訂單，在 Sales.SalesOrderDetail 資料表中加入訂單詳細資料項目。 Updategram 包含 nested 元素：在專案 **\<OD>** 內嵌套的元素 **\<Order>** 。 在這兩個元素之間的主索引鍵/外部索引鍵關聯性會在對應的結構描述中指定。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema="UpdategramMappingSchema.xml" >  
    <updg:before>  
       <Order SalesOrderID="43659" />  
    </updg:before>  
    <updg:after>  
      <Order SalesOrderID="43659" >  
          <OD ProductID="776" UnitPrice="2329.0000"  
              OrderQty="2" UnitPriceDiscount="0.0" />  
      </Order>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>若要測試 Updategram  
  
1.  複製上述的對應結構描述，並將其貼到文字檔中。 將檔案儲存為 UpdategramMappingSchema.xml。  
  
2.  複製上述的 updategram 範本，並將其貼到文字檔中。 然後將檔案在先前用於儲存對應結構描述 (UpdategramMappingSchema.xml) 的相同資料夾中，儲存為 UpdateWithMappingSchema.xml。  
  
3.  建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行 Updategram。  
  
     如需詳細資訊，請參閱[使用 ADO 執行 SQLXML 4.0 查詢](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 如需使用對應架構之 updategram 的更多範例，請參閱[在 Updategram 中指定批註式對應架構 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)。  
  
### <a name="f-using-a-mapping-schema-with-idrefs-attributes"></a>F. 搭配 IDREFS 屬性使用對應的結構描述  
 此範例說明 Updategrams 如何使用對應結構描述中的 IDREFS 屬性更新多個資料表中的記錄。 此範例假設資料庫由下列資料表組成：  
  
-   Student(StudentID, LastName)  
  
-   Course(CourseID, CourseName)  
  
-   Enrollment(StudentID, CourseID)  
  
 因為一位學生可以註冊許多課程，而且一個課程可以有許多學生，因此需要第三個資料表，也就是 Enrollment 資料表，來代表這個 M:N 關聯性。  
  
 下列 XSD 對應架構會使用 **\<Student>** 、和元素來提供資料表的 XML 視圖 **\<Course>** **\<Enrollment>** 。 對應架構中的**IDREFS**屬性會指定這些元素之間的關聯性。 元素上的**StudentIDList**屬性 **\<Course>** 是一個**IDREFS**類型屬性，它會參考註冊資料表中的 StudentID 資料行。 同樣地，元素上的**EnrolledIn**屬性 **\<Student>** 是一個**IDREFS**類型屬性，它會參考註冊資料表中的 CourseID 資料行。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="StudentEnrollment"  
          parent="Student"  
          parent-key="StudentID"  
          child="Enrollment"  
          child-key="StudentID" />  
  
    <sql:relationship name="CourseEnrollment"  
          parent="Course"  
          parent-key="CourseID"  
          child="Enrollment"  
          child-key="CourseID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Course" sql:relation="Course"   
                             sql:key-fields="CourseID" >  
    <xsd:complexType>  
    <xsd:attribute name="CourseID"  type="xsd:string" />   
    <xsd:attribute name="CourseName"   type="xsd:string" />   
    <xsd:attribute name="StudentIDList" sql:relation="Enrollment"  
                 sql:field="StudentID"  
                 sql:relationship="CourseEnrollment"   
                                     type="xsd:IDREFS" />  
  
    </xsd:complexType>  
  </xsd:element>  
  <xsd:element name="Student" sql:relation="Student" >  
    <xsd:complexType>  
    <xsd:attribute name="StudentID"  type="xsd:string" />   
    <xsd:attribute name="LastName"   type="xsd:string" />   
    <xsd:attribute name="EnrolledIn" sql:relation="Enrollment"  
                 sql:field="CourseID"  
                 sql:relationship="StudentEnrollment"   
                                     type="xsd:IDREFS" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 每當您在 Updategram 中指定此結構描述，並在 Course 資料表中插入記錄時，Updategram 會在 Course 資料表中插入一個新的課程記錄。 如果您為 the StudentIDList 屬性指定一或多個新的學生識別碼，Updategram 也會為每個新的學生，在 Enrollment 資料表中插入一筆記錄。 Updategram 可確保沒有將重複項目加入到 Enrollment 資料表中。  
  
##### <a name="to-test-the-updategram"></a>若要測試 Updategram  
  
1.  在資料庫中建立虛擬根目錄中指定的這些資料表：  
  
    ```  
    CREATE TABLE Student(StudentID varchar(10) primary key,   
                         LastName varchar(25))  
    CREATE TABLE Course(CourseID varchar(10) primary key,   
                        CourseName varchar(25))  
    CREATE TABLE Enrollment(StudentID varchar(10)   
                                      references Student(StudentID),  
                           CourseID varchar(10)   
                                      references Course(CourseID))  
    ```  
  
2.  加入這個範例資料：  
  
    ```  
    INSERT INTO Student VALUES ('S1','Davoli')  
    INSERT INTO Student VALUES ('S2','Fuller')  
  
    INSERT INTO Course VALUES  ('CS101', 'C Programming')  
    INSERT INTO Course VALUES  ('CS102', 'Understanding XML')  
  
    INSERT INTO Enrollment VALUES ('S1', 'CS101')  
    INSERT INTO Enrollment VALUES ('S1', 'CS102')  
    ```  
  
3.  複製上述的對應結構描述，並將其貼到文字檔中。 將檔案儲存為 SampleSchema.xml。  
  
4.  將 Updategram (SampleUpdategram) 儲存在前述步驟用於儲存對應結構描述的相同資料夾中  (這個 Updategram 會從 CS102 課程中卸除 StudentID="1" 的學生)。  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleSchema.xml" >  
        <updg:before>  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101 CS102" />  
        </updg:before>  
        <updg:after >  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
5.  建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行 Updategram。  
  
     如需詳細資訊，請參閱[使用 ADO 執行 SQLXML 4.0 查詢](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
6.  儲存並執行下列 Updategram，如前述步驟所述。 Updategram 會在 Enrollment 資料表中加入一筆記錄，藉以將 StudentID="1" 的學生加回 CS102 課程。  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleSchema.xml" >  
        <updg:before>  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101" />  
        </updg:before>  
        <updg:after >  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101 CS102" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
7.  儲存並執行這個接下來的 Updategram，如前述步驟所述。 這個 Updategram 會插入三個新的學生，並為他們註冊 CS101 課程。 IDREFS 關聯性會將資料表再次插入 Enrollment 資料表中。  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleSchema.xml" >  
        <updg:before>  
           <Course updg:id="y" CourseID="CS101"   
                               CourseName="C Programming" />  
        </updg:before>  
        <updg:after >  
           <Student updg:id="x1" StudentID="S3" LastName="Leverling" />  
           <Student updg:id="x2" StudentID="S4" LastName="Pecock" />  
           <Student updg:id="x3" StudentID="S5" LastName="Buchanan" />  
           <Course updg:id="y" CourseID="CS101"  
                               CourseName="C Programming"  
                               StudentIDList="S3 S4 S5" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
 這是相等的 XDR 結構描述：  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <ElementType name="Enrollment" sql:relation="Enrollment" sql:key-fields="StudentID CourseID">  
    <AttributeType name="StudentID" dt:type="id" />  
    <AttributeType name="CourseID" dt:type="id" />  
  
    <attribute type="StudentID" />  
    <attribute type="CourseID" />  
  </ElementType>  
  <ElementType name="Course" sql:relation="Course" sql:key-fields="CourseID">  
    <AttributeType name="CourseID" dt:type="id" />  
    <AttributeType name="CourseName" />  
  
    <attribute type="CourseID" />  
    <attribute type="CourseName" />  
  
    <AttributeType name="StudentIDList" dt:type="idrefs" />  
    <attribute type="StudentIDList" sql:relation="Enrollment" sql:field="StudentID" >  
        <sql:relationship  
                key-relation="Course"  
                key="CourseID"  
                foreign-relation="Enrollment"  
                foreign-key="CourseID" />  
    </attribute>  
  
  </ElementType>  
  <ElementType name="Student" sql:relation="Student">  
    <AttributeType name="StudentID" dt:type="id" />  
     <AttributeType name="LastName" />  
  
    <attribute type="StudentID" />  
    <attribute type="LastName" />  
  
    <AttributeType name="EnrolledIn" dt:type="idrefs" />  
    <attribute type="EnrolledIn" sql:relation="Enrollment" sql:field="CourseID" >  
        <sql:relationship  
                key-relation="Student"  
                key="StudentID"  
                foreign-relation="Enrollment"  
                foreign-key="StudentID" />  
    </attribute>  
  
    <element type="Enrollment" sql:relation="Enrollment" >  
        <sql:relationship key-relation="Student"  
                          key="StudentID"  
                          foreign-relation="Enrollment"  
                          foreign-key="StudentID" />  
    </element>  
  </ElementType>  
  
</Schema>  
```  
  
 如需使用對應架構之 updategram 的更多範例，請參閱[在 Updategram 中指定批註式對應架構 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;SQLXML 4.0&#41;的 Updategram 安全性考慮](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
