---
title: 使用 sql:使用 cdata (SQLXML) 建立 CDATA 節
description: 瞭解如何使用 sql:use-cdata 註解在 SQLXML 4.0 中創建 CDATA 部分,以轉義包含標記字元的文本塊。
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- markup characters [SQLXML]
- special characters [SQLXML]
- use-cdata annotation
- plain text [SQLXML]
- CDATA sections
- escaping blocks of text [SQLXML]
- annotated XSD schemas, CDATA sections
- sql:use-cdata
ms.assetid: 26d2b9dc-f857-44ff-bcd4-aaf64ff809d0
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: aa359c1c1e855c3652d7c6486d3993f588bae46d
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388196"
---
# <a name="creating-cdata-sections-using-sqluse-cdata-sqlxml-40"></a>使用 sql:use-cdata 建立 CDATA 區段 (SQLXML 4.0)

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  在 XML 中，CDATA 區段可用來逸出包含字元的文字區塊，否則這些字元會被辨識為標記字元。  
  
 Microsoft[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的資料庫有時可以包含 XML 解析器視為標記字元的字元;例如,角括弧(<和>)、小於或等於符號 (<+)和符號(&)被視為標記字元。 但是，您可以將這類型的特殊字元包裝在 CDATA 區段內，以免被視為標記字元。 XML 剖析器會將 CDATA 區段內的文字視為純文字。  
  
 **sql:use-cdata**註釋用於指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回 的數據應包裝在 CDATA 節中(即,它指示由**sql:field**指定的列中的值是否應包含在 CDATA 節中)。 **sql:use-cdata**註釋只能在映射到資料庫列的元素上指定。  
  
 **sql:use-cdata**註釋採用布爾值(0 = 假,1 = true)。 可接受的值為 0、1、true 和 false。  
  
 此註釋不能與**sql:url 編碼**或 ID、IDREF、IDREFS、NMTOKEN 和 NMTOKENS 屬性類型一起使用。  
  
## <a name="examples"></a>範例  
 若要使用下列範例建立工作範例，您必須符合某些需求。 有關詳細資訊,請參閱執行[SQLXML 範例的要求](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-specifying-sqluse-cdata-on-an-element"></a>A. 在元素上指定 sql:use-cdata  
 在以下架構中,**\<位址**>元素中的**\<AddressLine1>** 的**sql:use-cdata**設定為 1(True)。 因此，資料會在 CDATA 區段內傳回。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Address"   
               sql:relation="Person.Address"   
               sql:key-fields="AddressID" >  
   <xsd:complexType>  
        <xsd:sequence>  
          <xsd:element name="AddressID"  type="xsd:string" />  
          <xsd:element name="AddressLine1" type="xsd:string"   
                       sql:use-cdata="1" />  
        </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>針對結構描述測試範例 XPath 查詢  
  
1.  複製上述的結構描述程式碼，並將其貼到文字檔中。 將檔案儲存為 UseCData.xml。  
  
2.  複製下列範本，並將其貼到文字檔中。 將檔案儲存為 UseCDataT.xml 並放在與 UseCData.xml 相同的目錄中。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="UseCData.xml">  
            /Address[AddressID < 11]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     針對對應結構描述 (UseCData.xml) 指定的目錄路徑，相對於儲存範本的目錄。 您也可以指定絕對路徑，例如：  
  
    ```  
    mapping-schema="C:\SqlXmlTest\UseCData.xml"  
    ```  
  
3.  建立和使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行範本。  
  
     有關詳細資訊,請參閱使用[ADO 執行 SQLXML 4.0 查詢](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 這是部分結果集：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Address>   
    <AddressID>1</CustomerID>   
    <AddressLine1>   
      <![CDATA[ 1970 Napa Ct.  ]]>   
    </AddressLine1>   
  </Address>  
  <Address>  
    <AddressLine1>   
      <![CDATA[ 9833 Mt. Dias Blv. ]]>   
    </AddressLine1>   
  </Address>  
  ...  
</ROOT>  
```  
  
  
