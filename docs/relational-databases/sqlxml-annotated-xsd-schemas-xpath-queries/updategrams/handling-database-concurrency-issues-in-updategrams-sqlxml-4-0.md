---
title: Updategram (SQLXML) 中的資料庫並行問題
description: 瞭解如何使用 updategram (SQLXML 4.0) 中的開放式並行存取控制機制來處理資料庫平行存取問題。
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- <before> block
- low concurrency protection
- database concurrency [SQLXML]
- timestamp column [SQLXML]
- updategrams [SQLXML], database concurrency
- high concurrency protection [SQLXML]
- optimistic concurrency control
- concurrency [SQLXML]
- intermediate concurrency protection [SQLXML]
ms.assetid: d4b908d1-b25b-4ad9-8478-9cd882e8c44e
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0f7c39eac7fc19d9f35c800f71ac874159fe284b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479199"
---
# <a name="handling-database-concurrency-issues-in-updategrams-sqlxml-40"></a>在 Updategram (SQLXML 4.0) 中處理資料庫並行的問題
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  與其他資料庫更新機制一樣，Updategram 必須處理在多使用者環境中的資料並行更新。 Updategram 使用開放式並行控制，該控制使用選取欄位資料的比較為快照集，以確保自從要更新的資料從資料庫讀取後，尚未受到其他使用者應用程式改變。 Updategram 會將這些快照集值包含在 **\<before>** updategram 的區塊中。 更新資料庫之前，updategram 會 **\<before>** 根據目前在資料庫中的值來檢查區塊中指定的值，以確保更新有效。  
  
 開放式並行控制在 Updategram 中提供三種保護等級：低 (無)、中和高。 您可以藉由指定 Updategram，決定需要哪種保護等級。  
  
## <a name="lowest-level-of-protection"></a>最低保護等級  
 這個等級是一種盲目更新 (Blind Update)，在這個等級中，會直接處理更新，而不會參考自從上一次讀取資料庫之後所做的其他更新。 在這種情況下，您只需要在區塊中指定主鍵資料行 (s) **\<before>** 來識別記錄，並在區塊中指定更新的資訊 **\<after>** 。  
  
 例如，在下列的 Updategram 中的新連絡電話號碼是正確的，無論之前的電話號碼是幾號。 請注意， **\<before>** 區塊只會指定主鍵資料行 (ContactID) 。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
   <Person.Contact ContactID="1" />  
</updg:before>  
<updg:after>  
   <Person.Contact ContactID="1" Phone="111-111-1111" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
## <a name="intermediate-level-of-protection"></a>中級保護等級  
 在這個保護等級中，Updategram 會比較使用資料庫資料行中的值所更新的目前值，以確定自從您的交易讀取記錄之後，值沒有受到其他交易改變。  
  
 您可以藉由指定主鍵資料行 (s) ，以及您要在區塊中更新的資料行 () ，來取得此層級的保護 **\<before>** 。  
  
 例如，這個 Updategram 為 ContactID 為 1 的連絡人，變更了 Person.Contact 資料表 Phone 資料行中的值。 **\<before>** 區塊會指定 **Phone** 屬性，以確保此屬性值符合資料庫中對應資料行的值，然後再套用更新的值。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
   <Person.Contact ContactID="1" Phone="398-555-0132" />  
</updg:before>  
<updg:after>  
   <Person.Contact ContactID="1" Phone="111-111-1111" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
## <a name="high-level-of-protection"></a>高級保護等級  
 一種高級保護等級，可以確定記錄自從您的應用程式上次讀取之後是維持原狀的 (也就是說，自從您的應用程式讀取記錄後，該記錄尚未由其他交易改變)。  
  
 您可以藉由兩種方法，針對並行更新取得這個保護等級：  
  
