---
title: 在 XPath 查詢 (SQLXML 4.0) 中指定明確的轉換函式 |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- explicit conversion functions [SQLXML]
- string function
- number function
- XPath queries [SQLXML], explicit conversion functions
ms.assetid: 1111cb5d-2bd9-4bdb-8de2-dc0e47452dd6
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9f5fc967c37b894d6af9e6c000ee2998b3965c1d
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43085616"
---
# <a name="specifying-explicit-conversion-functions-in-xpath-queries-sqlxml-40"></a>在 XPath 查詢中指定明確轉換函數 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  下列範例將示範如何在 XPath 查詢中指定明確轉換函數。 這些範例中的 XPath 查詢會針對 SampleSchema1.xml 中包含的對應結構描述來指定。 如需此範例結構描述資訊，請參閱[範例註解式 XSD 結構描述 XPath 範例的&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-use-the-number-explicit-conversion-function"></a>A. 使用 number() 明確轉換函數  
 **Number （)** 函式會將引數轉換為數字。  
  
 假設的值**ContactID**是非數值，下列查詢會轉換**ContactID**的數字並比較它與 4 這個值。 然後查詢會傳回所有**\<員工 >** 的內容節點的項目子系**ContactID**數值的值為 4 的屬性：  
  
```  
/child::Contact[number(attribute::ContactID)= 4]  
```  
  
 捷徑**屬性**軸 (@) 可以指定，而且因為**子**軸是預設值，它可以從查詢省略：  
  
```  
/Contact[number(@ContactID) = 4]  
```  
  
 在關聯式詞彙中，查詢會傳回具有員工**ContactID**為 4。  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>針對對應的結構描述測試 XPath 查詢  
  
1.  複製[結構描述程式碼範例](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)並將它貼到文字檔。 將檔案儲存為 SampleSchema1.xml。  
  
2.  建立下列範本 (ExplicitConversionA.xml)，並將其儲存在儲存 SampleSchema1.xml 的目錄中。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /Contact[number(@ContactID)=4]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     針對對應結構描述 (SampleSchema1.xml) 指定的目錄路徑相對於儲存範本的目錄。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱 <<c0> [ 使用 ADO 執行 SQLXML 4.0 查詢](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 這個範本執行的結果集如下：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Contact ContactID="4" LastName="Acevedo" FirstName="Humberto" Title="Sr." />   
</ROOT>  
```  
  
### <a name="b-use-the-string-explicit-conversion-function"></a>B. 使用 string() 明確轉換函數  
 **String （)** 函式會將引數轉換為字串。  
  
 下列查詢會轉換**ContactID**成字串並比較它與字串值"4"。 此查詢會傳回所有**\<員工 >** 的內容節點的項目子系**ContactID** "4"的字串值：  
  
```  
/child::Contact[string(attribute::ContactID)="4"]  
```  
  
 捷徑**屬性**軸 (@) 可以指定，而且因為**子**軸是預設值，它可以從查詢省略：  
  
```  
/Contact[string(@ContactID)="4"]  
```  
  
 就功能而言，這個函數與上一個範例查詢會傳回相同的結果，不過其評估是針對字串值而非數值 (亦即，數字 4) 進行。  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>針對對應的結構描述測試 XPath 查詢  
  
1.  複製[結構描述程式碼範例](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)並將它貼到文字檔。 將檔案儲存為 SampleSchema1.xml。  
  
2.  建立下列範本 (ExplicitConversionB.xml)，並將其儲存在儲存 SampleSchema1.xml 的目錄中。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        Contact[string(@ContactID)="4"]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     針對對應結構描述 (SampleSchema1.xml) 指定的目錄路徑相對於儲存範本的目錄。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱 <<c0> [ 使用 ADO 執行 SQLXML 4.0 查詢](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 以下為範本執行的結果集：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Contact ContactID="4" LastName="Acevedo" FirstName="Humberto" Title="Sr." />   
</ROOT>  
```  
  
  
