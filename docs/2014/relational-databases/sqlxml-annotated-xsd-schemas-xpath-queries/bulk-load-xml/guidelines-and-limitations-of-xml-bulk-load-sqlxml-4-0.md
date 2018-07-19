---
title: 指導方針和限制的 XML 大量載入 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- XML Bulk Load [SQLXML], about XML Bulk Load
- bulk load [SQLXML], about bulk load
ms.assetid: c5885d14-c7c1-47b3-a389-455e99a7ece1
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 22ef1e64e2c8cf3dc1af65fde51c7b12107f1916
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37149359"
---
# <a name="guidelines-and-limitations-of-xml-bulk-load-sqlxml-40"></a>XML 大量載入的指導方針和限制 (SQLXML 4.0)
  當您使用 XML 大量載入時，應該先熟悉下列指導方針和限制：  
  
-   不支援內嵌結構描述。  
  
     如果您的 XML 來源文件中有一個內嵌結構描述，XML 大量載入會忽略該結構描述。 您會針對 XML 資料外部的 XML 大量載入，指定對應的結構描述。 您無法使用，以指定在節點上的對應結構描述**xmlns ="x： 結構描述 」** 屬性。  
  
-   XML 文件已確認格式正確，但尚未經過驗證。  
  
     XML 大量載入會檢查 XML 文件來判斷其格式是否正確，也就是確認 XML 符合全球資訊網協會對於 XML 1.0 建議的需求。 如果文件的格式不正確，XML 大量載入會取消處理並傳回錯誤。 唯一的例外是當文件為片段 (例如，文件沒有單一的根元素) 時，在此情況下，XML 大量載入將會載入文件。  
  
     XML 大量載入不會針對 XML 資料檔中定義或參考的任何 XML 資料或 DTD 結構描述驗證文件。 此外，XML 大量載入不會根據提供的對應結構描述驗證 XML 資料檔。  
  
-   系統會忽略任何 XML 初構資訊。  
  
     XML 大量載入會忽略之前和之後的所有資訊\<根 > 在 XML 文件中的項目。 例如，XML 大量載入會忽略任何 XML 宣告、內部 DTD 定義、外部 DTD 參考、註解等等。  
  
-   如果您擁有的對應結構描述會定義兩個資料表之間 (例如 Customer 和 CustOrder 之間) 的主索引鍵/外部索引鍵關聯性，則必須先在結構描述中描述具有主索引鍵的資料表。 包含外部索引鍵資料行的資料表稍後必須出現在結構描述中。 這是結構描述中所識別資料表的順序是用來載入資料庫的順序。例如，下列的 XDR 結構描述都會產生錯誤因為使用中 XML 大量載入時**\<順序 >** 元素的描述之前**\<客戶 >** 項目。 在 CustOrder 中的 CustomerID 資料行是外部索引鍵資料行，它會參考在 Cust 資料表中的 CustomerID 主索引鍵資料行。  
  
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
  
-   如果結構描述沒有使用 `sql:overflow-field` 註解指定溢位資料行，XML 大量載入會忽略顯示在 XML 文件中的任何資料，但是不會在對應結構描述中描述。  
  
     每當 XML 大量載入在 XML 資料流中碰到已知的標記時，會套用您所指定的對應結構描述。 它會忽略顯示在 XML 文件中的資料，但是不會在結構描述中描述。 例如，假設您有描述的對應結構描述**\<客戶 >** 項目。 XML 資料檔都 **\<AllCustomers >** 根標記 （這不會在結構描述） 圍住所有**\<客戶 >** 項目：  
  
    ```  
    <AllCustomers>  
      <Customer>...</Customer>  
      <Customer>...</Customer>  
       ...  
    </AllCustomers>  
    ```  
  
     在此情況下，XML 大量載入會忽略 **\<AllCustomers >** 項目，並開始在對應**\<客戶 >** 項目。 XML 大量載入會忽略結構描述中沒有描述但是顯示在 XML 文件中的元素。  
  
     請考慮另一個 XML 來源的資料檔案，其中包含**\<順序 >** 項目。 這些元素不會在對應的結構描述中描述：  
  
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
  
     XML 大量載入會忽略這些**\<順序 >** 項目。 但是，如果您使用`sql:overflow-field`結構描述識別為溢位資料行，XML 大量載入的資料行中的註解會將所有未耗用的資料儲存在這個資料行。  
  
