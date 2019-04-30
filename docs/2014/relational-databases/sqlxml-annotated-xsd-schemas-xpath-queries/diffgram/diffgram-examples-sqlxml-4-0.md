---
title: DiffGram 範例 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], examples
- examples [SQLXML], DiffGram
- diffgr:parentID
- parentID annotation
ms.assetid: fc148583-dfd3-4efb-a413-f47b150b0975
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ed354e6b72f66908c12e1254738df75008659f8d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127729"
---
# <a name="diffgram-examples-sqlxml-40"></a>DiffGram 範例 (SQLXML 4.0)
  本主題的範例是由 DiffGram 所組成，DiffGram 會針對資料庫執行插入、更新和刪除作業。 在使用範例之前，請注意下列事項：  
  
-   如果您想要測試 DiffGram 範例，範例中會使用兩個必須建立的資料表 (Cust 和 Ord)：  
  
    ```  
    Cust(CustomerID, CompanyName, ContactName)  
    Ord(OrderID, CustomerID)  
    ```  
  
-   本主題的大多數範例都會使用以下 XSD 結構描述：  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
    <xsd:annotation>  
      <xsd:documentation>  
        Diffgram Customers/Orders Schema.  
      </xsd:documentation>  
      <xsd:appinfo>  
           <sql:relationship name="CustomersOrders"   
                      parent="Cust"  
                      parent-key="CustomerID"  
                      child-key="CustomerID"  
                      child="Ord"/>  
      </xsd:appinfo>  
    </xsd:annotation>  
  
    <xsd:element name="Customer" sql:relation="Cust">  
      <xsd:complexType>  
        <xsd:sequence>  
          <xsd:element name="CompanyName"    type="xsd:string"/>  
          <xsd:element name="ContactName"    type="xsd:string"/>  
           <xsd:element name="Order" sql:relation="Ord" sql:relationship="CustomersOrders">  
            <xsd:complexType>  
              <xsd:attribute name="OrderID" type="xsd:int" sql:field="OrderID"/>  
              <xsd:attribute name="CustomerID" type="xsd:string"/>  
            </xsd:complexType>  
          </xsd:element>  
        </xsd:sequence>  
        <xsd:attribute name="CustomerID" type="xsd:string" sql:field="CustomerID"/>  
      </xsd:complexType>  
    </xsd:element>  
  
    </xsd:schema>     
    ```  
  
     請將這個結構描述儲存為 DiffGramSchema.xml，並放在您想要儲存範例中使用之其他檔案的相同資料夾內。  
  
## <a name="a-deleting-a-record-by-using-a-diffgram"></a>A. 使用 DiffGram 刪除記錄  
 此範例中的 DiffGram 會從 Cust 資料表中刪除客戶 (CustomerID 為 ALFKI) 記錄，並從 Ord 資料表中刪除對應的訂單記錄 (OrderID 為 1)。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
           xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
           xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance/>  
  
    <diffgr:before>  
        <Order diffgr:id="Order1"   
               msdata:rowOrder="0"   
               CustomerID="ALFKI"   
               OrderID="1"/>  
        <Customer diffgr:id="Customer1"   
                  msdata:rowOrder="0"   
                  CustomerID="ALFKI">  
           <CompanyName>Alfreds Futterkiste</CompanyName>  
           <ContactName>Maria Anders</ContactName>  
        </Customer>  
    </diffgr:before>  
    <msdata:errors/>  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 在  **\<之前 >** 區塊中，有 **\<順序 >** 項目 (**diffgr: id ="Diffgr:id="order1"**) 和 **\<客戶 >** 項目 (**diffgr: id ="Customer1"**)。 這些項目代表資料庫中的現有記錄。 **\<DataInstance >** 項目沒有對應的記錄 (具有相同**diffgr: id**)。 這表示刪除作業。  
  
#### <a name="to-test-the-diffgram"></a>若要測試 DiffGram  
  
1.  建立這些資料表中的**tempdb**資料庫。  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
2.  加入這個範例資料：  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquer??a', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  複製上述的 DiffGram，並將其貼到文字檔中。 然後將檔案儲存為 MyDiffGram.xml，放在前述步驟所使用的相同資料夾中。  
  
4.  複製本主題稍早所提供的 DiffGramSchema，並將它貼到文字檔中。 然後將檔案儲存為 DiffGramSchema.xml。  
  
5.  建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 來執行 DiffGram。  
  
     如需詳細資訊，請參閱 <<c0> [ 使用 ADO 執行 SQLXML 4.0 查詢](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
## <a name="b-inserting-a-record-by-using-a-diffgram"></a>B. 使用 DiffGram 插入記錄  
 在此範例中，DiffGram 會在 Cust 資料表中插入記錄，並在 Ord 資料表中插入記錄。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql"   
      sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
          xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
          xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
       <Customer diffgr:id="Customer1" msdata:rowOrder="0"    
                 diffgr:hasChanges="inserted" CustomerID="ALFKI">  
        <CompanyName>C3Company</CompanyName>  
        <ContactName>C3Contact</ContactName>  
        <Order diffgr:id="Order1"   
               msdata:rowOrder="0"  
               diffgr:hasChanges="inserted"   
               CustomerID="ALFKI" OrderID="1"/>  
      </Customer>  
    </DataInstance>  
  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 在這個 DiffGram **\<之前 >** 並未指定區塊 （任何現有的資料庫識別的記錄）。 有兩個記錄的執行個體 (由**\<客戶 >** 並 **\<順序 >** 中的項目 **\<DataInstance >** 區塊)，分別對應到 Cust 和 Ord 資料表。 這兩個項目指定**diffgr: haschanges**屬性 (**hasChanges ="inserted"**)。 這表示插入作業。 在這個 DiffGram 中，如果您指定**hasChanges ="modified"**，即表示您想要修改的記錄不存在，會導致錯誤。  
  
#### <a name="to-test-the-diffgram"></a>若要測試 DiffGram  
  
1.  建立這些資料表中的**tempdb**資料庫。  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
2.  加入這個範例資料：  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquer??a', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  複製上述的 DiffGram，並將其貼到文字檔中。 然後將檔案儲存為 MyDiffGram.xml，放在前述步驟所使用的相同資料夾中。  
  
4.  複製本主題稍早所提供的 DiffGramSchema，並將它貼到文字檔中。 然後將檔案儲存為 DiffGramSchema.xml。  
  
5.  建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 來執行 DiffGram。  
  
     如需詳細資訊，請參閱 <<c0> [ 使用 ADO 執行 SQLXML 4.0 查詢](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
## <a name="c-updating-an-existing-record-by-using-a-diffgram"></a>C. 使用 DiffGram 來更新現有的記錄  
 在此範例中，DiffGram 會更新客戶 ALFKI 的客戶資訊 (CompanyName 和 ContactName)。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
           xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
           xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
      <Customer diffgr:id="Customer1"   
                msdata:rowOrder="0" diffgr:hasChanges="modified"   
                CustomerID="ALFKI">  
          <CompanyName>Bottom Dollar Markets</CompanyName>  
          <ContactName>Antonio Moreno</ContactName>  
      </Customer>  
    </DataInstance>  
  
    <diffgr:before>  
     <Customer diffgr:id="Customer1"   
               msdata:rowOrder="0"   
               CustomerID="ALFKI">  
        <CompanyName>Alfreds Futterkiste</CompanyName>  
        <ContactName>Maria Anders</ContactName>  
      </Customer>  
    </diffgr:before>  
  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 **\<之前 >** 區塊包含 **\<客戶 >** 項目 (**diffgr: id ="Customer1"**)。 **\<DataInstance >** 區塊包含對應 **\<客戶 >** 具有相同的項目 **識別碼**。**\<客戶 >** 中的項目 **\<NewDataSet >** 也會指定 **diffgr: haschanges ="modified"**。 這表示更新作業，而且中的客戶記錄**Cust**資料表會隨之更新。 請注意，如果**diffgr: haschanges**未指定屬性，DiffGram 處理邏輯會忽略這個項目會執行任何更新。  
  
#### <a name="to-test-the-diffgram"></a>若要測試 DiffGram  
  
1.  建立這些資料表中的**tempdb**資料庫。  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
2.  加入這個範例資料：  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquer??a', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  複製上述的 DiffGram，並將其貼到文字檔中。 然後將檔案儲存為 MyDiffGram.xml，放在前述步驟所使用的相同資料夾中。  
  
4.  複製本主題稍早所提供的 DiffGramSchema，並將它貼到文字檔中。 然後將檔案儲存為 DiffGramSchema.xml。  
  
5.  建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 來執行 DiffGram。  
  
     如需詳細資訊，請參閱 <<c0> [ 使用 ADO 執行 SQLXML 4.0 查詢](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
## <a name="d-inserting-updating-and-deleting-records-by-using-a-diffgram"></a>D. 使用 DiffGram 來插入、更新及刪除記錄  
 這個範例中會使用相對複雜的 DiffGram 來執行插入、更新和刪除作業。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
         xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
         xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
      <Customer diffgr:id="Customer2" msdata:rowOrder="1"   
                diffgr:hasChanges="modified"   
                CustomerID="ANATR">  
          <CompanyName>Bottom Dollar Markets</CompanyName>  
          <ContactName>Elizabeth Lincoln</ContactName>  
          <Order diffgr:id="Order2" msdata:rowOrder="1"   
               msdata:hiddenCustomerID="ANATR"   
               CustomerID="ANATR" OrderID="2"/>  
      </Customer>  
  
      <Customer diffgr:id="Customer3" msdata:rowOrder="2"   
                CustomerID="ANTON">  
         <CompanyName>Chop-suey Chinese</CompanyName>  
         <ContactName>Yang Wang</ContactName>  
         <Order diffgr:id="Order3" msdata:rowOrder="2"   
               msdata:hiddenCustomerID="ANTON"   
               CustomerID="ANTON" OrderID="3"/>  
      </Customer>  
      <Customer diffgr:id="Customer4" msdata:rowOrder="3"   
                diffgr:hasChanges="inserted"   
                CustomerID="AROUT">  
         <CompanyName>Around the Horn</CompanyName>  
         <ContactName>Thomas Hardy</ContactName>  
         <Order diffgr:id="Order4" msdata:rowOrder="3"   
                diffgr:hasChanges="inserted"   
                msdata:hiddenCustomerID="AROUT"   
               CustomerID="AROUT" OrderID="4"/>  
      </Customer>  
    </DataInstance>  
    <diffgr:before>  
      <Order diffgr:id="Order1" msdata:rowOrder="0"   
             msdata:hiddenCustomerID="ALFKI"   
             CustomerID="ALFKI" OrderID="1"/>  
      <Customer diffgr:id="Customer1" msdata:rowOrder="0"   
                CustomerID="ALFKI">  
        <CompanyName>Alfreds Futterkiste</CompanyName>  
        <ContactName>Maria Anders</ContactName>  
      </Customer>  
      <Customer diffgr:id="Customer2" msdata:rowOrder="1"   
                CustomerID="ANATR">  
        <CompanyName>Ana Trujillo Emparedados y helados</CompanyName>  
        <ContactName>Ana Trujillo</ContactName>  
      </Customer>  
    </diffgr:before>  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 DiffGram 邏輯會處理這個 DiffGram，如下所示：  
  
-   根據 DiffGram 處理邏輯，在最上層的項目**\<之前 >** 封鎖對應至對應的資料表，因為對應結構描述中所述。  
  
-   **\<之前 >** 區塊**\<順序 >** 項目 (**dffgr:id ="Diffgr:id="order1"**)， **\<客戶>** 項目 (**diffgr: id ="Customer1 」**) 包括不在沒有對應的項目 **\<DataInstance >** （具有相同的識別碼） 的區塊。 這表示刪除作業，而且會從 Cust 和 Ord 資料表中刪除記錄。  
  
-   **\<之前 >** 區塊**\<客戶 >** 項目 (**diffgr: id ="Customer2"**) 包括不對應**\<客戶 >** 中的項目 **\<DataInstance >** （具有相同的識別碼） 的區塊。 中的項目 **\<DataInstance >** 區塊指定**diffgr: haschanges ="modified"**。 這是更新作業，對客戶 anatr 而言，在使用中所指定的值在 Cust 資料表中更新 CompanyName 和 ContactName 資訊 **\<DataInstance >** 區塊。  
  
-    **\<DataInstance >** 區塊**\<客戶 >** 項目 (**diffgr: id ="Customer3"**) 和 **\<順序 >** 項目 (**diffgr: id ="Order3"**)。 這些項目都不指定**diffgr: haschanges**屬性。 因此，DiffGram 處理邏輯會忽略這些元素。  
  
-    **\<DataInstance >** 區塊**\<客戶 >** 項目 (**diffgr: id ="Diffgr:id="customer4"**) 和 **\<順序 >** 項目 (**diffgr: id ="Diffgr:id="order4"**) 的其中有中的沒有對應項目\<之前 > 區塊。 在這些項目 **\<DataInstance >** 區塊指定**diffgr: haschanges ="inserted"**。 因此，新的記錄會加入 Cust 資料表和 Ord 資料表中。  
  
#### <a name="to-test-the-diffgram"></a>若要測試 DiffGram  
  
1.  建立下列資料表中的**tempdb**資料庫。  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
2.  加入這個範例資料：  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquer??a', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  複製上述的 DiffGram，並將其貼到文字檔中。 然後將檔案儲存為 MyDiffGram.xml，放在前述步驟所使用的相同資料夾中。  
  
4.  複製本主題稍早所提供的 DiffGramSchema，並將它貼到文字檔中。 然後將檔案儲存為 DiffGramSchema.xml。  
  
5.  建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 來執行 DiffGram。  
  
     如需詳細資訊，請參閱 <<c0> [ 使用 ADO 執行 SQLXML 4.0 查詢](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
## <a name="e-applying-updates-by-using-a-diffgram-with-the-diffgrparentid-annotation"></a>E. 搭配 diffgr:parentID 註解使用 DiffGram 來套用更新  
 此範例說明如何**parentID** 中指定的註釋 **\<之前 >** DiffGram 的區塊會在套用更新。  
  
```  
<NewDataSet />  
<diffgr:before>  
   <Order diffgr:id="Order1" msdata:rowOrder="0" OrderID="2" />  
   <Order diffgr:id="Order3" msdata:rowOrder="2" OrderID="4" />  
  
   <OrderDetail diffgr:id="OrderDetail1"   
                diffgr:parentId="Order1"   
                msdata:rowOrder="0"   
                ProductID="13"   
                OrderID="2" />  
   <OrderDetail diffgr:id="OrderDetail3"   
                diffgr:parentId="Order3"  
                ProductID="77"  
                OrderID="4"/>  
</diffgr:before>  
</diffgr:diffgram>  
```  
  
 這個 DiffGram 會指定刪除作業，因為只會有**\<之前 >** 區塊。 在此 DiffGram 中， **parentID**註解用來指定訂單與訂單詳細資料之間的父子式關聯性。 當 SQLXML 刪除記錄時，它會從這個關聯性所識別的子資料表中刪除記錄，然後從對應的父資料表中刪除記錄。  
  
  
