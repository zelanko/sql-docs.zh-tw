---
description: 結構描述區段
title: 架構區段 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Schema section [ADO]
ms.assetid: 4ac6e524-2c92-48e8-b871-0a4b5c8fda18
author: rothja
ms.author: jroth
ms.openlocfilehash: a1f294e9c0258f1cc9d108d1eb9a47087b456ca8
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979719"
---
# <a name="schema-section"></a>結構描述區段
需要架構區段。 如先前的範例所示，ADO 會寫出每個資料行的詳細中繼資料，盡可能地保留資料值的語法以進行更新。 不過，若要在 XML 中載入，ADO 只需要資料行的名稱和它們所屬的資料列集。 以下是基本架構的範例：  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"  
    xmlns:rs="urn:schemas-microsoft-com:rowset"  
    xmlns:z="#RowsetSchema">  
  <s:Schema id="RowsetSchema">  
    <s:ElementType name="row" content="eltOnly">  
      <s:AttributeType name="ShipperID"/>  
      <s:AttributeType name="CompanyName"/>  
      <s:AttributeType name="Phone"/>  
      <s:Extends type="rs:rowbase"/>  
    </s:ElementType>  
  </s:Schema>  
  <rs:data>  
...  
  </rs:data>  
</xml>  
```  
  
 在上述範例中，ADO 會將資料視為可變長度的字串，因為架構中沒有包含任何類型資訊。  
  
## <a name="creating-aliases-for-column-names"></a>建立資料行名稱的別名  
 Rs： name 屬性可讓您建立資料行名稱的別名，如此一來，資料列集所公開的資料行資訊中可能會出現易記的名稱，而且可能會在資料區段中使用較短的名稱。 例如，您可以修改先前的架構，將 ShipperID 對應至 s1、將其視為 s2 和 Phone 至 s3，如下所示：  
  
```  
<s:Schema id="RowsetSchema">   
<s:ElementType name="row" content="eltOnly" rs:updatable="true">   
<s:AttributeType name="s1" rs:name="ShipperID" rs:number="1" ...>   
...  
</s:AttributeType>   
<s:AttributeType name="s2" rs:name="CompanyName" rs:number="2" ...>   
...  
</s:AttributeType>   
<s:AttributeType name="s3" rs:name="Phone" rs:number="3" ...>   
...  
</s:AttributeType>   
...  
</s:ElementType>   
</s:Schema>  
```  
  
 然後，在 [資料] 區段中，資料列會使用名稱屬性 (不是 rs： name) 參考該資料行：  
  
```  
"<row s1="1" s2="Speedy Express" s3="(503) 555-9831"/>  
```  
  
 每當資料行名稱不是 XML 的有效屬性或標記名稱時，就需要建立資料行名稱的別名。 例如，"LastName" 必須有別名，因為具有內嵌空格的名稱是不正確屬性。 XML 剖析器不會正確處理下列程式程式碼，因此您必須為沒有內嵌空格的其他名稱建立別名。  
  
```  
<row last name="Jones"/>  
```  
  
 任何您用於 name 屬性的值，都必須在每個資料行都是在 XML 檔的架構和資料區段中參考的位置，以一致的方式使用。 下列範例示範如何使用 s1 的一致性：  
  
```  
<s:Schema id="RowsetSchema">  
  <s:ElementType name="row" content="eltOnly">  
    <s:attribute type="s1"/>  
    <s:attribute type="CompanyName"/>  
    <s:attribute type="s3"/>  
    <s:extends type="rs:rowbase"/>  
  </s:ElementType>  
  <s:AttributeType name="s1" rs:name="ShipperID" rs:number="1"   
    rs:maydefer="true" rs:writeunknown="true">  
    <s:datatype dt:type="i4" dt:maxLength="4" rs:precision="10"   
      rs:fixedlength="true" rs:maybenull="true"/>  
  </s:AttributeType>  
</s:Schema>  
<rs:data>  
  <z:row s1="1" CompanyName="Speedy Express" s3="(503) 555-9831"/>  
