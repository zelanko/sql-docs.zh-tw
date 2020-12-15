---
title: XML 大量載入 (SQLXML) 的指導方針和限制
description: 瞭解在 SQLXML 4.0 中使用 XML 大量載入的指導方針和限制。
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XML Bulk Load [SQLXML], about XML Bulk Load
- bulk load [SQLXML], about bulk load
ms.assetid: c5885d14-c7c1-47b3-a389-455e99a7ece1
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b17b1990f168326ae884b4db4f1ff22a63b24e21
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97439680"
---
# <a name="guidelines-and-limitations-of-xml-bulk-load-sqlxml-40"></a>XML 大量載入的指導方針和限制 (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  當您使用 XML 大量載入時，應該先熟悉下列指導方針和限制：  
  
-   不支援內嵌結構描述。  
  
     如果您的 XML 來源文件中有一個內嵌結構描述，XML 大量載入會忽略該結構描述。 您會針對 XML 資料外部的 XML 大量載入，指定對應的結構描述。 您無法使用 **xmlns = "x:schema"** 屬性指定節點上的對應架構。  
  
-   XML 文件已確認格式正確，但尚未經過驗證。  
  
     XML 大量載入會檢查 XML 檔以判斷其格式是否正確，也就是確保 XML 符合全球資訊網協會的 XML 1.0 建議的語法需求。 如果文件的格式不正確，XML 大量載入會取消處理並傳回錯誤。 唯一的例外是當文件為片段 (例如，文件沒有單一的根元素) 時，在此情況下，XML 大量載入將會載入文件。  
  
     XML 大量載入不會針對 XML 資料檔中定義或參考的任何 XML 資料或 DTD 結構描述驗證文件。 此外，XML 大量載入不會根據提供的對應結構描述驗證 XML 資料檔。  
  
-   系統會忽略任何 XML 初構資訊。  
  
     XML 大量載入會忽略 \<root> xml 檔中元素之前和之後的所有資訊。 例如，XML 大量載入會忽略任何 XML 宣告、內部 DTD 定義、外部 DTD 參考、註解等等。  
  
-   如果您擁有的對應結構描述會定義兩個資料表之間 (例如 Customer 和 CustOrder 之間) 的主索引鍵/外部索引鍵關聯性，則必須先在結構描述中描述具有主索引鍵的資料表。 包含外部索引鍵資料行的資料表稍後必須出現在結構描述中。 這是因為在架構中識別資料表的順序，就是用來將資料表載入資料庫的順序。例如，下列 XDR 架構在 XML 大量載入中會產生錯誤，因為元素會在專案 **\<Order>** 之前描述 **\<Customer>** 。 在 CustOrder 中的 CustomerID 資料行是外部索引鍵資料行，它會參考在 Cust 資料表中的 CustomerID 主索引鍵資料行。  
  
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
  
-   如果架構未使用 **sql：溢位欄位** 批註指定溢位資料行，Xml 大量載入會忽略任何存在於 xml 檔中的資料，但不會在對應架構中描述。  
  
     每當 XML 大量載入在 XML 資料流中碰到已知的標記時，會套用您所指定的對應結構描述。 它會忽略顯示在 XML 文件中的資料，但是不會在結構描述中描述。 例如，假設您有一個描述元素的對應架構 **\<Customer>** 。 XML 資料檔有 **\<AllCustomers>** 根標記 (，在包含所有元素的架構) 中並未說明 **\<Customer>** ：  
  
    ```  
    <AllCustomers>  
      <Customer>...</Customer>  
      <Customer>...</Customer>  
       ...  
    </AllCustomers>  
    ```  
  
     在此情況下，XML 大量載入會忽略 **\<AllCustomers>** 元素，並在專案開始進行對應 **\<Customer>** 。 XML 大量載入會忽略結構描述中沒有描述但是顯示在 XML 文件中的元素。  
  
     請考慮另一個包含元素的 XML 源資料檔案 **\<Order>** 。 這些元素不會在對應的結構描述中描述：  
  
    ```  
    <AllCustomers>  
      <Customer>...</Customer>  
        <Order> ... </Order>  
        <Order> ... </Order>  
         ...  
      <Customer>...</Customer>  
        <Order> ... </Order>  
        <Order> ... </Order>  
         ...  
      ...  
    </AllCustomers>  
    ```  
  
     XML 大量載入會忽略這些 **\<Order>** 元素。 但是，如果您在架構中使用 **sql：溢位欄位** 注釋來將資料行識別為溢位資料行，XML 大量載入會將所有未使用的資料儲存在此資料行中。  
  
