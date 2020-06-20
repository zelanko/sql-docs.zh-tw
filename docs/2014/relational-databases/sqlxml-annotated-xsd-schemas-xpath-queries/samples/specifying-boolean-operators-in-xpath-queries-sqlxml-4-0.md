---
title: 在 XPath 查詢中指定布林運算子（SQLXML 4.0） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath operators [SQLXML]
- OR operator
- Boolean operators
- XPath queries [SQLXML], Boolean operators
- operators [SQLXML]
ms.assetid: 9928cff5-62ac-42aa-96bf-2e09a1df0bc3
author: rothja
ms.author: jroth
ms.openlocfilehash: f4373229d6e612a7de401dbd94bc0da1766db45b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065687"
---
# <a name="specifying-boolean-operators-in-xpath-queries-sqlxml-40"></a>在 XPath 查詢中指定布林運算子 (SQLXML 4.0)
  下列範例顯示如何在 XPath 查詢中指定布林運算子。 此範例中的 XPath 查詢會針對 SampleSchema1.xml 中包含的對應結構描述來指定。 如需此範例架構的詳細資訊，請參閱[XPath 範例的範例批註式 XSD 架構 &#40;SQLXML 4.0&#41;](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-specify-the-or-boolean-operator"></a>A. 指定 OR 布林運算子  
 這個 XPath 查詢會傳回 **\<Customer>** **CustomerID**屬性值為13或31之內容節點的元素子系：  
  
```  
/child::Customer[attribute::CustomerID="13" or attribute::CustomerID="31"]  
```  
  
 您可以指定 `attribute` 軸的快速鍵 (@)，而且因為 `child` 軸是預設值，因此可省略：  
  
```  
/Customer[@CustomerID="13" or @CustomerID="31"]  
```  
  
 在述詞中， `attribute` 是軸而且 `CustomerID` 是節點測試（如果**CustomerID**是節點，則為 TRUE **\<attribute>** ，因為 **\<attribute>** 節點是軸的主要節點 `attribute` ）。 述詞會篩選項目 **\<Customer>** ，並只傳回滿足述詞中所指定條件的元素。  
  
##### <a name="to-test-the-xpath-queries-against-the-mapping-schema"></a>針對對應的結構描述測試 XPath 查詢  
  
1.  複製[範例架構程式碼](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)，並將它貼到文字檔中。 將檔案儲存為 SampleSchema1.xml。  
  
2.  建立下列範本 (BooleanOperatorsA.xml)，並將其儲存在儲存 SampleSchema1.xml 的目錄中。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /Customer[@CustomerID="13" or @CustomerID="31"]  
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
  <Customer CustomerID="13" SalesPersonID="286" TerritoryID="7" AccountNumber="13" CustomerType="S" />   
  <Customer CustomerID="31" SalesPersonID="286" TerritoryID="7" AccountNumber="31" CustomerType="S" Orders="Ord-51803 Ord-69427">  
    <Order SalesOrderID="Ord-51803" SalesPersonID="286" OrderDate="2003-08-01T00:00:00" DueDate="2003-08-13T00:00:00" ShipDate="2003-08-08T00:00:00">  
      <OrderDetail ProductID="Prod-718" UnitPrice="1059.31" OrderQty="1" UnitPriceDiscount="0" />   
      <OrderDetail ProductID="Prod-838" UnitPrice="1059.31" OrderQty="1" UnitPriceDiscount="0" />   
    </Order>  
    <Order SalesOrderID="Ord-69427" SalesPersonID="286" OrderDate="2004-05-01T00:00:00" DueDate="2004-05-13T00:00:00" ShipDate="2004-05-08T00:00:00">  
      <OrderDetail ProductID="Prod-835" UnitPrice="440.1742" OrderQty="1" UnitPriceDiscount="0" />   
    </Order>  
  </Customer>  
</ROOT>  
```  
  
  
