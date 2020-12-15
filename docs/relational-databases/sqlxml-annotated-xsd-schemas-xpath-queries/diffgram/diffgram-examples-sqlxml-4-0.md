---
title: " (SQLXML) 的 DiffGram 範例"
description: 在 SQLXML 4.0 中查看對資料庫執行插入、更新和刪除作業的 diffgram 範例。
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], examples
- examples [SQLXML], DiffGram
- diffgr:parentID
- parentID annotation
ms.assetid: fc148583-dfd3-4efb-a413-f47b150b0975
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c4681c4babe25ec9c683d78e583ddd2c1a4d91fe
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97415217"
---
# <a name="diffgram-examples-sqlxml-40"></a>DiffGram 範例 (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
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
  
 在 **\<before>** 區塊中，有一個 **\<Order>** 元素 (**diffgr： Id = "Order1"**) 和 **\<Customer>** (**diffgr： id = "Customer1"**) 的元素。 這些項目代表資料庫中的現有記錄。 **\<DataInstance>** 元素沒有對應的記錄 (具有相同的 **diffgr： id**) 。 這表示刪除作業。  
  
#### <a name="to-test-the-diffgram"></a>若要測試 DiffGram  
  
1.  在 **tempdb** 資料庫中建立這些資料表。  
  
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
         (N'ANTON', N'Antonio Moreno Taquería', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  複製上述的 DiffGram，並將其貼到文字檔中。 然後將檔案儲存為 MyDiffGram.xml，放在前述步驟所使用的相同資料夾中。  
  
4.  複製本主題稍早所提供的 DiffGramSchema，並將它貼到文字檔中。 然後將檔案儲存為 DiffGramSchema.xml。  
  
5.  建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 來執行 DiffGram。  
  
     如需詳細資訊，請參閱 [使用 ADO 執行 SQLXML 4.0 查詢](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
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
  
 在這個 DiffGram 中， **\<before>** 不會指定區塊 () 找不到任何現有的資料庫記錄。 有兩個記錄實例 (由 **\<Customer>** **\<Order>**) 區塊中的和元素所識別，而這些專案 **\<DataInstance>** 分別對應至 [加入] 和 [Ord] 資料表。 這兩個元素都會指定 **diffgr： hasChanges** 屬性 (**hasChanges = "插入"**) 。 這表示插入作業。 在這個 DiffGram 中，如果您指定 **hasChanges = "modified"**，就表示您想要修改不存在的記錄，這會導致錯誤。  
  
#### <a name="to-test-the-diffgram"></a>若要測試 DiffGram  
  
1.  在 **tempdb** 資料庫中建立這些資料表。  
  
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
         (N'ANTON', N'Antonio Moreno Taquería', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  複製上述的 DiffGram，並將其貼到文字檔中。 然後將檔案儲存為 MyDiffGram.xml，放在前述步驟所使用的相同資料夾中。  
  
4.  複製本主題稍早所提供的 DiffGramSchema，並將它貼到文字檔中。 然後將檔案儲存為 DiffGramSchema.xml。  
  
5.  建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 來執行 DiffGram。  
  
     如需詳細資訊，請參閱 [使用 ADO 執行 SQLXML 4.0 查詢](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
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
  
 **\<before>** 區塊包含 **\<Customer>** 元素 (**diffgr： Id = "Customer1"**) 。 **\<DataInstance>** 區塊包含 **\<Customer>** 具有相同 **識別碼** 的對應元素。**\<customer>** 中的元素 **\<NewDataSet>** 也會指定 **diffgr： hasChanges = "modified"**。 這表示更新作業，而 **customer 資料表中的客戶** 記錄也會隨之更新。 請注意，如果未指定 **diffgr： hasChanges** 屬性，DiffGram 處理邏輯會忽略這個元素，而且不會執行任何更新。  
  
#### <a name="to-test-the-diffgram"></a>若要測試 DiffGram  
  
1.  在 **tempdb** 資料庫中建立這些資料表。  
  
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
         (N'ANTON', N'Antonio Moreno Taquería', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  複製上述的 DiffGram，並將其貼到文字檔中。 然後將檔案儲存為 MyDiffGram.xml，放在前述步驟所使用的相同資料夾中。  
  
4.  複製本主題稍早所提供的 DiffGramSchema，並將它貼到文字檔中。 然後將檔案儲存為 DiffGramSchema.xml。  
  
5.  建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 來執行 DiffGram。  
  
     如需詳細資訊，請參閱 [使用 ADO 執行 SQLXML 4.0 查詢](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
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
  
-   根據 DiffGram 處理邏輯，區塊中的所有最上層元素都會 **\<before>** 對應至對應的資料表，如對應架構中所述。  
  
-   **\<before>** 區塊具有 **\<Order>** (**dffgr： Id = "Order1"**) 的元素，以及 **\<Customer>** (**diffgr： id = "Customer1"**) 的元素，但區塊 (中沒有對應的元素 **\<DataInstance>**) 具有相同的識別碼。 這表示刪除作業，而且會從 Cust 和 Ord 資料表中刪除記錄。  
  
-   **\<before>** 區塊具有 **\<Customer>** (**diffgr： Id = "Customer2"**) 的元素，而 **\<Customer>** 區塊 (中有對應的元素 **\<DataInstance>**) 具有相同的識別碼。 區塊中的元素會 **\<DataInstance>** 指定 **Diffgr： hasChanges = "modified"**。 這是針對客戶 ANATR 的更新作業，會使用在區塊中指定的值，在 customer 資料表中更新公司名稱和連絡人資訊 **\<DataInstance>** 。  
  
-   **\<DataInstance>** 區塊具有 **\<Customer>** (**diffgr： Id = "Customer3"**) 的元素，以及 **\<Order>** (**diffgr： id = "Order3"**) 的元素。 這些元素都不會指定 **diffgr： hasChanges** 屬性。 因此，DiffGram 處理邏輯會忽略這些元素。  
  
-   **\<DataInstance>** 區塊具有 **\<Customer>** (**diffgr： Id = "Customer4"**) 的元素，以及 **\<Order>** (**diffgr： id = "Order4"**) 的元素，但區塊中沒有對應的元素 \<before> 。 區塊中的這些元素會 **\<DataInstance>** 指定 **Diffgr： hasChanges = "插入"**。 因此，新的記錄會加入 Cust 資料表和 Ord 資料表中。  
  
#### <a name="to-test-the-diffgram"></a>若要測試 DiffGram  
  
1.  在 **tempdb** 資料庫中建立下列資料表。  
  
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
         (N'ANTON', N'Antonio Moreno Taquería', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  複製上述的 DiffGram，並將其貼到文字檔中。 然後將檔案儲存為 MyDiffGram.xml，放在前述步驟所使用的相同資料夾中。  
  
4.  複製本主題稍早所提供的 DiffGramSchema，並將它貼到文字檔中。 然後將檔案儲存為 DiffGramSchema.xml。  
  
5.  建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 來執行 DiffGram。  
  
     如需詳細資訊，請參閱 [使用 ADO 執行 SQLXML 4.0 查詢](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
## <a name="e-applying-updates-by-using-a-diffgram-with-the-diffgrparentid-annotation"></a>E. 搭配 diffgr:parentID 註解使用 DiffGram 來套用更新  
 此範例說明如何在套用 **\<before>** 更新時使用 DiffGram 的區塊中指定的 parentID 批註。  
  
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
  
 這項 DiffGram 會指定刪除作業，因為只有一個 **\<before>** 區塊。 在 DiffGram 中， **parentID** 批註是用來指定訂單與訂單詳細資料之間的父子式關聯性。 當 SQLXML 刪除記錄時，它會從這個關聯性所識別的子資料表中刪除記錄，然後從對應的父資料表中刪除記錄。  
  
  
