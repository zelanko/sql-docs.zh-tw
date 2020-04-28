---
title: 運算式內容和查詢評估（XQuery） |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- expression context [XQuery]
- XQuery, expression context
- XQuery, query evaluation
- static context
- dynamic context [XQuery]
ms.assetid: 5059f858-086a-40d4-811e-81fedaa18b06
author: rothja
ms.author: jroth
ms.openlocfilehash: d665b16c6b635da8b267ac0549ab8d918af8c06b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68038926"
---
# <a name="expression-context-and-query-evaluation-xquery"></a>運算式內容和查詢評估 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  運算式的內容是用來分析和評估它的資訊。 以下是評估 XQuery 的兩個階段：  
  
-   **靜態內容**-這是查詢編譯階段。 依據可用的資訊，有時候錯誤是在靜態分析查詢期間引發。  
  
-   **動態內容**-這是查詢執行階段。 即使查詢沒有靜態錯誤 (例如查詢編譯期間的錯誤)，查詢仍可能在其執行期間傳回錯誤。  
  
## <a name="static-context"></a>靜態內容  
 靜態內容初始化是指集中所有資訊，以進行運算式之靜態分析的過程。 在靜態內容初始化的過程中，會完成下列項目：  
  
-   **界限空白字元**原則會設定為 [帶狀]。 因此，查詢中的**任何**專案和**屬性**的函式不會保留界限空白字元。 例如：  
  
    ```  
    declare @x xml  
    set @x=''  
    select @x.query('<a>  {"Hello"}  </a>,  
  
        <b> {"Hello2"}  </b>')  
    ```  
  
     此查詢傳回下列結果，因為在剖析 XQuery 運算式的過程中移除了邊界空格：  
  
    ```  
    <a>Hello</a><b>Hello2</b>  
    ```  
  
-   將針對下列各項，初始化前置詞和命名空間的繫結：  
  
    -   一組預先定義的命名空間。  
  
    -   任何使用 WITH XMLNAMESPACES 定義的命名空間。 如需詳細資訊，請參閱使用[With xmlnamespaces 將命名空間加入至查詢](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)。  
  
    -   任何在查詢初構中定義的命名空間。 請注意，初構中的命名空間宣告可能覆寫 WITH XMLNAMESPACES 中的命名空間宣告。 例如，在下列查詢中，WITH WITH XMLNAMESPACES 會宣告將它系結至命名空間（`https://someURI`）的前置詞（pd）。 不過，在 WHERE 子句中，查詢初構會覆寫繫結。  
  
        ```  
        WITH XMLNAMESPACES ('https://someURI' AS pd)  
        SELECT ProductModelID, CatalogDescription.query('  
            <Product   
                ProductModelID= "{ sql:column("ProductModelID") }"   
                />  
        ') AS Result  
        FROM Production.ProductModel  
        WHERE CatalogDescription.exist('  
            declare namespace  pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
             /pd:ProductDescription[(pd:Specifications)]'  
            ) = 1  
        ```  
  
     所有這些命名空間繫結都是在靜態內容初始化期間解析的。  
  
-   如果查詢具類型的**xml**資料行或變數，與資料行或變數相關聯之 xml 架構集合的元件會匯入至靜態內容中。 如需詳細資訊，請參閱[比較具類型的 xml 與](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)不具類型的 xml。  
  
-   對於所匯入之結構描述中的每一個不可部份完成類型，也可以在靜態內容中使用轉換函數。 下列範例會加以說明。 在此範例中，查詢是針對具類型的**xml**變數所指定。 與此變數相關聯之 XML 結構描述集合會定義不可部份完成類型 myType。 對應至這個類型，在靜態分析期間可以使用轉換函數**myType （）**。 查詢運算式 (`ns:myType(0)`) 傳回 myType 的值。  
  
    ```  
    -- DROP XML SCHEMA COLLECTION SC  
    -- go  
    CREATE XML SCHEMA COLLECTION SC AS '<schema xmlns="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="myNS" xmlns:ns="myNS"  
    xmlns:s="https://schemas.microsoft.com/sqlserver/2004/sqltypes">  
          <import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
          <simpleType name="myType">  
                <restriction base="int">  
                 <enumeration value="0" />  
                  <enumeration value="1"/>  
                </restriction>  
          </simpleType>  
          <element name="root" type="ns:myType"/>  
    </schema>'  
    go  
  
    DECLARE @var XML(SC)  
    SET @var = '<root xmlns="myNS">0</root>'  
    -- specify myType() casting function in the query  
    SELECT @var.query('declare namespace ns="myNS"; ns:myType(0)')  
    ```  
  
     在下列範例中，會在運算式中指定**int**內建 XML 類型的轉換函式。  
  
    ```  
    declare @x xml  
    set @x = ''  
    select @x.query('xs:int(5)')  
    go  
    ```  
  
 在靜態內容初始化之後，會分析 (編譯) 查詢運算式。 靜態分析包含下列動作：  
  
