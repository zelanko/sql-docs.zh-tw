---
title: 在 XPath 查詢中指定關係運算子（SQLXML 4.0） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], relational operators
- relational operators [SQLXML]
- XPath operators [SQLXML]
- operators [SQLXML]
ms.assetid: 177a0eb2-11ef-4459-a317-485a433ee769
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1597893c203f1223ad916f5c7acecb66ff554c76
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66012443"
---
# <a name="specifying-relational-operators-in-xpath-queries-sqlxml-40"></a>在 XPath 查詢中指定關係運算子 (SQLXML 4.0)
  下列範例示範如何在 XPath 查詢中指定關係運算子。 這些範例中的 XPath 查詢會針對 SampleSchema1.xml 中包含的對應結構描述來指定。 如需此範例架構的詳細資訊，請參閱[XPath 範例的範例批註式 XSD 架構 &#40;SQLXML 4.0&#41;](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-specify-relational-operator"></a>A. 指定關係運算子  
 這個 XPath 查詢會傳回** \<Customer>** 元素的子項目，其中**CustomerID**屬性值為 "1"，而任何子** \<Order>** 元素包含具有值大於3之**OrderQty**屬性的** \<OrderDetail>** 子系：  
  
```  
/child::Customer[@CustomerID="1"]/Order/OrderDetail[@OrderQty > 3]  
```  
  
 括弧中指定的述詞會篩選** \<Customer>** 元素。 只會傳回至少有一個** \<OrderDetail>** 孫代具有大於3的 OrderQty 屬性值的** \<客戶>** 元素。  
  
 
  `child` 軸是預設值。 因此，此查詢可以指定為：  
  
```  
/Customer[@CustomerID="1"]/Order/OrderDetail[@OrderQty > 3]  
```  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>針對對應的結構描述測試 XPath 查詢  
  
1.  複製[範例架構程式碼](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)，並將它貼到文字檔中。 將檔案儲存為 SampleSchema1.xml。  
  
2.  建立下列範本 (SpecifyRelationalA.xml)，並將其儲存在儲存 SampleSchema1.xml 的目錄中。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /Customer[@CustomerID="1"]/Order/OrderDetail[@OrderQty > 3]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     針對對應結構描述 (SampleSchema1.xml) 指定的目錄路徑相對於儲存範本的目錄。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱[使用 ADO 執行 SQLXML 4.0 查詢](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 以下為範本執行的結果集：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <OrderDetail ProductID="Prod-760" UnitPrice="503.3507" OrderQty="4" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-763" UnitPrice="503.3507" OrderQty="4" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-766" UnitPrice="503.3507" OrderQty="4" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-732" UnitPrice="440.1742" OrderQty="4" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-757" UnitPrice="1049.7528" OrderQty="4" UnitPriceDiscount="0" />   
</ROOT>  
```  
  
### <a name="b-specify-relational-operator-in-the-xpath-query-and-use-boolean-function-to-compare-the-result"></a>B. 在 XPath 查詢中指定關係運算子並使用布林函數來比較結果  
 此查詢會傳回**SalesPersonID**屬性值小於270之內容節點的所有** \<Order>** 元素子系：  
  
```  
/child::Customer/child::Order[(attribute::SalesPersonID < 270)=true()]  
```  
  
 您可以指定 `attribute` 軸的快速鍵 (@)，而且因為 `child` 軸是預設值，因此可從查詢省略：  
  
```  
/Customer/Order[(@SalesPersonID < 270)=true()]  
```  
  
> [!NOTE]  
>  在範本中指定此查詢時，< 字元必須是實體編碼，因為 < 字元在 XML 檔中具有特殊意義。 在範本中，使用`<`來指定 < 字元。  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>針對對應的結構描述測試 XPath 查詢  
  
1.  複製[範例架構程式碼](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)，並將它貼到文字檔中。 將檔案儲存為 SampleSchema1.xml。  
  
2.  建立下列範本 (SpecifyRelationalB.xml)，並將其儲存在儲存 SampleSchema1.xml 的目錄中。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="SampleSchema1.xml">  
            /Customer/Order[(@SalesPersonID<270)=true()]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     針對對應結構描述 (SampleSchema1.xml) 指定的目錄路徑相對於儲存範本的目錄。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱[使用 ADO 執行 SQLXML 4.0 查詢](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 以下為範本執行的部分結果集：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Order SalesOrderID="Ord-46613" SalesPersonID="268"   
         OrderDate="2002-07-01T00:00:00"   
         DueDate="2002-07-13T00:00:00"   
         ShipDate="2002-07-08T00:00:00">  
    <OrderDetail ProductID="Prod-739" UnitPrice="917.9363"   
                 OrderQty="2" UnitPriceDiscount="0" />   
    <OrderDetail ProductID="Prod-779" UnitPrice="1491.4221"   
                 OrderQty="1" UnitPriceDiscount="0" />   
    <OrderDetail ProductID="Prod-825" UnitPrice="242.1391"   
                 OrderQty="1" UnitPriceDiscount="0" />   
  </Order>  
  <Order SalesOrderID="Ord-71919" SalesPersonID="268"  
         OrderDate="2004-06-01T00:00:00"   
         DueDate="2004-06-13T00:00:00"   
         ShipDate="2004-06-08T00:00:00">  
    <OrderDetail ProductID="Prod-961" UnitPrice="534.492"   
                 OrderQty="1" UnitPriceDiscount="0" />   
    <OrderDetail ProductID="Prod-965" UnitPrice="534.492"   
                 OrderQty="1" UnitPriceDiscount="0" />   
    <OrderDetail ProductID="Prod-966" UnitPrice="1716.5304"   
                 OrderQty="1" UnitPriceDiscount="0" />   
  </Order>  
  ...  
</ROOT>  
```  
  
  
