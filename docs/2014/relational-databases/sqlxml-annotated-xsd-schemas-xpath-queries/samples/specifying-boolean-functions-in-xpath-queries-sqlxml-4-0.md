---
title: 在 XPath 查詢 (SQLXML 4.0) 中指定布林函數 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], Boolean functions
- false function
- not function [SQLXML]
- true function
- Boolean functions
ms.assetid: c72cd333-9294-4d41-84f2-1748bf20e3eb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d0960fa50551b3279f97b289892d7b544c5a9e6d
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/22/2019
ms.locfileid: "66012389"
---
# <a name="specifying-boolean-functions-in-xpath-queries-sqlxml-40"></a>在 XPath 查詢中指定布林函數 (SQLXML 4.0)
  下列範例顯示如何在 XPath 查詢中指定布林函數。 這些範例中的 XPath 查詢會針對 SampleSchema1.xml 中包含的對應結構描述來指定。 如需此範例結構描述資訊，請參閱[範例註解式 XSD 結構描述 XPath 範例的&#40;SQLXML 4.0&#41;](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)。  
  
## <a name="examples"></a>範例  
  
## <a name="a-specify-the-not-boolean-function"></a>A. 指定 not() 布林函數  
 此查詢會傳回所有 **\<客戶 >** 的內容節點的子項目沒有 **\<順序 >** 子項目：  
  
```  
/child::Customer[not(child::Order)]  
```  
  
 `child` 軸是預設值。 因此，此查詢可以指定為：  
  
```  
/Customer[not(Order)]  
```  
  
#### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>針對對應的結構描述測試 XPath 查詢  
  
1.  複製[結構描述程式碼範例](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)並將它貼到文字檔。 將檔案儲存為 SampleSchema1.xml。  
  
2.  建立下列範本 (BooleanFunctionsA.xml)，並將其儲存在儲存 SampleSchema1.xml 的目錄中。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        Customer[not(Order)]  
    </sql:xpath-query>  
    </ROOT>  
    ```  
  
     針對對應結構描述 (SampleSchema1.xml) 指定的目錄路徑相對於儲存範本的目錄。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱 <<c0> [ 使用 ADO 執行 SQLXML 4.0 查詢](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 以下為範本執行的部分結果集：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customer CustomerID="13" SalesPersonID="286" TerritoryID="7" AccountNumber="13" CustomerType="S" />   
  <Customer CustomerID="32" SalesPersonID="289" TerritoryID="8" AccountNumber="32" CustomerType="S" />   
  <Customer CustomerID="35" SalesPersonID="275" TerritoryID="2" AccountNumber="35" CustomerType="S" />   
  ...  
</ROOT>  
```  
  
## <a name="b-specify-the-true-and-false-boolean-functions"></a>B. 指定 true() 和 false() 布林函數  
 此查詢會傳回所有 **\<客戶 >** 項目子系內容節點沒有 **\<順序 >** 子項目。 在關聯式詞彙中，此查詢會傳回尚未下任何訂單的所有客戶。  
  
```  
/child::Customer[child::Order=false()]  
```  
  
 `child` 軸是預設值。 因此，此查詢可以指定為：  
  
```  
/Customer[Order=false()]  
```  
  
 這個查詢相當於下列語法：  
  
```  
/Customer[not(Order)]  
```  
  
 下列查詢會傳回至少已經下了一個訂單的所有客戶：  
  
```  
/Customer[Order=true()]  
```  
  
 這個查詢相當於下列語法：  
  
```  
/Customer[Order]  
```  
  
#### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>針對對應的結構描述測試 XPath 查詢  
  
1.  複製[結構描述程式碼範例](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)並將它貼到文字檔。 將檔案儲存為 SampleSchema1.xml。  
  
2.  建立下列範本 (BooleanFunctionsB.xml)，並將其儲存在儲存 SampleSchema1.xml 的目錄中。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /Customer[Order=false()]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     針對對應結構描述 (SampleSchema1.xml) 指定的目錄路徑相對於儲存範本的目錄。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     如需詳細資訊，請參閱 <<c0> [ 使用 ADO 執行 SQLXML 4.0 查詢](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 以下為範本執行的部分結果集：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customer CustomerID="13" SalesPersonID="286" TerritoryID="7" AccountNumber="13" CustomerType="S" />   
  <Customer CustomerID="32" SalesPersonID="289" TerritoryID="8" AccountNumber="32" CustomerType="S" />   
  <Customer CustomerID="35" SalesPersonID="275" TerritoryID="2" AccountNumber="35" CustomerType="S" />   
  ...  
</ROOT>  
```  
  
  