-   CDATA 區段和實體參考會在儲存在資料庫之前，先轉譯成其對等字串。  
  
     在此範例中，CDATA 區段會包裝元素的值 **\<City>** 。 XML 大量載入會先將字串值 ( "NY" ) ，然後再將 **\<City>** 元素插入資料庫。  
  
    ```  
    <City><![CDATA[NY]]> </City>  
    ```  
  
     XML 大量載入不會保留實體參考。  
  
-   如果對應結構描述指定屬性的預設值，而且 XML 來源資料不包含該屬性，XML 大量載入會使用預設值。  
  
     下列範例 XDR 架構會將預設值指派給 **雇用** 屬性：  
  
    ```  
    <?xml version="1.0" ?>  
    <Schema xmlns="urn:schemas-microsoft-com:xml-data"   
            xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
            xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
       <ElementType name="root" sql:is-constant="1">  
          <element type="Customers" />  
       </ElementType>  
  
       <ElementType name="Customers" sql:relation="Cust3" >  
          <AttributeType name="CustomerID" dt:type="int"  />  
          <AttributeType name="HireDate"  default="2000-01-01" />  
          <AttributeType name="Salary"   />  
  
          <attribute type="CustomerID" sql:field="CustomerID" />  
          <attribute type="HireDate"   sql:field="HireDate"  />  
          <attribute type="Salary"     sql:field="Salary"    />  
       </ElementType>  
    </Schema>  
    ```  
  
     在此 XML 資料中，第二個元素遺漏了 **雇用** 屬性 **\<Customers>** 。 當 XML 大量載入將第二個 **\<Customers>** 元素插入資料庫時，它會使用在架構中指定的預設值。  
  
    ```  
    <ROOT>  
      <Customers CustomerID="1" HireDate="1999-01-01" Salary="10000" />  
      <Customers CustomerID="2" Salary="10000" />  
    </ROOT>  
    ```  
  
-   不支援 **sql： url 編碼** 注釋：  
  
     您無法在 XML 資料輸入中指定 URL，然後預期大量載入會從該位置讀取資料。  
  
     系統會建立在對應結構描述中所識別的資料表 (資料庫必須存在)。 如果有一或多個資料表已經存在於資料庫中，SGDropTables 屬性會決定是否要卸載和重新建立這些預先存在的資料表。  
  
-   如果您指定 SchemaGen 屬性 (例如，SchemaGen = true) ，則會建立對應架構中所識別的資料表。 但是，SchemaGen 不會建立任何條件約束 (例如在這些資料表上) PRIMARY KEY/FOREIGN KEY 條件約束，但有一個例外狀況：如果在關聯性中構成主鍵的 XML 節點定義為擁有 XML 類型的 ID (也就是，XSD) 的 **type = "xsd： ID"** ，而 SchemaGen 的 SGUseID 屬性設定為 True，則不只是從識別碼型別節點建立的主鍵，而是從對應架構關聯性建立主鍵/外鍵關聯性。  
  
-   SchemaGen 不會使用 XSD 架構 facet 和延伸模組來產生關聯式 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 架構。  
  
-   如果您指定 SchemaGen 屬性 (例如，SchemaGen = true) 在大量載入時，只會更新 (的資料表，而不會更新指定的共用名稱) 。  
  
-   SchemaGen 只提供從批註式 XSD 產生關聯式架構的基本功能。 如果需要，使用者應該手動修改產生的資料表。  
  
-   當資料表之間存在一個以上的關聯性時，SchemaGen 會嘗試建立單一關聯性，其中包含兩個數據表之間的所有相關索引鍵。 這個限制可能是 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 錯誤的原因。  
  
-   當您將 XML 資料大量載入資料庫時，在對應結構描述中至少要有一個對應到資料庫資料行的屬性或子元素。  
  
-   如果您要使用 XML 大量載入來插入日期值，必須以 (-)CCYY-MM-DD((+-)TZ) 格式指定這些值。 這是用於日期的標準 XSD 格式。  
  
-   某些屬性旗標與其他屬性旗標不相容。 例如，大量載入不支援搭配 **Keepidentity = false** 的 **Ignoreduplicatekeys = true** 。 當 **Keepidentity = false** 時，大量載入預期伺服器會產生索引鍵值。 資料表應該有索引鍵的身分 **識別** 條件約束。 伺服器不會產生重複的索引鍵，這表示不需要將 **Ignoreduplicatekeys** 設定為 **true**。 只有將內送資料的主鍵值上傳至具有資料列的資料表，且可能發生主鍵值衝突時，才應該將 **Ignoreduplicatekeys** 設為 **true** 。  
  
  
