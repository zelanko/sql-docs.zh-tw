---
title: 在 XPath 查詢 (SQLXML 4.0) 中指定算術運算子 |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- arithmetic operators
- XPath operators [SQLXML]
- XPath queries [SQLXML], arithmetic operators
- operators [SQLXML]
ms.assetid: fdfbc87d-759f-4abc-acf5-a21de01f78d3
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d9513da290322ca23b7d950e0f36404cde9ee859
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43070476"
---
# <a name="specifying-arithmetic-operators-in-xpath-queries-sqlxml-40"></a>在 XPath 查詢中指定算術運算子 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  下列範例示範如何在 XPath 查詢中指定算術運算子。 此範例中的 XPath 查詢會針對 SampleSchema1.xml 中包含的對應結構描述來指定。 如需此範例結構描述資訊，請參閱[範例註解式 XSD 結構描述 XPath 範例的&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-specify-the--arithmetic-operator"></a>A. 指定 * 算術運算子  
 此 XPath 查詢會傳回 **\<OrderDetail >** 滿足指定的述詞的項目：  
  
```  
/child::OrderDetail[@UnitPrice * @Quantity = 12.350]  
```  
  
 在查詢中，`child`是軸和`OrderDetail`為節點測試 (TRUE 如果**OrderDetail**會**\<項目節點 >**，因為 **\<項目 >** 節點是主要節點**子**軸)。 針對所有 **\<OrderDetail >** 項目 節點中，套用述詞中的測試，並且會傳回只在符合條件的節點。  
  
> [!NOTE]  
>  XPath 中的數字為雙精確度浮點數，而且在範例中比較浮點數會造成四捨五入。  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>針對對應的結構描述測試 XPath 查詢  
  
1.  複製[結構描述程式碼範例](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)並將它貼到文字檔。 將檔案儲存為 SampleSchema1.xml。  
  
2.  建立下列範本 (ArithmeticOperatorA.xml)，並將其儲存在儲存 SampleSchema1.xml 的目錄中。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /OrderDetail[@UnitPrice * @OrderQty = 12.350]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     針對對應結構描述 (SampleSchema1.xml) 指定的目錄路徑相對於儲存範本的目錄。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱 <<c0> [ 使用 ADO 執行 SQLXML 4.0 查詢](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
```  
Here is the partial result set of the template execution:    
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <OrderDetail ProductID="Prod-709" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-709" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-709" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-709" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-709" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-709" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-709" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-710" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
   ...  
</ROOT>  
```  
  
  
