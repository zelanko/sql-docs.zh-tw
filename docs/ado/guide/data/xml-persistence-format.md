---
title: XML 保存格式 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XML persistence [ADO], persistence format
ms.assetid: 6e146738-ac4d-47bb-b6cd-d87b2260aead
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2330703450e42e8ddf9bfeed536dd3649d65edf8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63184842"
---
# <a name="xml-persistence-format"></a>XML 保存格式
ADO 使用 utf-8 編碼方式，它會保存為 XML 資料流。  
  
 ADO XML 格式會分成兩個區段，後面接著資料區段的結構描述一節。 以下是從 Northwind 資料庫的貨運公司 資料表的範例 XML 檔案。 下列範例將討論各種組件的 xml。  
  
## <a name="remarks"></a>備註  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"   
xmlns:dt="uuid:C2F41010-65B3-11d1-A29F-00AA00C14882"   
xmlns:rs="urn:schemas-microsoft-com:rowset"   
xmlns:z="#RowsetSchema">   
  <s:Schema id="RowsetSchema">   
    <s:ElementType name="row" content="eltOnly" rs:updatable="true">   
      <s:AttributeType name="ShipperID" rs:number="1"   
        rs:basetable="shippers" rs:basecolumn="ShipperID"  
        rs:keycolumn="true">   
        <s:datatype dt:type="int" dt:maxLength="4" rs:precision="10"   
          rs:fixedlength="true" rs:maybenull="false"/>   
      </s:AttributeType>   
      <s:AttributeType name="CompanyName" rs:number="2"   
        rs:nullable="true" rs:write="true" rs:basetable="shippers"   
        rs:basecolumn="CompanyName">   
        <s:datatype dt:type="string" dt:maxLength="40" />   
      </s:AttributeType>   
      <s:AttributeType name="Phone" rs:number="3" rs:nullable="true"   
        rs:write="true" rs:basetable="shippers"   
        rs:basecolumn="Phone">   
        <s:datatype dt:type="string" dt:maxLength="24"/>   
      </s:AttributeType>   
      <s:extends type="rs:rowbase"/>   
    </s:ElementType>   
  </s:Schema>   
  
  <rs:data>   
    <z:row ShipperID="1" CompanyName="Speedy Express"   
      Phone="(503) 555-9831"/>   
    <z:row ShipperID="2" CompanyName="United Package"   
      Phone="(503) 555-3199"/>   
    <z:row ShipperID="3" CompanyName="Federal Shipping"   
      Phone="(503) 555-9931"/>   
  </rs:data>   
</xml>  
```  
  
 結構描述會顯示宣告的命名空間、 結構描述 區段中和 資料 區段。 結構描述區段包含定義資料列、 即貨運公司編號、 CompanyName 和電話。  
  
 結構描述定義符合[W3C XML 資料的規格](http://www.w3.org/TR/1998/NOTE-XML-data/)並可在 （雖然驗證不會發生在 Internet Explorer 5） 完整驗證。 XML 資料是目前唯一支援的結構描述的格式資料錄集的持續性。  
  
 資料區段會有三個資料列包含貨運公司的相關資訊。 空的資料列集，[資料] 區段可能是空的但\<rs： 資料 > 標記必須存在。 沒有資料，您可以簡單地撰寫標記速記\<rs： 資料 / >。 加上"rs"任何標記表示它是在 urn: schemas-microsoft 所定義的命名空間-microsoft-com:rowset。  
  
## <a name="see-also"></a>另請參閱  
 [以 XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)