-   CDATA 區段和實體參考會在儲存在資料庫之前，先轉譯成其對等字串。  
  
     在此範例中，CDATA 區段包裝的值**\<縣 （市) >** 項目。 XML 大量載入會擷取字串值 ("NY") 之前它會插入, **\<縣 （市) >** 到資料庫的項目。  
  
    ```  
    <City><![CDATA[NY]]> </City>  
    ```  
  
     XML 大量載入不會保留實體參考。  
  
-   如果對應結構描述指定屬性的預設值，而且 XML 來源資料不包含該屬性，XML 大量載入會使用預設值。  
  
     下列範例 XDR 結構描述預設將值指派給**HireDate**屬性：  
  
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
  
     在此 XML 資料中， **HireDate**屬性是從第二個遺失**\<客戶 >** 項目。 當 XML 大量載入會將第二個**\<客戶 >** 到資料庫的項目，它會使用結構描述中指定的預設值。  
  
    ```  
    <ROOT>  
      <Customers CustomerID="1" HireDate="1999-01-01" Salary="10000" />  
      <Customers CustomerID="2" Salary="10000" />  
    </ROOT>  
    ```  
  
-   不支援 `sql:url-encode` 註解：  
  
     您無法在 XML 資料輸入中指定 URL，然後預期大量載入會從該位置讀取資料。  
  
     系統會建立在對應結構描述中所識別的資料表 (資料庫必須存在)。 如果一或多個資料表的資料庫中已經存在，SGDropTables 屬性會決定是否要卸除並重新建立這些預先存在的資料表。  
  
-   如果您指定 SchemaGen 屬性 (例如 SchemaGen = true)，會建立對應結構描述中所識別的資料表。 但 SchemaGen 不會建立這些資料表上的任何條件約束 （例如 PRIMARY KEY/FOREIGN KEY 條件約束），但有一個例外： 如果構成關聯性中的主索引鍵的 XML 節點定義為具有 XML 類型的識別碼 (也就是`type="xsd:ID"`的XSD) 和 SGUseID 屬性設定為 True 的 SchemaGen，則不只主索引鍵建立從 ID 類型節點，但從對應結構描述關聯性建立主索引鍵/外部索引鍵關聯性。  
  
-   SchemaGen 不會使用 XSD 結構描述 facet 和延伸模組來產生關聯式[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]結構描述。  
  
-   如果您指定 SchemaGen 屬性 (例如 SchemaGen = true) 在大量載入，只有資料表 （和不共用名稱的檢視） 所指定更新。  
  
-   SchemaGen 只會提供從註解式 XSD 產生的關聯式結構描述的基本功能。 如果需要，使用者應該手動修改產生的資料表。  
  
-   在多個關聯性的資料表之間不存在，SchemaGen 會嘗試建立包含兩個資料表間所涉及的所有金鑰的單一關聯性。 這個限制可能是 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 錯誤的原因。  
  
-   當您將 XML 資料大量載入資料庫時，在對應結構描述中至少要有一個對應到資料庫資料行的屬性或子元素。  
  
-   如果您要使用 XML 大量載入來插入日期值，必須以 (-)CCYY-MM-DD((+-)TZ) 格式指定這些值。 這是用於日期的標準 XSD 格式。  
  
-   某些屬性旗標與其他屬性旗標不相容。 例如，大量載入不同時支援 `Ignoreduplicatekeys=true` 及 `Keepidentity=false`。 `Keepidentity=false` 時，大量載入需要伺服器才能產生索引鍵值。 資料表在索引鍵上應該要有 `IDENTITY` 條件約束。 伺服器不會產生重複的索引鍵，這表示不需要將 `Ignoreduplicatekeys` 設定為 `true`。 只有在下列兩種情況下才需要將 `Ignoreduplicatekeys` 設定為 `true`：從內送資料上傳主索引鍵值到具有資料列的資料表以及可能會發生主索引鍵值衝突時。  
  
  