</rs:data>  
```  
  
 同樣地，因為 `CompanyName` 在先前的範例中並未定義別名，所以 `CompanyName` 必須在整個檔中一致地使用。  
  
## <a name="data-types"></a>資料類型  
 您可以將資料類型套用至具有 dt： type 屬性的資料行。 如需允許的 XML 類型的最終指南，請參閱 [W3C Xml 資料規格](http://www.w3.org/TR/1998/NOTE-XML-data/)的資料類型一節。 您可以使用兩種方式來指定資料類型：直接在資料行定義上指定 dt： type 屬性，或使用 s:datatype 結構做為資料行定義的嵌套元素。 例如，  
  
```  
<s:AttributeType name="Phone" >  
  <s:datatype dt:type="string"/>  
</s:AttributeType>  
```  
  
 相當於  
  
```  
<s:AttributeType name="Phone" dt:type="string"/>  
```  
  
 如果您完全從資料列定義中省略 dt： type 屬性，根據預設，資料行的類型會是可變長度的字串。  
  
 如果您的類型資訊不只是類型名稱 (例如 dt： maxLength) ，它可讓您更容易閱讀使用 s:datatype 子項目。 但這只是慣例，而不是需求。  
  
 下列範例會進一步示範如何在您的架構中包含型別資訊。  
  
```  
<!-- 1. String with no max length -->  
<s:AttributeType name="title_id"/>  
<!-or -->  
<s:AttributeType name="title_id" dt:type="string"/>  
  
<!-- 2. Fixed length string with max length of 6 -->  
<s:AttributeType name="title_id">  
    <s:datatype dt:type="string" dt:maxLength="6" rs:fixedlength="true" />  
</s:AttributeType>  
  
<!-- 3. Variable length string with max length of 6 -->  
<s:AttributeType name="title_id">  
    <s:datatype dt:type="string" dt:maxLength="6" />  
</s:AttributeType>  
  
<!-- 4. Integer -->  
<s:AttributeType name="title_id" dt:type="int"/>  
```  
  
 第二個範例中的 rs： fixedlength 屬性有微妙的用法。 將 rs： fixedlength 屬性設為 true 的資料行，表示資料必須在架構中定義長度。 在此情況下，有效的 title_id 值為 "123456"，也就是 "123"。 不過，"123" 不是有效的，因為它的長度是3，而不是6。 如需 fixedlength 屬性的更完整說明，請參閱 OLE DB 程式設計人員指南。  
  
## <a name="handling-nulls"></a>處理 Null  
 Null 值是由 rs： maybenull 屬性處理。 如果這個屬性設定為 true，則資料行的內容可以包含 null 值。 此外，如果在資料列中找不到資料行，則從資料列集讀取資料的使用者會從 IRowset：：取得 null 狀態， ( # A1。 請考慮下列來自 [貨主] 資料表的資料行定義。  
  
```  
<s:AttributeType name="ShipperID">  
  <s:datatype dt:type="int" dt:maxLength="4"/>  
</s:AttributeType>  
<s:AttributeType name="CompanyName">  
  <s:datatype dt:type="string" dt:maxLength="40" rs:maybenull="true"/>  
</s:AttributeType>  
```  
  
 定義允許為 `CompanyName` null，但 `ShipperID` 不能包含 null 值。 如果 data 區段包含下列資料列，持續性提供者會將資料行的資料狀態設定 `CompanyName` 為 OLE DB 狀態常數 DBSTATUS_S_ISNull：  
  
```  
<z:row ShipperID="1"/>  
```  
  
 如果資料列完全是空的（如下所示），持續性提供者會傳回 DBSTATUS_E_UNAVAILABLE 的 OLE DB 狀態， `ShipperID` 並 DBSTATUS_S_ISNull 為公司。  
  
```  
<z:row/>   
```  
  
 請注意，零長度的字串與 null 不同。  
  
```  
<z:row ShipperID="1" CompanyName=""/>  
```  
  
 針對前一個資料列，持續性提供者會傳回兩個數據行的 OLE DB 狀態為 DBSTATUS_S_OK。 `CompanyName`在此案例中，只是 "" (零長度的字串) 。  
  
 如需可用於 OLE DB 之 XML 檔架構內的 OLE DB 結構的詳細資訊，請參閱 "urn： schema-microsoft-com： rowset" 的定義和 OLE DB 程式設計人員指南。  
  
## <a name="see-also"></a>另請參閱  
 [以 XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)