1.  查詢剖析。  
  
2.  解析運算式中所指定的函數和類型名稱。  
  
3.  查詢的靜態類型 (Static Typing)。 這可確定查詢為安全類型。 例如，下列查詢會傳回靜態錯誤，因為**+** 運算子需要數值基本類型引數：  
  
    ```  
    declare @x xml  
    set @x=''  
    SELECT @x.query('"x" + 4')  
    ```  
  
     在下列範例中， **value （）** 運算子需要 singleton。 如 XML 架構中所指定，可以有多個\<Elem> 元素。 運算式的靜態分析判斷它不是安全類型，而傳回靜態錯誤。 若要解決此錯誤，必須將運算式重寫為明確指定單一值 (`data(/x:Elem)[1]`)。  
  
    ```  
    DROP XML SCHEMA COLLECTION SC  
    go  
    CREATE XML SCHEMA COLLECTION SC AS '<schema xmlns="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="myNS" xmlns:ns="myNS"  
    xmlns:s="https://schemas.microsoft.com/sqlserver/2004/sqltypes">  
          <import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
          <element name="Elem" type="string"/>  
    </schema>'  
    go  
  
    declare @x xml (SC)  
    set @x='<Elem xmlns="myNS">test</Elem><Elem xmlns="myNS">test2</Elem>'  
    SELECT @x.value('declare namespace x="myNS"; data(/x:Elem)[1]','varchar(20)')  
    ```  
  
     如需詳細資訊，請參閱[XQuery 和靜態類型](../xquery/xquery-and-static-typing.md)。  
  
### <a name="implementation-restrictions"></a>實作限制  
 下列是與靜態內容相關的限制：  
  
-   不支援 XPath 相容性模式。  
  
-   若為 XML 建構，只支援 Strip 建構模式。 這是預設值。 因此，結構化專案節點的類型是**xdt：** 不具類型的型別，而屬性則是**xdt： untypedAtomic**型別。  
  
-   只支援已排序的順序模式。  
  
-   只支援「移除 XML 空格」原則。  
  
-   不支援基本 URI 功能。  
  
-   **fn： doc （）** 不受支援。  
  
-   **fn：不支援 collection （）** 。  
  
-   不提供 XQuery Static Flagger。  
  
-   使用與**xml**資料類型相關聯的定序。 此定序一律設為 Unicode 字碼指標定序。  
  
## <a name="dynamic-context"></a>動態內容  
 動態內容是指在執行運算式時必須提供的資訊。 除了靜態內容之外，下列資訊也會初始化成為動態內容的一部份：  
  
-   運算式焦點如內容項目、內容位置和內容大小皆已初始化，如後文所示。 請注意，[節點（）方法](../t-sql/xml/nodes-method-xml-data-type.md)可以覆寫所有這些值。  
  
    -   **Xml**資料類型會將內容專案（正在處理的節點）設定為檔節點。  
  
    -   內容位置 (即內容項目相對於所處理之節點的位置) 先設為 1。  
  
    -   內容大小 (即所處理之序列的項目數) 先設為 1，因為每次都有一個文件節點。  
  
### <a name="implementation-restrictions"></a>實作限制  
 下列是與動態內容相關的限制：  
  
-   不支援**目前的日期和時間**內容函數（ **fn： current-date**、 **fn： current time**和**fn： current-dateTime**）。  
  
-   **隱含時區**會固定為 UTC + 0，而且無法變更。  
  
-   不支援**fn： doc （）** 函數。 所有查詢都會針對**xml**類型資料行或變數來執行。  
  
-   不支援**fn： collection （）** 函數。  
  
## <a name="see-also"></a>另請參閱  
 [XQuery 基本概念](../xquery/xquery-basics.md)   
 [比較具類型的 XML 與不具類型的 XML](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML 結構描述集合 &#40;SQL Server&#41;](../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
