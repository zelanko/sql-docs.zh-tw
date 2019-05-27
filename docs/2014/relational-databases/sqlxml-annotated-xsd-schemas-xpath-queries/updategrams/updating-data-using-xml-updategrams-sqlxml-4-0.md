---
title: 更新資料使用 XML Updategram (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: d171270a7605c258f9bc347781cd9a4d91c7a348
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/22/2019
ms.locfileid: "66014680"
---
# <a name="updating-data-using-xml-updategrams-sqlxml-40"></a>使用 XML Updategram 更新資料 (SQLXML 4.0)
  當您更新現有的資料時，您必須同時指定 **\<之前>** 並 **\<之後>** 區塊。 在指定的項目 **\<之前>** 並 **\<之後 >** 區塊描述所需的變更。 Updategram 會使用中所指定的項目 **\<之前>** 區塊來識別資料庫中的現有記錄。 中的對應項目 **\<之後 >** 區塊表示記錄在執行更新作業後所呈現的外觀。 這項資訊，updategram 會建立比對的 SQL 陳述式 **\<之後 >** 區塊。 接著，Updategram 會使用此陳述式來更新資料庫。  
  
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
  
 `<updg:before>`  
 中的項目 **\<之前>** 區塊識別資料庫資料表中的現有記錄。  
  
 `<updg:after>`  
 中的項目 **\<之後>** 區塊描述中指定的記錄 **\<之前>** 區塊應該套用更新之後更新。  
  
 `mapping-schema` 屬性會識別 Updategram 所使用的對應結構描述。 如果 updategram 指定對應結構描述，元素和屬性名稱中指定 **\<之前>** 並 **\<之後>** 區塊必須符合結構描述中的名稱。 對應的結構描述會將這些元素或屬性名稱對應到資料庫資料表和資料行名稱。  
  
 如果 Updategram 沒有指定結構描述，Updategram 會使用預設的對應。 在預設的對應， **\<項目名稱 >** 則 updategram 會對應至資料庫資料表和子元素或屬性對應至資料庫資料行中指定。  
  
 中的項目 **\<之前>** 區塊必須符合資料庫中只有一個資料表資料列。 如果元素符合多個資料表的資料列，或者不符合任何資料表資料列，updategram 會傳回錯誤，並取消整個 **\<同步 >** 區塊。  
  
 Updategram 可以包含多個 **\<同步 >** 區塊。 每個 **\<同步 >** 區塊視為交易。 每個 **\<同步>** 區塊可以有多個 **\<之前>** 並 **\<之後>** 區塊。 例如，如果您要更新兩個現有的記錄，您可以指定兩個 **\<之前>** 並 **\<之後>** 配對，各正在更新每一筆記錄。  
  
## <a name="using-the-updgid-attribute"></a>使用 updg:id 屬性  
 多個項目中指定的時 **\<之前>** 並 **\<之後>** 區塊，使用`updg:id`屬性來標記中的資料列 **\<之前>** 並 **\<之後>** 區塊。 處理邏輯會使用這項資訊來判斷中的哪個記錄 **\<之前>** 區塊中的哪個記錄配對 **\<之後>** 區塊。  
  
 如果下列其中一個項目存在，就不需要 `updg:id` 屬性 (但建議存在)：  
  
-   指定之對應結構描述中的元素已經定義 `sql:key-fields` 屬性。  
  
-   在 Updategram 中有一或多個針對索引鍵欄位提供的特定值。  
  
 如果不是在案例中，updategram 會使用索引鍵資料行中所指定`sql:key-fields`配對中的項目 **\<之前>** 並 **\<之後>** 區塊。  
  
 如果對應結構描述沒有識別索引鍵資料行 (透過使用 `sql:key-fields`)，或者如果 Updategram 要更新索引鍵資料行值，您必須指定 `updg:id`。  
  
 中所識別的資料錄 **\<之前>** 並 **\<之後>** 區塊並沒有相同的順序。 `updg:id`屬性會強制執行中所指定的項目之間的關聯 **\<之前>** 並 **\<之後>** 區塊。  
  
 如果您指定一個項目 **\<之前>** 區塊，並在只有一個對應的項目 **\<之後>** 封鎖，請使用`updg:id`不需要。 不過，建議您無論如何還是指定 `updg:id` 來避免模稜兩可的情況。  
  
## <a name="examples"></a>範例  
 使用 Updategram 範例之前，請注意下列事項：  
  
-   大部分的範例都會使用預設對應 (也就是說，Updategram 中不會指定任何對應結構描述)。 如需使用對應結構描述的 updategram 的範例，請參閱[在 Updategram 中指定註解式對應結構描述&#40;SQLXML 4.0&#41;](specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)。  
  
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
  
 記錄中所述 **\<之前>** 區塊則代表在資料庫中目前的記錄。 Updategram 會使用指定的資料行值的所有 **\<之前>** 来搜尋的記錄區塊。 在此 updategram 中， **\<之前>** 區塊僅提供 ContactID 資料行; 因此，updategram 會使用這個值來搜尋記錄。 如果您要將 LastName 值加入到此區塊中，Updategram 會同時使用 ContactID 和 LastName 值進行搜尋。  
  
 在此 updategram 中， **\<之後 >** 區塊提供只有 LastName 資料行值，因為這是唯一的值正在變更。  
  
##### <a name="to-test-the-updategram"></a>若要測試 Updategram  
  
1.  複製上述的 updategram 範本，並將其貼到文字檔中。 將檔案儲存為 UpdateLastName.xml。  
  
2.  建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行 Updategram。  
  
     如需詳細資訊，請參閱 <<c0> [ 使用 ADO 執行 SQLXML 4.0 查詢](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
### <a name="b-updating-multiple-records-by-using-the-updgid-attribute"></a>B. 使用 updg:id 屬性更新多筆記錄  
 在此範例中，updategram 會在 AdventureWorks 資料庫的 HumanResources.Shift 資料表上執行兩個變更：  
  
-   它會將早上七點起的原始日班名稱從 "Day" 變更為 "Early Morning"。  
  
-   它會插入名稱為 "Late Morning" 的新輪班，從早上十點開始。  
  
 在 updategram 中，`updg:id`屬性會建立中的項目之間的關聯 **\<之前>** 並 **\<之後>** 區塊。  
  
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
  
 請注意如何`updg:id`配對的第一個執行個體的屬性\<HumanResources.Shift> 中的項目 **\<之前>** 區塊的第二個執行個體\<HumanResources.Shift > 中的項目 **\<之後>** 區塊。  
  
##### <a name="to-test-the-updategram"></a>若要測試 Updategram  
  
1.  複製上述的 updategram 範本，並將其貼到文字檔中。 將檔案儲存為 UpdateMultipleRecords.xml。  
  
2.  建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行 Updategram。  
  
     如需詳細資訊，請參閱 <<c0> [ 使用 ADO 執行 SQLXML 4.0 查詢](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
### <a name="c-specifying-multiple-before-and-after-blocks"></a>C. 指定多重\<之前> 和\<之後> 區塊  
 若要避免模稜兩可，您可以撰寫 updategram 範例 B 中使用多個 **\<之前>** 並 **\<之後>** 區塊配對。 指定 **\<之前>** 並 **\<之後>** 組是一種方式的指定最不混亂的多個更新。 此外，如果每一個的 **\<之前>** 並 **\<之後>** 區塊指定最多一個項目，您不必使用`updg:id`屬性。  
  
> [!NOTE]  
>  若要形成配對， **\<之後>** 標籤必須緊接其對應 **\<之前>** 標記。  
  
 在下列的 updategram 中，第一個 **\<之前>** 並 **\<之後>** 配對會更新日班的輪班名稱。 第二個配對會插入新的輪班記錄。  
  
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
  
     如需詳細資訊，請參閱 <<c0> [ 使用 ADO 執行 SQLXML 4.0 查詢](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
### <a name="d-specifying-multiple-sync-blocks"></a>D. 指定多個\<同步 > 區塊  
 您可以指定多個 **\<同步 >** 封鎖在 updategram 中。 每個 **\<同步 >** 指定的區塊是獨立的交易。  
  
 在下列的 updategram 中，第一個 **\<同步 >** 區塊會更新 Sales.Customer 資料表中的記錄。 為了簡單起見，Updategram 僅會指定所需的資料行值；識別值 (CustomerID) 以及要更新的值 (SalesPersonID)。  
  
 第二個 **\<同步 >** 區塊會將 Sales.SalesOrderHeader 資料表中的兩筆記錄。 針對這個資料表，SalesOrderID 是 IDENTITY 類型的資料行。 因此，updategram 未指定 SalesOrderID 的值在每個\<Sales.SalesOrderHeader > 項目。  
  
 指定多重 **\<同步 >** 區塊相當實用因為如果第二個 **\<同步 >** 區塊 （交易） 無法將記錄加入到 Sales.SalesOrderHeader 資料表第一個 **\<同步 >** 區塊仍然可以更新 Sales.Customer 資料表中的客戶記錄。  
  
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
  
     如需詳細資訊，請參閱 <<c0> [ 使用 ADO 執行 SQLXML 4.0 查詢](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
### <a name="e-using-a-mapping-schema"></a>E. 使用對應的結構描述  
 在此範例中，Updategram 會使用 `mapping-schema` 屬性指定對應的結構描述  (沒有預設的對應，也就是說，對應結構描述會在 Updategram 中提供所需的元素和屬性對應給資料庫資料表與資料行)。  
  
 在 Updategram 中指定的元素和屬性指的是對應結構描述中的元素和屬性。  
  
 下列 XSD 對應結構描述擁有 **\<客戶 >** ， **\<順序 >** ，以及 **\<OD >** 元素會對應到資料庫中的 Sales.Customer、 Sales.SalesOrderHeader 和 Sales.SalesOrderDetail 資料表。  
  
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
  
 此對應結構描述 (UpdategramMappingSchema.xml) 會在下列的 Updategram 中指定。 Updategram 會針對特定的訂單，在 Sales.SalesOrderDetail 資料表中加入訂單詳細資料項目。 Updategram 包含巢狀項目：  **\<OD >** 元素內部巢狀 **\<順序 >** 項目。 在這兩個元素之間的主索引鍵/外部索引鍵關聯性會在對應的結構描述中指定。  
  
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
  
     如需詳細資訊，請參閱 <<c0> [ 使用 ADO 執行 SQLXML 4.0 查詢](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 如需使用對應結構描述的 updategram 的範例，請參閱[在 Updategram 中指定註解式對應結構描述&#40;SQLXML 4.0&#41;](specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)。  
  
### <a name="f-using-a-mapping-schema-with-idrefs-attributes"></a>F. 搭配 IDREFS 屬性使用對應的結構描述  
 此範例說明 Updategrams 如何使用對應結構描述中的 IDREFS 屬性更新多個資料表中的記錄。 此範例假設資料庫由下列資料表組成：  
  
-   Student(StudentID, LastName)  
  
-   Course(CourseID, CourseName)  
  
-   Enrollment(StudentID, CourseID)  
  
 因為一位學生可以註冊許多課程，而且一個課程可以有許多學生，因此需要第三個資料表，也就是 Enrollment 資料表，來代表這個 M:N 關聯性。  
  
 下列 XSD 對應結構描述透過提供資料表的 XML 檢視 **\<學生 >** ， **\<課程 >** ，以及 **\<註冊>** 項目。 **IDREFS**對應結構描述中的屬性會指定這些項目之間的關聯性。 **StudentIDList**屬性上 **\<課程 >** 項目是**IDREFS**參考 Enrollment 資料表中的 StudentID 資料行的類型屬性。 同樣地， **enrolledin 屬性**屬性上 **\<學生 >** 項目是**IDREFS**參考註冊中的 CourseID 資料行的類型屬性資料表。  
  
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
  
     如需詳細資訊，請參閱 <<c0> [ 使用 ADO 執行 SQLXML 4.0 查詢](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
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
  
 如需使用對應結構描述的 updategram 的範例，請參閱[在 Updategram 中指定註解式對應結構描述&#40;SQLXML 4.0&#41;](specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Updategram 安全性考量&#40;SQLXML 4.0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
