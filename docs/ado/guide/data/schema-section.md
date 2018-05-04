---
title: 結構描述 > 一節 |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Schema section [ADO]
ms.assetid: 4ac6e524-2c92-48e8-b871-0a4b5c8fda18
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7614a2c23d21d88652c32fef480367df4db65be8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="schema-section"></a>結構描述 > 一節
需要結構描述 」 一節。 如先前範例所示，ADO 將保留的資料值語意盡可能更新每個資料行的相關寫出詳細的中繼資料。 不過，若要載入 XML 中，ADO 只需要資料行和其所屬的資料列集的名稱。 最小的結構描述的範例如下：  
  
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
  
 在上述範例中，ADO 會將資料視為可變長度的字串是因為沒有型別資訊已包含結構描述中。  
  
## <a name="creating-aliases-for-column-names"></a>建立資料行名稱的別名  
 Rs: name 屬性，可讓您建立的資料行名稱的別名，讓易記名稱可能會出現在資料列集所公開的資料行資訊，而可能使用較短的名稱，在資料區段。 例如，先前的結構描述無法修改即貨運公司編號對應至 s1、 s2 的 CompanyName 和電話號碼，以 s3，如下所示：  
  
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
  
 然後，在資料區段的資料列會使用 name 屬性 （而非 rs： 名稱） 來參考該資料行：  
  
```  
"<row s1="1" s2="Speedy Express" s3="(503) 555-9831"/>  
```  
  
 建立別名的資料行名稱是必要，每當資料行名稱不是有效的屬性或在 XML 中的標記名稱。 例如，"LastName"必須要有別名由於有內嵌空格的名稱是無效的屬性。 下列程式不會正確處理 XML 剖析器，因此您必須建立別名，以其他沒有內嵌的空格的名稱。  
  
```  
<row last name="Jones"/>  
```  
  
 不論您使用的名稱屬性的值必須使用一致的資料行參考結構描述和資料的 XML 文件的各節中的每個位置。 下列範例示範使用 s1 一致：  
  
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
  
 同樣地，因為沒有定義別名的`CompanyName`在前一個範例中，`CompanyName`必須一致地使用整個文件。  
  
## <a name="data-types"></a>資料型別  
 您可以套用 dt: type 屬性的資料行的資料類型。 若要允許 XML 類型的最後指南，請參閱資料類型 區段中的[W3C XML 資料的規格](http://www.w3.org/TR/1998/NOTE-XML-data/)。 您可以指定資料類型有兩種： 直接在本身的資料行定義上指定 dt: type 屬性或 s:datatype 建構做為資料行定義的巢狀項目。 例如，  
  
```  
<s:AttributeType name="Phone" >  
  <s:datatype dt:type="string"/>  
</s:AttributeType>  
```  
  
 相當於  
  
```  
<s:AttributeType name="Phone" dt:type="string"/>  
```  
  
 如果您省略 dt: type 屬性完全與資料列定義，根據預設，資料行的類型就是可變長度字串。  
  
 如果您有多個型別資訊比只是型別名稱 （例如，dt: maxlength 而言），它會更容易閱讀，若要使用 s:datatype 子項目。 這是只使用慣例，不過，不一定。  
  
 下列範例進一步示範如何在您的結構描述中包含型別資訊。  
  
```  
<!-- 1. String with no max length -->  
<s:AttributeType name="title_id"/>  
<!—or -->  
<s:AttributeType name="title_id" dt:type="string"/>  
  
<!—- 2. Fixed length string with max length of 6 -->  
<s:AttributeType name="title_id">  
    <s:datatype dt:type="string" dt:maxLength="6" rs:fixedlength="true" />  
</s:AttributeType>  
  
<!—- 3. Variable length string with max length of 6 -->  
<s:AttributeType name="title_id">  
    <s:datatype dt:type="string" dt:maxLength="6" />  
</s:AttributeType>  
  
<!—- 4. Integer -->  
<s:AttributeType name="title_id" dt:type="int"/>  
```  
  
 沒有在第二個範例的 rs: fixedlength 屬性的細微用法。 Rs: fixedlength 屬性的資料行設定為 true，表示資料必須擁有結構描述中定義的長度。 在此情況下，title_id 有效的值為"123456，"因為"123"。 不過，「 123 」 不會有效因為它的長度為 3，不是 6。 請參閱更 fixedlength 屬性的完整描述的 OLE DB 程式設計人員指南。  
  
## <a name="handling-nulls"></a>處理 null 值  
 Null 值是由 rs: maybenull 屬性處理。 如果這個屬性設為 true，資料行的內容可以包含 null 值。 此外，如果資料列中找不到資料行，從資料列集讀取資料的使用者將從 Irowset 得到 null 狀態。 請考慮下列資料行定義從貨運公司資料表。  
  
```  
<s:AttributeType name="ShipperID">  
  <s:datatype dt:type="int" dt:maxLength="4"/>  
</s:AttributeType>  
<s:AttributeType name="CompanyName">  
  <s:datatype dt:type="string" dt:maxLength="40" rs:maybenull="true"/>  
</s:AttributeType>  
```  
  
 定義允許`CompanyName`不得為 null，但`ShipperID`不能包含 null 值。 如果資料區段包含下列資料列中，持續性提供者可以將資料的狀態`CompanyName`OLE DB 狀態常數 DBSTATUS_S_ISNULL 的資料行：  
  
```  
<z:row ShipperID="1"/>  
```  
  
 如果資料列完全空白的如下所示，將持續性提供者會傳回 OLE DB 的狀態為 DBSTATUS_E_UNAVAILABLE`ShipperID`和 CompanyName 的 DBSTATUS_S_ISNULL。  
  
```  
<z:row/>   
```  
  
 請注意，零長度字串不為 null 一樣。  
  
```  
<z:row ShipperID="1" CompanyName=""/>  
```  
  
 針對先前的資料列，持續性提供者會傳回 OLE DB 的狀態 DBSTATUS_S_OK 兩個資料行。 `CompanyName`在此情況下只是""（零長度字串）。  
  
 OLE DB 的進一步資訊建構可供使用的 XML 文件結構描述中的 OLE DB，請參閱的定義 」 描述 urn:-microsoft-com:rowset 」 和 OLE DB 程式設計人員指南 》。  
  
## <a name="see-also"></a>另請參閱  
 [以 XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)
