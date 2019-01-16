---
title: 結構描述區段 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Schema section [ADO]
ms.assetid: 4ac6e524-2c92-48e8-b871-0a4b5c8fda18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 45e8e37d8bb85e727771072abda9249b8155076f
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/14/2019
ms.locfileid: "54256193"
---
# <a name="schema-section"></a>結構描述區段
需要結構描述一節。 如先前範例所示，ADO 會為了保留資料值的語意盡可能更新每個資料行的相關寫出詳細的中繼資料。 不過，若要載入在 XML 中，ADO 只需要資料行和其所屬的資料列集的名稱。 最小的結構描述的範例如下：  
  
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
  
 在上述範例中，ADO 會將資料視為可變長度的字串因為任何型別資訊不包含在結構描述。  
  
## <a name="creating-aliases-for-column-names"></a>建立資料行名稱別名  
 Rs: name 屬性，可讓您建立的資料行名稱的別名，讓易記的名稱可能會出現在資料列集所公開的資料行資訊，並可能使用較短的名稱，在 [資料] 區段中。 比方說，無法修改先前的結構描述，即貨運公司編號對應至 s1，s2，CompanyName 和電話號碼，以 s3，如下所示：  
  
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
  
 接著，在 [資料] 區段中，資料列會使用 name 屬性 （非 rs： 名稱） 來參考該資料行：  
  
```  
"<row s1="1" s2="Speedy Express" s3="(503) 555-9831"/>  
```  
  
 每當資料行名稱不是有效的屬性或 XML 中的標記名稱，建立別名的資料行名稱是必要的。 例如，"LastName"必須要有別名由於有內嵌空格的名稱是無效的屬性。 下面這行不會正確地處理 XML 剖析器，因此您必須建立別名，並沒有內嵌的空格的其他名稱。  
  
```  
<row last name="Jones"/>  
```  
  
 不論您使用 name 屬性的值必須以一致的方式使用，每個資料行參考的結構描述和資料的 XML 文件的各節中的位置。 下列範例顯示使用一致的 s1:  
  
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
  
 同樣地，因為沒有定義別名的`CompanyName`在前一個範例中，`CompanyName`必須以一致的方式使用整個文件。  
  
## <a name="data-types"></a>資料型別  
 您可以套用 dt: type 屬性的資料行的資料類型。 允許的 XML 類型的最後指南，請參閱資料類型 區段中的[W3C XML 資料的規格](http://www.w3.org/TR/1998/NOTE-XML-data/)。 您可以指定資料類型有兩種： 直接在資料行定義本身上指定 dt: type 屬性，或使用 s:datatype 建構為巢狀資料行定義的項目。 例如，  
  
```  
<s:AttributeType name="Phone" >  
  <s:datatype dt:type="string"/>  
</s:AttributeType>  
```  
  
 相當於  
  
```  
<s:AttributeType name="Phone" dt:type="string"/>  
```  
  
 如果您省略 dt: type 屬性完全從資料列定義，根據預設，資料行的類型會是可變長度字串。  
  
 如果您有多個型別資訊比只是型別名稱 (例如 dt: maxlength) 時，它可以更容易閱讀，若要使用 s:datatype 子項目。 這是只使用慣例，不過，並不是需求。  
  
 下列範例進一步示範如何在您的結構描述中包含類型資訊。  
  
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
  
 沒有 rs: fixedlength 屬性，在第二個範例中的細微用法。 Rs: fixedlength 屬性的資料行設定為 true 表示資料必須擁有結構描述中定義的長度。 在此情況下，title_id 的有效值為"123456，"因為"123"。 不過，"123"會不是有效因為其長度是 3，不是 6。 請參閱更 fixedlength 屬性的完整描述的 OLE DB 程式設計人員指南。  
  
## <a name="handling-nulls"></a>處理 Null  
 Null 值是由 rs: maybenull 屬性處理。 如果此屬性設為 true，資料行的內容可以包含 null 值。 此外，如果資料列中找不到資料行，從資料列集讀取資料的使用者會從 IRowset::GetData() 取得 null 的狀態。 請考慮從貨運公司資料表的下列資料行定義。  
  
```  
<s:AttributeType name="ShipperID">  
  <s:datatype dt:type="int" dt:maxLength="4"/>  
</s:AttributeType>  
<s:AttributeType name="CompanyName">  
  <s:datatype dt:type="string" dt:maxLength="40" rs:maybenull="true"/>  
</s:AttributeType>  
```  
  
 定義可讓`CompanyName`不得為 null，但`ShipperID`nemůže obsahovat hodnotu null。 如果 [資料] 區段包含下列資料列，持續性提供者會設定為資料的狀態`CompanyName`OLE DB 狀態常數 DBSTATUS_S_ISNULL 的資料行：  
  
```  
<z:row ShipperID="1"/>  
```  
  
 如果資料列完全空白的如下所示，持續性提供者會傳回 OLE DB 的狀態為 DBSTATUS_E_UNAVAILABLE`ShipperID`和 CompanyName 的 DBSTATUS_S_ISNULL。  
  
```  
<z:row/>   
```  
  
 請注意，長度為零的字串不是 null 相同。  
  
```  
<z:row ShipperID="1" CompanyName=""/>  
```  
  
 上述的資料列中，持續性提供者會傳回 OLE DB 的 DBSTATUS_S_OK 的狀態這兩個資料行。 `CompanyName`只在此情況下是""（零長度字串）。  
  
 之 OLE DB 的進一步資訊建構可用於 XML 文件結構描述中的 OLE DB，請參閱定義的"urn: schemas-microsoft-microsoft-com:rowset 」 和 OLE DB 程式設計人員指南。  
  
## <a name="see-also"></a>另請參閱  
 [以 XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)
