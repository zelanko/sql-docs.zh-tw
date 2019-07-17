---
title: XML 大量載入範例 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- overflow-field annotation
- ConnectionCommand property
- XMLFragment property
- relationship chains [SQLXML]
- multiple table bulk loading
- examples [SQLXML], XML Bulk Load
- overflow data [SQLXML]
- sql:datatype
- transaction mode [SQLXML]
- CheckConstraints property
- sql:overflow-field
- XML Bulk Load [SQLXML], examples
- TempFilePath property
- datatype annotation
- Transaction property
- KeepIdentity property
- Execute method
- streaming XML data
- xml data type [SQL Server], SQLXML
- bulk load [SQLXML], examples
ms.assetid: 970e4553-b41d-4a12-ad50-0ee65d1f305d
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7e2b536b6f1bc22e15948dfb1a0d4df539c099f6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68005271"
---
# <a name="xml-bulk-load-examples-sqlxml-40"></a>XML 大量載入範例 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  下列範例說明 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的 XML 大量載入功能。 每個範例都會提供一個 XSD 結構描述及其等同的 XDR 結構描述。  
  
## <a name="bulk-loader-script-validateandbulkloadvbs"></a>大量載入程式指令碼 (ValidateAndBulkload.vbs)  
 下列指令碼，以撰寫[!INCLUDE[msCoName](../../../includes/msconame-md.md)]Visual Basic Scripting Edition (VBScript)，將 XML 文件載入到 XML DOM; 根據結構描述; 進行驗證，而且文件是否有效，執行 XML 大量載入將 XML 載入[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料表。 此指令碼可以搭配本主題稍後所參考的每個個別範例使用。  
  
> [!NOTE]  
>  如果沒有從資料檔上傳任何內容，XML 大量載入不會擲回警告或錯誤。 因此，最好在執行大量載入作業之前，先驗證您的 XML 資料檔。  
  
```vbs  
Dim FileValid  
  
set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
objBL.ConnectionString = "provider=SQLOLEDB;data source=MyServer;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile = "c:\error.log"  
  
'Validate the data file prior to bulkload  
Dim sOutput   
sOutput = ValidateFile("SampleXMLData.xml", "", "SampleSchema.xml")  
WScript.Echo sOutput  
  
If FileValid Then  
   ' Check constraints and initiate transaction (if needed)  
   ' objBL.CheckConstraints = True  
   ' objBL.Transaction=True  
  'Execute XML bulkload using file.  
  objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
  set objBL=Nothing  
End If  
  
Function ValidateFile(strXmlFile,strUrn,strXsdFile)  
  
   ' Create a schema cache and add SampleSchema.xml to it.  
   Dim xs, fso, sAppPath  
   Set fso = CreateObject("Scripting.FileSystemObject")   
   Set xs = CreateObject("MSXML2.XMLSchemaCache.6.0")  
   sAppPath = fso.GetFolder(".")   
   xs.Add strUrn, sAppPath & "\" & strXsdFile  
  
   ' Create an XML DOMDocument object.  
   Dim xd   
   Set xd = CreateObject("MSXML2.DOMDocument.6.0")  
  
   ' Assign the schema cache to the DOM document.  
   ' schemas collection.  
   Set xd.schemas = xs  
  
   ' Load XML document as DOM document.  
   xd.async = False  
   xd.Load sAppPath & "\" & strXmlFile  
  
   ' Return validation results in message to the user.  
   If xd.parseError.errorCode <> 0 Then  
        ValidateFile = "Validation failed on " & _  
             strXmlFile & vbCrLf & _  
             "=======" & vbCrLf & _  
             "Reason: " & xd.parseError.reason & _  
             vbCrLf & "Source: " & _  
             xd.parseError.srcText & _  
             vbCrLf & "Line: " & _  
             xd.parseError.Line & vbCrLf  
             FileValid = False  
    Else  
        ValidateFile = "Validation succeeded for " & _  
             strXmlFile & vbCrLf & _  
             "========" & _  
             vbCrLf & "Contents to be bulkloaded" & vbCrLf  
             FileValid = True  
    End If  
End Function  
```  
  
## <a name="a-bulk-loading-xml-in-a-table"></a>A. 將 XML 大量載入到資料表中  
 此範例會建立執行個體的連接[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ConnectionString 屬性 (MyServer) 中指定。 此範例也會指定 ErrorLogFile 屬性。 因此，錯誤輸出會儲存在指定的檔案 ("C:\error.log") 中，您也可以決定變更到不同的位置。 另請注意 Execute 方法已做為參數的對應結構描述檔案 (SampleSchema.xml) 和 XML 資料檔 (SampleXMLData.xml)。 大量載入時執行，您已在中建立的 Cust 資料表**tempdb**資料庫會包含在 XML 資料檔案的內容為基礎的新記錄。  
  
#### <a name="to-test-a-sample-bulk-load"></a>測試大量載入範例  
  
1.  建立下述資料表：  
  
    ```sql  
    CREATE TABLE Cust(CustomerID  int PRIMARY KEY,  
                      CompanyName varchar(20),  
                      City        varchar(20));  
    GO  
    ```  
  
2.  以慣用的文字編輯器或 XML 編輯器建立一個檔案，然後將其儲存為 SampleSchema.xml。 將下列 XSD 結構描述加入到此檔案中：  
  
    ```xml  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
       <xsd:element name="ROOT" sql:is-constant="1" >  
         <xsd:complexType>  
           <xsd:sequence>  
             <xsd:element name="Customers" sql:relation="Cust" maxOccurs="unbounded">  
               <xsd:complexType>  
                 <xsd:sequence>  
                   <xsd:element name="CustomerID"  type="xsd:integer" />  
                   <xsd:element name="CompanyName" type="xsd:string" />  
                   <xsd:element name="City"        type="xsd:string" />  
                 </xsd:sequence>  
               </xsd:complexType>  
             </xsd:element>  
           </xsd:sequence>  
          </xsd:complexType>  
         </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  以慣用的文字編輯器或 XML 編輯器建立一個檔案，然後將其儲存為 SampleXMLData.xml。 將下列 XML 文件加入到此檔案中：  
  
    ```xml  
    <ROOT>  
      <Customers>  
        <CustomerID>1111</CustomerID>  
        <CompanyName>Sean Chai</CompanyName>  
        <City>New York</City>  
      </Customers>  
      <Customers>  
        <CustomerID>1112</CustomerID>  
        <CompanyName>Tom Johnston</CompanyName>  
         <City>Los Angeles</City>  
      </Customers>  
      <Customers>  
        <CustomerID>1113</CustomerID>  
        <CompanyName>Institute of Art</CompanyName>  
        <City>Chicago</City>  
      </Customers>  
    </ROOT>  
    ```  
  
4.  以慣用的文字編輯器或 XML 編輯器建立一個檔案，然後將其儲存為 ValidateAndBulkload.vbs。 將本主題開頭提供的 VBScript 程式碼加入到此檔案中。 修改連接字串以提供適當的伺服器名稱。 指定適當的路徑，做為 Execute 方法的參數所指定的檔案。  
  
5.  執行 VBScript 程式碼。 XML 大量載入會將 XML 載入到 Cust 資料表中。  
  
 這是相等的 XDR 結構描述：  
  
```xml  
  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >   
  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="ROOT" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers"  sql:relation="Cust" >  
      <element type="CustomerID"  sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City"        sql:field="City" />  
  
   </ElementType>  
</Schema>  
```  
  
## <a name="b-bulk-loading-xml-data-in-multiple-tables"></a>B. 將 XML 資料大量載入到多個資料表中  
 在此範例中，XML 文件組成 **\<客戶 >** 並 **\<順序 >** 項目。  
  
```xml  
<ROOT>  
  <Customers>  
    <CustomerID>1111</CustomerID>  
    <CompanyName>Sean Chai</CompanyName>  
    <City>NY</City>  
    <Order OrderID="1" />  
    <Order OrderID="2" />  
  </Customers>  
  <Customers>  
    <CustomerID>1112</CustomerID>  
    <CompanyName>Tom Johnston</CompanyName>  
     <City>LA</City>    
    <Order OrderID="3" />  
  </Customers>  
  <Customers>  
    <CustomerID>1113</CustomerID>  
    <CompanyName>Institute of Art</CompanyName>  
    <Order OrderID="4" />  
  </Customers>  
</ROOT>  
```  
  
 此範例會大量載入 XML 資料到兩個資料表**Cust**並**CustOrder**:  
  
-   Cust (CustomerID、 CompanyName、 City)  
  
-   CustOrder （訂單編號、 客戶編號）  
  
 下列 XSD 結構描述會定義這些資料表的 XML 檢視。 結構描述指定的父-子關係 **\<客戶 >** 並 **\<順序 >** 項目。  
  
```xml  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:appinfo>  
      <sql:relationship name="CustCustOrder"  
          parent="Cust"  
          parent-key="CustomerID"  
          child="CustOrder"  
          child-key="CustomerID" />  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="ROOT" sql:is-constant="1" >  
    <xsd:complexType>  
      <xsd:sequence>  
        <xsd:element name="Customers" sql:relation="Cust" >  
          <xsd:complexType>  
            <xsd:sequence>  
              <xsd:element name="CustomerID"  type="xsd:integer" />  
              <xsd:element name="CompanyName" type="xsd:string" />  
              <xsd:element name="City"        type="xsd:string" />  
              <xsd:element name="Order"   
                          sql:relation="CustOrder"  
                          sql:relationship="CustCustOrder" >  
                <xsd:complexType>  
                  <xsd:attribute name="OrderID" type="xsd:integer" />  
                </xsd:complexType>  
              </xsd:element>  
             </xsd:sequence>  
          </xsd:complexType>  
        </xsd:element>  
      </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 XML 大量載入會使用主索引鍵/外部索引鍵關聯性之間指定上述 **\<Cust >** 並 **\<CustOrder >** 大量的項目會將資料載入至兩個資料表.  
  
#### <a name="to-test-a-sample-bulk-load"></a>測試大量載入範例  
  
1.  建立兩個資料表中的**tempdb**資料庫：  
  
    ```sql  
    USE tempdb;  
    CREATE TABLE Cust(  
           CustomerID  int PRIMARY KEY,  
           CompanyName varchar(20),  
           City        varchar(20));  
    CREATE TABLE CustOrder(        OrderID     int PRIMARY KEY,   
            CustomerID int FOREIGN KEY REFERENCES Cust(CustomerID));  
    ```  
  
2.  以慣用的文字編輯器或 XML 編輯器建立一個檔案，然後將其儲存為 SampleSchema.xml。 將這個範例所提供的 XSD 結構描述加入到此檔案中。  
  
3.  以慣用的文字編輯器或 XML 編輯器建立一個檔案，然後將其儲存為 SampleData.xml。 將這個範例先前所提供的 XML 文件加入到此檔案中。  
  
4.  以慣用的文字編輯器或 XML 編輯器建立一個檔案，然後將其儲存為 ValidateAndBulkload.vbs。 將本主題開頭提供的 VBScript 程式碼加入到此檔案中。 修改連接字串以提供適當的伺服器和資料庫名稱。 指定適當的路徑，做為 Execute 方法的參數所指定的檔案。  
  
5.  執行上述的 VBScript 程式碼。 XML 大量載入會將 XML 文件載入到 Cust 和 CustOrder 資料表中。  
  
 這是相等的 XDR 結構描述：  
  
```xml  
  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >   
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="ROOT" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust" >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
<sql:relationship  
                key-relation="Cust"  
                key="CustomerID"  
                foreign-key="CustomerID"  
                foreign-relation="CustOrder" />  
      </element>  
   </ElementType>  
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
</Schema>  
```  
  
## <a name="c-using-chain-relationships-in-the-schema-to-bulk-load-xml"></a>C. 使用結構描述中的鏈結關聯性大量載入 XML  
 此範例說明 XML 大量載入如何使用在對應結構描述中指定的 M:N 關聯性，將代表 M:N 關聯性的資料載入到資料表中。  
  
 例如，請考慮下列 XSD 結構描述：  
  
```xml  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="OrderOD"  
          parent="Ord"  
          parent-key="OrderID"  
          child="OrderDetail"  
          child-key="OrderID" />  
  
    <sql:relationship name="ODProduct"  
          parent="OrderDetail"  
          parent-key="ProductID"  
          child="Product"  
          child-key="ProductID"   
          inverse="true"/>  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="ROOT" sql:is-constant="1" >  
    <xsd:complexType>  
      <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Ord"   
                     sql:key-fields="OrderID" >  
          <xsd:complexType>  
            <xsd:sequence>  
             <xsd:element name="Product"  
                          sql:relation="Product"   
                          sql:key-fields="ProductID"  
                          sql:relationship="OrderOD ODProduct">  
               <xsd:complexType>  
                 <xsd:attribute name="ProductID" type="xsd:int" />  
                 <xsd:attribute name="ProductName" type="xsd:string" />  
               </xsd:complexType>  
             </xsd:element>  
           </xsd:sequence>  
           <xsd:attribute name="OrderID"   type="xsd:integer" />   
           <xsd:attribute name="CustomerID"   type="xsd:string" />  
         </xsd:complexType>  
       </xsd:element>  
      </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 結構描述會指定 **\<順序 >** 項目 **\<產品 >** 子項目。 **\<順序 >** 元素會對應到 Ord 資料表並 **\<產品 >** 元素會對應到資料庫中的 Product 資料表。 在指定的鏈結關聯性 **\<產品 >** 項目會識別 OrderDetail 資料表所代表的 M:N 關聯性。 (一個訂單可以包含許多產品，而一個產品可以包含在許多訂單中)。  
  
 當您要使用此結構描述大量載入 XML 文件時，會將記錄加入到 Ord、Product 和 OrderDetail 資料表中。  
  
#### <a name="to-test-a-working-sample"></a>測試工作範例  
  
1.  建立三個資料表：  
  
    ```sql  
    CREATE TABLE Ord (  
             OrderID     int  PRIMARY KEY,  
             CustomerID  varchar(5));  
    GO  
    CREATE TABLE Product (  
             ProductID   int PRIMARY KEY,  
             ProductName varchar(20));  
    GO  
    CREATE TABLE OrderDetail (  
           OrderID     int FOREIGN KEY REFERENCES Ord(OrderID),  
           ProductID   int FOREIGN KEY REFERENCES Product(ProductID),  
                       CONSTRAINT OD_key PRIMARY KEY (OrderID, ProductID));  
    GO  
    ```  
  
2.  將這個範例在上方所提供的結構描述儲存為 SampleSchema.xml。  
  
3.  將下列 XML 資料範例儲存為 SampleXMLData.xml：  
  
    ```xml  
    <ROOT>    
      <Order OrderID="1" CustomerID="ALFKI">  
        <Product ProductID="1" ProductName="Chai" />  
        <Product ProductID="2" ProductName="Chang" />  
      </Order>  
      <Order OrderID="2" CustomerID="ANATR">  
        <Product ProductID="3" ProductName="Aniseed Syrup" />  
        <Product ProductID="4" ProductName="Gumbo Mix" />  
      </Order>  
    </ROOT>  
    ```  
  
4.  以慣用的文字編輯器或 XML 編輯器建立一個檔案，然後將其儲存為 ValidateAndBulkload.vbs。 將本主題開頭提供的 VBScript 程式碼加入到此檔案中。 修改連接字串以提供適當的伺服器和資料庫名稱。 從此範例的原始程式碼取消註解下列幾行。  
  
    ```vbs  
    objBL.CheckConstraints = True  
    objBL.Transaction=True  
    ```  
  
5.  執行 VBScript 程式碼。 XML 大量載入會將 XML 文件載入到 Ord 和 Product 資料表中。  
  
## <a name="d-bulk-loading-in-identity-type-columns"></a>D. 大量載入識別類型資料行  
 此範例說明大量載入如何處理識別類型資料行。 在此範例中，資料會大量載入到三個資料表 (Ord、Product 和 OrderDetail) 中。  
  
 在這些資料表中：  
  
-   Ord 資料表中的 OrderID 是識別類型資料行  
  
-   Product 資料表中的 ProductID 是識別類型資料行。  
  
-   OrderDetail 中的 OrderID 和 ProductID 資料行是參考 Ord 和 Product 資料表中對應主索引鍵資料行的外部索引鍵資料行。  
  
 下列是此範例的資料表結構描述：  
  
```  
Ord (OrderID, CustomerID)  
Product (ProductID, ProductName)  
OrderDetail (OrderID, ProductID)  
```  
  
 在此範例中的 XML 大量載入，大量載入物件模型的 KeepIdentity 屬性設為 false。 因此，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會分別在 Product 和 Ord 資料表中，為 ProductID 和 OrderID 資料行產生識別值 (系統會忽略要大量載入之文件所提供的任何值)。  
  
 在此情況下，XML 大量載入會在資料表之間識別主索引鍵/外部索引鍵關聯性。 大量載入會先將記錄插入具有主索引鍵的資料表，然後再將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 所產生的識別值傳播到具有外部索引鍵資料行的資料表中。 在下列範例中，XML 大量載入會以下列順序，將資料插入資料表中。  
  
1.  產品  
  
2.  Ord  
  
3.  OrderDetail  
  
    > [!NOTE]  
    >  若要傳播在 Products 和 Orders 資料表中產生的識別值，處理邏輯需要 XML 大量載入追蹤這些值，以便稍後插入 OrderDetails 資料表中。 方法是，XML 大量載入建立中繼資料表、在這些資料表中擴展資料，並在稍後移除它們。  
  
#### <a name="to-test-a-working-sample"></a>測試工作範例  
  
1.  建立這些資料表：  
  
    ```  
    CREATE TABLE Ord (  
             OrderID     int identity(1,1)  PRIMARY KEY,  
             CustomerID  varchar(5));  
    GO  
    CREATE TABLE Product (  
             ProductID   int identity(1,1) PRIMARY KEY,  
             ProductName varchar(20));  
    GO  
    CREATE TABLE OrderDetail (  
           OrderID     int FOREIGN KEY REFERENCES Ord(OrderID),  
           ProductID   int FOREIGN KEY REFERENCES Product(ProductID),  
                       CONSTRAINT OD_key PRIMARY KEY (OrderID, ProductID));  
    GO  
    ```  
  
2.  以慣用的文字編輯器或 XML 編輯器建立一個檔案，然後將其儲存為 SampleSchema.xml。 將這個 XSD 結構描述加入到此檔案中。  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
     <xsd:annotation>  
       <xsd:appinfo>  
        <sql:relationship name="OrderOD"  
              parent="Ord"  
              parent-key="OrderID"  
              child="OrderDetail"  
              child-key="OrderID" />  
        <sql:relationship name="ODProduct"  
              parent="OrderDetail"  
              parent-key="ProductID"  
              child="Product"  
              child-key="ProductID"   
              inverse="true"/>  
       </xsd:appinfo>  
     </xsd:annotation>  
  
      <xsd:element name="Order" sql:relation="Ord"   
                                sql:key-fields="OrderID" >  
       <xsd:complexType>  
         <xsd:sequence>  
            <xsd:element name="Product" sql:relation="Product"   
                         sql:key-fields="ProductID"  
                         sql:relationship="OrderOD ODProduct">  
              <xsd:complexType>  
                 <xsd:attribute name="ProductID" type="xsd:int" />  
                 <xsd:attribute name="ProductName" type="xsd:string" />  
              </xsd:complexType>  
            </xsd:element>  
         </xsd:sequence>  
            <xsd:attribute name="OrderID"   type="xsd:integer" />   
            <xsd:attribute name="CustomerID"   type="xsd:string" />  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  以慣用的文字編輯器或 XML 編輯器建立一個檔案，然後將其儲存為 SampleXMLData.xml。 加入下列 XML 文件。  
  
    ```  
    <ROOT>    
      <Order OrderID="11" CustomerID="ALFKI">  
        <Product ProductID="11" ProductName="Chai" />  
        <Product ProductID="22" ProductName="Chang" />  
      </Order>  
      <Order OrderID="22" CustomerID="ANATR">  
         <Product ProductID="33" ProductName="Aniseed Syrup" />  
        <Product ProductID="44" ProductName="Gumbo Mix" />  
      </Order>  
    </ROOT>  
    ```  
  
4.  以慣用的文字編輯器或 XML 編輯器建立一個檔案，然後將其儲存為 ValidateAndBulkload.vbs。 將下列 VBScript 程式碼加入到此檔案中。 修改連接字串以提供適當的伺服器和資料庫名稱。 指定檔案做為參數的適當路徑**Execute**方法。  
  
    ```  
    Set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "C:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Transaction = False  
    objBL.KeepIdentity = False  
    objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
    Set objBL = Nothing  
    MsgBox "Done."  
    ```  
  
5.  執行 VBScript 程式碼。 XML 大量載入會將資料載入到適當的資料表中。  
  
## <a name="e-generating-table-schemas-before-bulk-loading"></a>E. 大量載入前產生資料表結構描述  
 如果大量載入前資料表不存在，XML 大量載入可以選擇性地產生資料表。 SchemaGen 屬性設定 SQLXMLBulkLoad 物件，則為 TRUE 會如此。 您可以選擇性地要求 XML 大量載入卸除任何現有的資料表，然後重新建立它們 SGDropTables 屬性設為 TRUE。 下列 VBScript 範例說明這些屬性的用法。  
  
 同時，此範例會將兩個額外的屬性設定為 TRUE：  
  
-   CheckConstraints。 將此屬性設定為 TRUE 可確保要插入資料表的資料沒有違反已經在資料表上指定的任何條件約束 (在此情況下為 Cust 和 CustOrder 資料表之間指定的 PRIMARY KEY/FOREIGN KEY 條件約束)。 如果有條件約束違規，大量載入便會失敗。  
  
-   XMLFragment。 此屬性必須設定為 TRUE，因為 XML 文件 (資料來源) 範例不包含單一的最上層元素 (因此為片段)。  
  
 這是 VBScript 程式碼：  
  
```  
Dim objBL   
Set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile = "c:\error.log"  
  
objBL.CheckConstraints=true  
objBL.XMLFragment = True  
objBL.SchemaGen = True  
objBL.SGDropTables = True  
  
objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
Set objBL = Nothing  
```  
  
#### <a name="to-test-a-working-sample"></a>測試工作範例  
  
1.  以慣用的文字編輯器或 XML 編輯器建立一個檔案，然後將其儲存為 SampleSchema.xml。 將稍早範例「使用結構描述中的鏈結關聯性大量載入 XML」中提供的 XSD 結構描述加入到檔案中。  
  
2.  以慣用的文字編輯器或 XML 編輯器建立一個檔案，然後將其儲存為 SampleXMLData.xml。 將稍早範例「使用結構描述中的鏈結關聯性大量載入 XML」中提供的 XML 文件加入到檔案中。 移除\<根 > 項目 （如果您要讓其成為片段） 的文件。  
  
3.  以慣用的文字編輯器或 XML 編輯器建立一個檔案，然後將其儲存為 ValidateAndBulkload.vbs。 將此範例中的 VBScript 程式碼加入到此檔案中。 修改連接字串以提供適當的伺服器和資料庫名稱。 指定適當的路徑，做為 Execute 方法的參數所指定的檔案。  
  
4.  執行 VBScript 程式碼。 XML 大量載入會根據所提供的對應結構描述建立所需的資料表，並在其中大量載入資料。  
  
## <a name="f-bulk-loading-from-a-stream"></a>F. 從資料流大量載入  
 XML 大量載入物件模型的 Execute 方法會採用兩個參數。 第一個參數是對應的結構描述檔案。 第二個參數會提供要載入到資料庫中的 XML 資料。 有兩種方式可將 XML 資料傳遞至 Execute 方法的 XML 大量載入：  
  
-   將檔案名稱指定為參數。  
  
-   傳遞包含 XML 資料的資料流。  
  
 此範例說明如何從資料流大量載入。  
  
 VBScript 會先執行 SELECT 陳述式，從 Northwind 資料庫的 Customers 資料表中擷取客戶資訊。 由於 FOR XML 子句是在 SELECT 陳述式中指定的 (利用 ELEMENTS 選項)，因此查詢會傳回此形式的元素中心 XML 文件：  
  
```  
<Customer>  
  <CustomerID>..</CustomerID>  
  <CompanyName>..</CompanyName>  
  <City>..</City>  
</Customer>  
...  
```  
  
 指令碼接著會傳遞 XML 做為資料流的 Execute 方法做為其第二個參數。 Execute 方法大量載入到 Cust 資料表的資料。  
  
 因為此指令碼會將 SchemaGen 屬性設為 TRUE 和 SGDropTables 屬性設定為 TRUE，XML 大量載入會在指定的資料庫中建立 Cust 資料表。 (如果此資料表已存在，它會先卸除資料表，然後再重新建立它)。  
  
 這是 VBScript 範例：  
  
```  
Set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
Set objCmd = CreateObject("ADODB.Command")  
Set objConn = CreateObject("ADODB.Connection")  
Set objStrmOut = CreateObject ("ADODB.Stream")  
  
objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile     = "c:\error.log"  
objBL.CheckConstraints = True  
objBL.SchemaGen        = True  
objBL.SGDropTables     = True  
objBL.XMLFragment      = True  
' Open a connection to the instance of SQL Server to get the source data.  
  
objConn.Open "provider=SQLOLEDB;server=(local);database=tempdb;integrated security=SSPI"  
Set objCmd.ActiveConnection = objConn  
objCmd.CommandText = "SELECT CustomerID, CompanyName, City FROM Customers FOR XML AUTO, ELEMENTS"  
  
' Open the return stream and execute the command.  
Const adCRLF = -1  
Const adExecuteStream = 1024  
objStrmOut.Open  
objStrmOut.LineSeparator = adCRLF  
objCmd.Properties("Output Stream").Value = objStrmOut  
objCmd.Execute , , adExecuteStream  
objStrmOut.Position = 0  
  
' Execute bulk load. Read source XML data from the stream.  
objBL.Execute "SampleSchema.xml", objStrmOut  
  
Set objBL = Nothing  
```  
  
 下列 XSD 對應結構描述會提供必要的資訊來建立資料表：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:element name="ROOT" sql:is-constant="true" >  
  <xsd:complexType>  
    <xsd:sequence>  
      <xsd:element ref="Customers"/>  
    </xsd:sequence>  
  </xsd:complexType>  
</xsd:element>  
<xsd:element name="Customers" sql:relation="Cust" >  
  <xsd:complexType>  
    <xsd:sequence>  
      <xsd:element name="CustomerID"  
                   type="xsd:string"  
                   sql:datatype="nvarchar(5)"/>  
      <xsd:element name="CompanyName"  
                   type="xsd:string"  
                   sql:datatype="nvarchar(40)"/>  
      <xsd:element name="City"  
                   type="xsd:string"  
                   sql:datatype="nvarchar(40)"/>  
    </xsd:sequence>  
  </xsd:complexType>  
</xsd:element>  
</xsd:schema>  
```  
  
 這是相等的 XDR 結構描述：  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust"  >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
    </ElementType>  
</Schema>  
```  
  
### <a name="opening-a-stream-on-an-existing-file"></a>開啟現有檔案上的資料流  
 您也可以開啟現有的 XML 資料檔上的資料流，並將資料流做為參數傳遞給 Execute 方法 （而不是做為參數傳遞的檔案名稱）。  
  
 這是將資料流當做參數傳遞的 Visual Basic 範例：  
  
```  
Private Sub Form_Load()  
Dim objBL As New SQLXMLBulkLoad  
Dim objStrm As New ADODB.Stream  
Dim objFileSystem As New Scripting.FileSystemObject  
Dim objFile As Scripting.TextStream  
  
MsgBox "Begin BulkLoad..."  
objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile = "c:\error.log"  
objBL.CheckConstraints = True  
objBL.SchemaGen = True  
objBL.SGDropTables = True  
' Here again a stream is specified that contains the source data   
' (instead of the file name). But this is just an illustration.  
' Usually this is useful if you have an XML data   
' stream that is created by some other means that you want to bulk   
' load. This example starts with an XML text file, so it may not be the   
' best to use a stream (you can specify the file name directly).  
' Here you could have specified the file name itself.   
Set objFile = objFileSystem.OpenTextFile("c:\SampleData.xml")  
objStrm.Open  
objStrm.WriteText objFile.ReadAll  
objStrm.Position = 0  
objBL.Execute "c:\SampleSchema.xml", objStrm  
  
Set objBL = Nothing  
MsgBox "Done."  
End Sub  
```  
  
 若要測試應用程式，請在此範例中提供的檔案 (SampleData.xml) 和 XSD 結構描述中使用下列 XML 文件：  
  
 這是 XML 來源資料 (SampleData.xml)：  
  
```  
<ROOT>  
  <Customers>  
    <CustomerID>1111</CustomerID>  
    <CompanyName>Hanari Carnes</CompanyName>  
    <City>NY</City>  
    <Order OrderID="1" />  
    <Order OrderID="2" />  
  </Customers>  
  
  <Customers>  
    <CustomerID>1112</CustomerID>  
    <CompanyName>Toms Spezialitten</CompanyName>  
     <City>LA</City>  
    <Order OrderID="3" />  
  </Customers>  
  <Customers>  
    <CustomerID>1113</CustomerID>  
    <CompanyName>Victuailles en stock</CompanyName>  
    <Order CustomerID= "4444" OrderID="4" />  
</Customers>  
</ROOT>  
```  
  
 這是相等的 XDR 結構描述：  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
  
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust"  >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
             <sql:relationship  
                key-relation="Cust"  
                key="CustomerID"  
                foreign-key="CustomerID"  
                foreign-relation="CustOrder" />  
      </element>  
   </ElementType>  
</Schema>  
```  
  
## <a name="g-bulk-loading-in-overflow-columns"></a>G. 大量載入溢位資料行  
 如果對應結構描述會使用指定的溢位資料行**sql: overflow-field-欄位**註釋，XML 大量載入將所有未耗用的資料從來源文件複製到此資料行。  
  
 請考慮使用這個 XSD 結構描述：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustCustOrder"  
          parent="Cust"  
          parent-key="CustomerID"  
          child="CustOrder"  
          child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  <xsd:element name="Customers" sql:relation="Cust"  
                                sql:overflow-field="OverflowColumn" >  
   <xsd:complexType>  
     <xsd:sequence>  
       <xsd:element name="CustomerID"  type="xsd:integer" />  
       <xsd:element name="CompanyName" type="xsd:string" />  
       <xsd:element name="City"        type="xsd:string" />  
       <xsd:element name="Order"   
                          sql:relation="CustOrder"  
                          sql:relationship="CustCustOrder" >  
         <xsd:complexType>  
          <xsd:attribute name="OrderID" type="xsd:integer" />  
          <xsd:attribute name="CustomerID" type="xsd:integer" />  
         </xsd:complexType>  
       </xsd:element>  
     </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 此結構描述會識別 Cust 資料表的溢位資料行 (OverflowColumn)。 如此一來，所有未 XML 資料消耗每 **\<客戶 >** 元素會加入至這個資料行。  
  
> [!NOTE]  
>  所有抽象元素 (其中的項目**抽象 ="true"** 指定) 以及所有禁止的屬性 (屬性**禁止 ="true"** 指定) 會被視為 XML 大量溢位負載和都加入至溢位資料行中，如果指定。 (否則便會予以忽略)。  
  
#### <a name="to-test-a-working-sample"></a>測試工作範例  
  
1.  建立兩個資料表中的**tempdb**資料庫：  
  
    ```  
    USE tempdb;  
    CREATE TABLE Cust (  
                  CustomerID     int         PRIMARY KEY,  
                  CompanyName    varchar(20) NOT NULL,  
                  City           varchar(20) DEFAULT 'Seattle',  
                  OverflowColumn nvarchar(200));  
    GO  
    CREATE TABLE CustOrder (  
                  OrderID    int PRIMARY KEY,  
                  CustomerID int FOREIGN KEY   
                                 REFERENCES Cust(CustomerID));  
    GO  
    ```  
  
2.  以慣用的文字編輯器或 XML 編輯器建立一個檔案，然後將其儲存為 SampleSchema.xml。 將這個範例所提供的 XSD 結構描述加入到此檔案中。  
  
3.  以慣用的文字編輯器或 XML 編輯器建立一個檔案，然後將其儲存為 SampleXMLData.xml。 將下列 XML 文件加入到此檔案中：  
  
    ```  
    <ROOT>  
      <Customers>  
        <CustomerID>1111</CustomerID>  
        <CompanyName>Hanari Carnes</CompanyName>  
        <City><![CDATA[NY]]> </City>  
        <Junk>garbage in overflow</Junk>  
        <Order OrderID="1" />  
        <Order OrderID="2" />  
      </Customers>  
  
      <Customers>  
        <CustomerID>1112</CustomerID>  
        <CompanyName>Toms Spezialitten</CompanyName>  
         <![CDATA[LA]]>   
        <!-- <xyz><address>111 Maple, Seattle</address></xyz>   -->  
        <Order OrderID="3" />  
      </Customers>  
      <Customers>  
        <CustomerID>1113</CustomerID>  
        <CompanyName>Victuailles en stock</CompanyName>  
        <Order OrderID="4" />  
    </Customers>  
    </ROOT>  
    ```  
  
4.  以慣用的文字編輯器或 XML 編輯器建立一個檔案，然後將其儲存為 ValidateAndBulkload.vbs。 將下列 Microsoft Visual Basic Scripting Edition (VBScript) 程式碼加入到此檔案中。 修改連接字串以提供適當的伺服器和資料庫名稱。 指定適當的路徑，做為 Execute 方法的參數所指定的檔案。  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
5.  執行 VBScript 程式碼。  
  
 這是相等的 XDR 結構描述：  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
  
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust"   
                       sql:overflow-field="OverflowColumn"  >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
             <sql:relationship  
                key-relation="Cust"  
                key="CustomerID"  
                foreign-key="CustomerID"  
                foreign-relation="CustOrder" />  
      </element>  
   </ElementType>  
</Schema>  
```  
  
## <a name="h-specifying-the-file-path-for-temp-files-in-transaction-mode"></a>H. 在交易模式下指定暫存檔案的檔案路徑  
 當您在交易模式下的大量載入 （也就是當交易屬性設定為 TRUE），您也必須設定 TempFilePath 屬性其中一個下列條件為 true 時：  
  
-   您要大量載入到遠端伺服器。  
  
-   您想要使用替代的本機磁碟或資料夾 (非 TEMP環境變數所指定的路徑) 來儲存交易模式下所建立的暫存檔案。  
  
 例如，下列 VBScript 程式碼會在交易模式下，將資料從 SampleXMLData.xml 檔大量載入到資料庫資料表。 TempFilePath 屬性會指定要設定在交易模式下產生的暫存檔案的路徑。  
  
```  
set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile = "c:\error.log"  
objBL.CheckConstraints = True  
objBL.Transaction=True  
objBL.TempFilePath="\\Server\MyDir"  
objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
set objBL=Nothing  
```  
  
> [!NOTE]  
>  暫存檔案路徑必須是一個共用位置，可存取 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 目標執行個體之服務帳戶以及執行大量載入應用程式的帳戶。 除非您是在本機伺服器上的大量載入時，暫存檔案路徑必須是 UNC 路徑 (例如\\\servername\sharename)。  
  
#### <a name="to-test-a-working-sample"></a>測試工作範例  
  
1.  建立這個資料表中的**tempdb**資料庫：  
  
    ```  
    USE tempdb;  
    CREATE TABLE Cust (     CustomerID uniqueidentifier,   
          LastName  varchar(20));  
    GO  
    ```  
  
2.  以慣用的文字編輯器或 XML 編輯器建立一個檔案，然後將其儲存為 SampleSchema.xml。 將下列 XSD 結構描述加入到此檔案中：  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
      <xsd:element name="ROOT" sql:is-constant="true" >  
        <xsd:complexType>  
          <xsd:sequence>  
            <xsd:element ref="Customers" />  
          </xsd:sequence>  
        </xsd:complexType>  
      </xsd:element>  
  
      <xsd:element name="Customers" sql:relation="Cust" >  
       <xsd:complexType>  
         <xsd:attribute name="CustomerID"  type="xsd:string" />  
         <xsd:attribute name="LastName" type="xsd:string" />  
       </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  以慣用的文字編輯器或 XML 編輯器建立一個檔案，然後將其儲存為 SampleXMLData.xml。 將下列 XML 文件加入到此檔案中：  
  
    ```  
    <ROOT>  
    <Customers CustomerID="6F9619FF-8B86-D011-B42D-00C04FC964FF"   
               LastName="Smith" />  
    </ROOT>  
    ```  
  
4.  以慣用的文字編輯器或 XML 編輯器建立一個檔案，然後將其儲存為 ValidateAndBulkload.vbs。 將下列 VBScript 程式碼加入到此檔案中。 修改連接字串以提供適當的伺服器和資料庫名稱。 指定適當的路徑，做為 Execute 方法的參數所指定的檔案。 也指定 TempFilePath 屬性的適當路徑。  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Transaction=True  
    objBL.TempFilePath="\\server\folder"  
    objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
5.  執行 VBScript 程式碼。  
  
     必須指定的結構描述對應**sql: datatype** for **CustomerID**屬性時的值**CustomerID**指定為包含大括號 （{GUID和}），例如：  
  
    ```  
    <ROOT>  
    <Customers CustomerID="{6F9619FF-8B86-D011-B42D-00C04FC964FF}"   
               LastName="Smith" />  
    </ROOT>  
    ```  
  
     這是更新的結構描述：  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
      <xsd:element name="ROOT" sql:is-constant="true" >  
        <xsd:complexType>  
          <xsd:sequence>  
            <xsd:element ref="Customers" />  
          </xsd:sequence>  
        </xsd:complexType>  
      </xsd:element>  
  
      <xsd:element name="Customers" sql:relation="Cust" >  
       <xsd:complexType>  
         <xsd:attribute name="CustomerID"  type="xsd:string"   
                        sql:datatype="uniqueidentifier" />  
         <xsd:attribute name="LastName" type="xsd:string" />  
       </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
     當**sql: datatype**會指定用來識別資料行類型為**uniqueidentifier**，在大量載入作業會移除大括號 （{和}） 從**CustomerID**值之前將其插入資料行中。  
  
 這是相等的 XDR 結構描述：  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
<ElementType name="ROOT" sql:is-constant="1">  
      <element type="Customers" />  
</ElementType>  
<ElementType name="Customers" sql:relation="Cust" >  
  <AttributeType name="CustomerID"  sql:datatype="uniqueidentifier" />  
  <AttributeType name="LastName"   />  
  
  <attribute type="CustomerID" />  
  <attribute type="LastName"   />  
</ElementType>  
</Schema>  
```  
  
## <a name="i-using-an-existing-database-connection-with-the-connectioncommand-property"></a>I. 搭配 ConnectionCommand 屬性使用現有的資料庫連接  
 您可以使用現有的 ADO 連接來大量載入 XML。 這在 XML 大量載入只是將在資料來源上執行之許多作業中的一個時相當實用。  
  
 ConnectionCommand 屬性可讓您透過 ADO 命令物件使用現有的 ADO 連接。 這會在下列 Visual Basic 範例中加以說明：  
  
```  
Private Sub Form_Load()  
Dim objBL As New SQLXMLBulkLoad4  
Dim objCmd As New ADODB.Command  
Dim objConn As New ADODB.Connection  
  
'Open a connection to an instance of SQL Server.  
objConn.Open "provider=SQLOLEDB;data source=(local);database=tempdb;integrated security=SSPI"  
'Ask the Command object to use the connection just established.  
Set objCmd.ActiveConnection = objConn  
  
'Tell Bulk Load to use the active command object that is using the Connection obj.  
objBL.ConnectionCommand = objCmd  
objBL.ErrorLogFile = "c:\error.log"  
objBL.CheckConstraints = True  
'The Transaction property must be set to True if you use ConnectionCommand.  
objBL.Transaction = True  
objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
Set objBL = Nothing  
End Sub  
```  
  
#### <a name="to-test-a-working-sample"></a>測試工作範例  
  
1.  建立兩個資料表中的**tempdb**資料庫：  
  
    ```  
    USE tempdb;  
    CREATE TABLE Cust(  
                   CustomerID   varchar(5) PRIMARY KEY,  
                   CompanyName  varchar(30),  
                   City         varchar(20));  
    GO  
    CREATE TABLE CustOrder(  
                   CustomerID  varchar(5) references Cust (CustomerID),  
                   OrderID     varchar(5) PRIMARY KEY);  
    GO  
    ```  
  
2.  以慣用的文字編輯器或 XML 編輯器建立一個檔案，然後將其儲存為 SampleSchema.xml。 將下列 XSD 結構描述加入到此檔案中：  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
    <xsd:annotation>  
      <xsd:appinfo>  
        <sql:relationship name="CustCustOrder"  
              parent="Cust"  
              parent-key="CustomerID"  
              child="CustOrder"  
              child-key="CustomerID" />  
      </xsd:appinfo>  
    </xsd:annotation>  
      <xsd:element name="ROOT" sql:is-constant="true" >  
        <xsd:complexType>  
          <xsd:sequence>  
            <xsd:element ref="Customers" />  
          </xsd:sequence>  
        </xsd:complexType>  
      </xsd:element>  
      <xsd:element name="Customers" sql:relation="Cust" >  
       <xsd:complexType>  
         <xsd:sequence>  
           <xsd:element name="CustomerID"  type="xsd:integer" />  
           <xsd:element name="CompanyName" type="xsd:string" />  
           <xsd:element name="City"        type="xsd:string" />  
           <xsd:element name="Order"   
                              sql:relation="CustOrder"  
                              sql:relationship="CustCustOrder" >  
             <xsd:complexType>  
              <xsd:attribute name="OrderID" type="xsd:integer" />  
              <xsd:attribute name="CustomerID" type="xsd:integer" />  
             </xsd:complexType>  
           </xsd:element>  
         </xsd:sequence>  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  以慣用的文字編輯器或 XML 編輯器建立一個檔案，然後將其儲存為 SampleXMLData.xml。 將下列 XML 文件加入到此檔案中：  
  
    ```  
    <ROOT>  
      <Customers>  
        <CustomerID>1111</CustomerID>  
        <CompanyName>Hanari Carnes</CompanyName>  
        <City>NY</City>  
        <Order OrderID="1" />  
        <Order OrderID="2" />  
      </Customers>  
  
      <Customers>  
        <CustomerID>1112</CustomerID>  
        <CompanyName>Toms Spezialitten</CompanyName>  
         <City>LA</City>  
        <Order OrderID="3" />  
      </Customers>  
      <Customers>  
        <CustomerID>1113</CustomerID>  
        <CompanyName>Victuailles en stock</CompanyName>  
        <Order OrderID="4" />  
    </Customers>  
    </ROOT>  
    ```  
  
4.  建立 Visual Basic (標準 EXE) 應用程式與之前的程式碼。 將這些參考加入到專案中：  
  
    ```  
    Microsoft XML BulkLoad for SQL Server 4.0 Type Library  
    Microsoft ActiveX Data objects 2.6 Library  
    ```  
  
5.  執行應用程式。  
  
 這是相等的 XDR 結構描述：  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust"  >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
         <sql:relationship  
                key-relation="Cust"  
                key="CustomerID"  
                foreign-key="CustomerID"  
                foreign-relation="CustOrder" />  
      </element>  
   </ElementType>  
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
</Schema>  
```  
  
## <a name="j-bulk-loading-in-xml-data-type-columns"></a>J. 大量載入到 xml 資料類型資料行  
 如果對應結構描述指定[xml 資料型別](../../../t-sql/xml/xml-transact-sql.md)使用的資料行**sql: datatype ="xml"** 註釋，XML 大量載入可以複製對應欄位的 XML 子元素的來源文件到這個資料行。  
  
 請考慮使用下列 XSD 結構描述，該結構描述會對應 AdventureWorks 範本資料庫中的 Production.ProductModel 資料表檢視。 下表中的 CatalogDescription 欄位**xml**資料類型對應至 **\<Desc >** 項目使用**sql: field**和**sql:資料類型 ="xml"** 註解。  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
           xmlns:sql="urn:schemas-microsoft-com:mapping-schema"  
           xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">   
  <xsd:element name="ProductModel"  sql:relation="Production.ProductModel" >  
    <xsd:complexType>  
      <xsd:sequence>  
        <xsd:element name="Name" type="xs:string"></xsd:element>  
        <xsd:element name="Desc" sql:field="CatalogDescription" sql:datatype="xml">  
        <xsd:complexType>  
          <xsd:sequence>  
            <xsd:element name="ProductDescription">  
              <xsd:complexType>  
                <xsd:sequence>  
                  <xsd:element name="Summary" type="xs:anyType"/>  
                </xsd:sequence>  
              </xsd:complexType>  
            </xsd:element>  
          </xsd:sequence>  
        </xsd:complexType>  
        </xsd:element>   
     </xsd:sequence>  
     <xsd:attribute name="ProductModelID" sql:field="ProductModelID" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
#### <a name="to-test-a-working-sample"></a>測試工作範例  
  
1.  確認已安裝 AdventureWorks 範例資料庫。  
  
2.  以慣用的文字編輯器或 XML 編輯器建立一個檔案，然後將其儲存為 SampleSchema.xml。 複製以上的 XSD 結構描述，並將其貼入檔案並加以儲存。  
  
3.  以慣用的文字編輯器或 XML 編輯器建立一個檔案，然後將其儲存為 SampleXMLData.xml。 複製下列 XML 文件，然後將其貼入檔案並儲存在先前步驟所使用的相同資料夾中。  
  
    ```  
    <ProductModel ProductModelID="2005">  
        <Name>Mountain-100 (2005 model)</Name>  
        <Desc><?xml-stylesheet href="ProductDescription.xsl" type="text/xsl"?>  
            <p1:ProductDescription xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
                  xmlns:wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"   
                  xmlns:wf="https://www.adventure-works.com/schemas/OtherFeatures"   
                  xmlns:html="http://www.w3.org/1999/xhtml"   
                  xmlns="">  
                <p1:Summary>  
                    <html:p>Our top-of-the-line competition mountain bike.   
          Performance-enhancing options include the innovative HL Frame,   
          super-smooth front suspension, and traction for all terrain.  
                            </html:p>  
                </p1:Summary>  
                <p1:Manufacturer>  
                    <p1:Name>AdventureWorks</p1:Name>  
                    <p1:Copyright>2002-2005</p1:Copyright>  
                    <p1:ProductURL>HTTP://www.Adventure-works.com</p1:ProductURL>  
                </p1:Manufacturer>  
                <p1:Features>These are the product highlights.   
                     <wm:Warranty>  
                        <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
                        <wm:Description>parts and labor</wm:Description>  
                    </wm:Warranty><wm:Maintenance>  
                        <wm:NoOfYears>10 years</wm:NoOfYears>  
                        <wm:Description>maintenance contract available through your dealer or any AdventureWorks retail store.</wm:Description>  
                    </wm:Maintenance><wf:wheel>High performance wheels.</wf:wheel><wf:saddle>  
                        <html:i>Anatomic design</html:i> and made from durable leather for a full-day of riding in comfort.</wf:saddle><wf:pedal>  
                        <html:b>Top-of-the-line</html:b> clipless pedals with adjustable tension.</wf:pedal><wf:BikeFrame>Each frame is hand-crafted in our Bothell facility to the optimum diameter   
          and wall-thickness required of a premium mountain frame.   
          The heat-treated welded aluminum frame has a larger diameter tube that absorbs the bumps.</wf:BikeFrame><wf:crankset> Triple crankset; alumunim crank arm; flawless shifting. </wf:crankset></p1:Features>  
                <!-- add one or more of these elements... one for each specific product in this product model -->  
                <p1:Picture>  
                    <p1:Angle>front</p1:Angle>  
                    <p1:Size>small</p1:Size>  
                    <p1:ProductPhotoID>118</p1:ProductPhotoID>  
                </p1:Picture>  
                <!-- add any tags in <specifications> -->  
                <p1:Specifications> These are the product specifications.  
                       <Material>Almuminum Alloy</Material><Color>Available in most colors</Color><ProductLine>Mountain bike</ProductLine><Style>Unisex</Style><RiderExperience>Advanced to Professional riders</RiderExperience></p1:Specifications>  
            </p1:ProductDescription>  
        </Desc>  
    </ProductModel>  
    ```  
  
4.  以慣用的文字編輯器或 XML 編輯器建立一個檔案，然後將其儲存為 BulkloadXml.vbs。 複製下列 VBScript 程式碼，並將其貼入檔案。 將其儲存在先前 XML 資料和結構描述檔案所使用的相同資料夾中。  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=MyServer;database=AdventureWorks;integrated security=SSPI"  
  
    Dim fso, sAppPath  
    Set fso = CreateObject("Scripting.FileSystemObject")   
    sAppPath = fso.GetFolder(".")   
  
    objBL.ErrorLogFile = sAppPath & "\error.log"  
  
    'Execute XML bulkload using file.  
    objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
5.  執行 BulkloadXml.vbs 指令碼。  
  
  
