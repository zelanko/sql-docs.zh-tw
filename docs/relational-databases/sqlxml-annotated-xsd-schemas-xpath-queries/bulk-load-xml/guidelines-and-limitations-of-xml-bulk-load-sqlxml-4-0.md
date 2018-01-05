---
title: "方針和限制的 XML 大量載入 (SQLXML 4.0) |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- XML Bulk Load [SQLXML], about XML Bulk Load
- bulk load [SQLXML], about bulk load
ms.assetid: c5885d14-c7c1-47b3-a389-455e99a7ece1
caps.latest.revision: "26"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 453ce7fe955af4ffe25d13b1ab1abfef0f48cf59
ms.sourcegitcommit: 7673ad0e84a6de69420e19247a59e39ca751a8aa
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/03/2018
---
# <a name="guidelines-and-limitations-of-xml-bulk-load-sqlxml-40"></a>XML 大量載入的指導方針和限制 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]當您使用 XML 大量載入時，您應該熟悉下列指導方針和限制：  
  
-   不支援內嵌結構描述。  
  
     如果您的 XML 來源文件中有一個內嵌結構描述，XML 大量載入會忽略該結構描述。 您會針對 XML 資料外部的 XML 大量載入，指定對應的結構描述。 您無法使用，以指定對應結構描述節點處所**xmlns ="x： 結構描述 」**屬性。  
  
-   XML 文件已確認格式正確，但尚未經過驗證。  
  
     XML 大量載入會檢查 XML 文件來判斷其格式是否正確，也就是確認 XML 符合全球資訊網協會對於 XML 1.0 建議的需求。 如果文件的格式不正確，XML 大量載入會取消處理並傳回錯誤。 唯一的例外是當文件為片段 (例如，文件沒有單一的根元素) 時，在此情況下，XML 大量載入將會載入文件。  
  
     XML 大量載入不會針對 XML 資料檔中定義或參考的任何 XML 資料或 DTD 結構描述驗證文件。 此外，XML 大量載入不會根據提供的對應結構描述驗證 XML 資料檔。  
  
-   系統會忽略任何 XML 初構資訊。  
  
     XML 大量載入會忽略之前和之後的所有資訊\<根目錄 > XML 文件中的項目。 例如，XML 大量載入會忽略任何 XML 宣告、內部 DTD 定義、外部 DTD 參考、註解等等。  
  
-   如果您擁有的對應結構描述會定義兩個資料表之間 (例如 Customer 和 CustOrder 之間) 的主索引鍵/外部索引鍵關聯性，則必須先在結構描述中描述具有主索引鍵的資料表。 包含外部索引鍵資料行的資料表稍後必須出現在結構描述中。 這是結構描述中所識別的資料表的順序是用來載入資料庫中的順序。例如，下列 XDR 結構描述會產生錯誤時它用於 XML 大量載入因為**\<順序 >**元素的之前描述**\<客戶 >**項目。 在 CustOrder 中的 CustomerID 資料行是外部索引鍵資料行，它會參考在 Cust 資料表中的 CustomerID 主索引鍵資料行。  
  
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
  
-   如果結構描述不會指定溢位資料行使用**sql: overflow-field-欄位**註釋，XML 大量載入會忽略任何存在於 XML 文件中，但不是會在對應結構描述中描述的資料。  
  
     每當 XML 大量載入在 XML 資料流中碰到已知的標記時，會套用您所指定的對應結構描述。 它會忽略顯示在 XML 文件中的資料，但是不會在結構描述中描述。 例如，假設您有對應的結構描述，描述**\<客戶 >**項目。 XML 資料檔案具有 **\<AllCustomers >**根標記 （這不在結構描述） 圍住所有**\<客戶 >**項目：  
  
    ```  
    <AllCustomers>  
      <Customer>...</Customer>  
      <Customer>...</Customer>  
       ...  
    </AllCustomers>  
    ```  
  
     在此情況下，XML 大量載入會忽略 **\<AllCustomers >**項目，並開始在對應**\<客戶 >**項目。 XML 大量載入會忽略結構描述中沒有描述但是顯示在 XML 文件中的元素。  
  
     請考慮其他 XML 來源的資料檔案，其中包含**\<順序 >**項目。 這些元素不會在對應的結構描述中描述：  
  
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
  
     XML 大量載入會忽略這些**\<順序 >**項目。 但是，如果您使用**sql: overflow-field-欄位**註解結構描述識別為溢位資料行，XML 大量載入的資料行中儲存此資料行中的所有未耗用的資料。  
  