-   在區塊中指定資料表中的其他 **\<before>** 資料行。  
  
     如果您在區塊中指定其他 **\<before>** 資料行，updategram 會比較這些資料行所指定的值與資料庫中的值，然後再套用更新。 如果任何記錄資料行在您的交易讀取記錄之後變更的話，則 Updategram 不會執行更新。  
  
     例如，下列 updategram 會更新 shift 名稱，但會指定額外的資料行 (StartTime、EndTime) 在 **\<before>** 區塊中，藉此針對並行更新要求更高的保護層級。  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
    <updg:sync >  
    <updg:before>  
       <HumanResources.Shift ShiftID="1"   
                 Name="Day"   
                 StartTime="1900-01-01 07:00:00.000"   
                 EndTime="1900-01-01 15:00:00.000" />  
    </updg:before>  
    <updg:after>  
       <HumanResources.Shift Name="Morning" />  
    </updg:after>  
    </updg:sync>  
    </ROOT>  
    ```  
  
     這個範例會指定區塊中記錄的所有資料行值，藉以指定最高層級的保護 **\<before>** 。  
  
-   如果區塊中有可用的) ，請指定時間戳記資料行 (**\<before>** 。  
  
     除了指定 * * 區塊中的所有記錄資料行之外 \<before**> ，您只可以指定時間戳記資料行 (如果資料表有一個) ，以及區塊中) 的主鍵資料行 (**\<before>** 。 資料庫會在每一筆記錄更新後，將時間戳記資料行更新為唯一值。 在這個狀況下，Updategram 會比較時間戳記值與資料庫中對應的值。 儲存在資料庫中的時間戳記值是二進位值。 因此，時間戳記資料行必須在架構中指定為 **dt： type = "bin. hex"**、 **dt： type = "bin. base64"** 或 **sql： datatype = "timestamp"**。  (您可以指定 **xml** 資料類型或 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。 )   
  
#### <a name="to-test-the-updategram"></a>若要測試 Updategram  
  
1.  在 **tempdb** 資料庫中建立此資料表：  
  
    ```  
    USE tempdb  
    CREATE TABLE Customer (  
                 CustomerID  varchar(5),  
                 ContactName varchar(20),  
                 LastUpdated timestamp)  
    ```  
  
2.  新增這個範例記錄：  
  
    ```  
    INSERT INTO Customer (CustomerID, ContactName) VALUES   
                         ('C1', 'Andrew Fuller')  
    ```  
  
3.  複製下列 XSD 結構描述並貼到 [記事本] 中， 將它儲存為 ConcurrencySampleSchema.xml：  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
      <xsd:element name="Customer" sql:relation="Customer" >  
       <xsd:complexType>  
            <xsd:attribute name="CustomerID"    
                           sql:field="CustomerID"   
                           type="xsd:string" />   
  
            <xsd:attribute name="ContactName"    
                           sql:field="ContactName"   
                           type="xsd:string" />  
  
            <xsd:attribute name="LastUpdated"   
                           sql:field="LastUpdated"   
                           type="xsd:hexBinary"   
                 sql:datatype="timestamp" />  
  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
4.  複製下列 Updategram 程式碼並貼到 [記事本] 中，然後將它儲存為 ConcurrencySampleTemplate.xml 並放在與前一個步驟中所建立的結構描述一樣的目錄中。 (請注意，以下 LastUpdated 的時間戳記值與您的範例 Customer 資料表中的值不同，所以請從資料表複製 LastUpdated 的實際值，並貼至 Updategram 中)。  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
    <updg:sync mapping-schema="SampleSchema.xml" >  
    <updg:before>  
       <Customer CustomerID="C1"   
                 LastUpdated = "0x00000000000007D1" />  
    </updg:before>  
    <updg:after>  
       <Customer ContactName="Robert King" />  
    </updg:after>  
    </updg:sync>  
    </ROOT>  
    ```  
  
5.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱 [使用 ADO 執行 SQLXML 4.0 查詢](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 這是相等的 XDR 結構描述：  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<ElementType name="Customer" sql:relation="Customer" >  
    <AttributeType name="CustomerID" />  
    <AttributeType name="ContactName" />  
    <AttributeType name="LastUpdated"  dt:type="bin.hex"   
                                       sql:datatype="timestamp" />  
    <attribute type="CustomerID" />  
    <attribute type="ContactName" />  
    <attribute type="LastUpdated" />  
</ElementType>  
</Schema>  
```  
  
## <a name="see-also"></a>另請參閱  
 [Updategram &#40;SQLXML 4.0&#41;的安全性考慮 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
