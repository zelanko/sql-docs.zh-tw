---
title: XML 持續性格式 |Microsoft Docs
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
ms.openlocfilehash: e2d1c30546a8466ba9950f31cffdfb9447bd89ed
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923383"
---
# <a name="xml-persistence-format"></a>XML 保存格式
ADO 會針對它保存的 XML 資料流程使用 UTF-8 編碼。  
  
 ADO XML 格式分成兩個區段，一個是架構區段，後面接著資料區段。 以下是 Northwind 資料庫的「貨主」資料表的範例 XML 檔案。 下列範例會討論 XML 的各個部分。  
  
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
  
 架構會顯示命名空間、架構區段和資料區段的宣告。 [架構] 區段包含資料列、ShipperID、公司名稱和電話的定義。  
  
 架構定義符合[W3C XML 資料規格](http://www.w3.org/TR/1998/NOTE-XML-data/)，而且可以完整驗證（雖然 Internet Explorer 5 不會進行驗證）。 XML-資料是目前唯一支援的記錄集持續性架構格式。  
  
 Data 區段有三個數據列，其中包含有關貨主的資訊。 如果是空的資料列集，data 區段可能是空的\<，但是 rs： data> 標記必須存在。 在沒有資料的情況下，您可以將標記速記\<撰寫為單純的 rs： data/>。 任何前面加上 "rs" 的標記都會指出它位於 urn：架構-microsoft-com：資料列集所定義的命名空間中。  
  
## <a name="see-also"></a>另請參閱  
 [以 XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)