-   CDATA 區段和實體參考會在儲存在資料庫之前，先轉譯成其對等字串。  
  
     在此範例中，CDATA 區段包裝的值**\<縣 （市) >**項目。 XML 大量載入會擷取字串值 ("NY") 之前它會插入, **\<縣 （市) >**到資料庫的項目。  
  
    ```  
    <City><![CDATA[NY]]> </City>  
    ```  
  
     XML 大量載入不會保留實體參考。  
  
-   如果對應結構描述指定屬性的預設值，而且 XML 來源資料不包含該屬性，XML 大量載入會使用預設值。  
  
     下列範例 XDR 結構描述指派的預設值來**HireDate**屬性：  
  
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
  
     在此 XML 資料， **HireDate**屬性是在第二個遺失**\<客戶 >**項目。 當 XML 大量載入將第二個**\<客戶 >**到資料庫的項目，它會使用預設值，指定結構描述中。  
  
    ```  
    <ROOT>  
      <Customers CustomerID="1" HireDate="1999-01-01" Salary="10000" />  
      <Customers CustomerID="2" Salary="10000" />  
    </ROOT>  
    ```  
  
-   **Sql: url-encode-編碼**不支援註解：  
  
     您無法在 XML 資料輸入中指定 URL，然後預期大量載入會從該位置讀取資料。  
  
     系統會建立在對應結構描述中所識別的資料表 (資料庫必須存在)。 如果一或多個資料表的資料庫中已經存在，SGDropTables 屬性會決定是否要卸除並重新建立這些預先存在的資料表。  
  
-   如果您指定 SchemaGen 屬性 (例如，SchemaGen = true)，會建立對應結構描述中所識別的資料表。 但 SchemaGen 不會建立這些資料表上的任何條件約束 （例如 PRIMARY KEY/FOREIGN KEY 條件約束） 有一個例外狀況： 如果構成關聯性的主索引鍵的 XML 節點定義為具有 XML 類型的識別碼 (也就是**類型 =「 xsd:ID"** xsd) 和 SGUseID 屬性設定為 True 的 SchemaGen，則不只主索引鍵建立從 ID 類型節點，但從對應結構描述關聯性建立主索引鍵/外部索引鍵關聯性。  
  
-   SchemaGen 不使用 XSD 結構描述 facet 和延伸模組來產生關聯式[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]結構描述。  
  
-   如果您指定 SchemaGen 屬性 (例如 SchemaGen = true) 上大量載入，只有資料表 （和不共用名稱的檢視） 指定的更新。  
  
-   SchemaGen 只會提供從註解式 XSD 產生的關聯式結構描述的基本功能。 如果需要，使用者應該手動修改產生的資料表。  
  
-   在一個以上的關聯性存在資料表之間 SchemaGen 會嘗試建立單一關聯性，其包含兩個資料表間所涉及的所有金鑰。 這個限制可能是 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 錯誤的原因。  
  
-   當您將 XML 資料大量載入資料庫時，在對應結構描述中至少要有一個對應到資料庫資料行的屬性或子元素。  
  
-   如果您要使用 XML 大量載入來插入日期值，必須以 (-)CCYY-MM-DD((+-)TZ) 格式指定這些值。 這是用於日期的標準 XSD 格式。  
  
-   某些屬性旗標與其他屬性旗標不相容。 大量載入不支援的例如**Ignoreduplicatekeys = true**搭配**Keepidentity = false**。 當**Keepidentity = false**，大量載入需要伺服器才能產生索引鍵值。 資料表應該有**識別**鍵條件約束。 伺服器不會產生重複的索引鍵，這表示不需要針對**Ignoreduplicatekeys**設為**true**。 **Ignoreduplicatekeys**應該設定為**true**只能上傳至資料表的主索引鍵值，從內送資料時具有資料列，且主索引鍵值衝突可能會。  
  
  
