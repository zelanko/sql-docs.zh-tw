---
description: XML 保存格式
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 081ba6f2b82e6369d2871a2c9c7352c7335bc0d4
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88758978"
---
# <a name="xml-persistence-format"></a>XML 保存格式
ADO 會針對其保存的 XML 資料流程使用 UTF-8 編碼。  
  
 ADO XML 格式分為兩個區段，也就是架構區段，後面接著 data 區段。 以下是來自 Northwind 資料庫之貨主資料表的範例 XML 檔。 下列範例會討論 XML 的各個部分。  
  
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
  
 架構會顯示命名空間的宣告、架構區段和資料區段。 [架構] 區段包含資料列、ShipperID、公司名稱和電話的定義。  
  
 架構定義符合 [W3C XML 資料規格](http://www.w3.org/TR/1998/NOTE-XML-data/) ，而且可以完全驗證 (但 Internet Explorer 5) 中不會進行驗證。 XML 資料是目前唯一支援的記錄集持續性架構格式。  
  
 Data 區段有三個數據列，其中包含有關貨主的資訊。 如果是空的資料列集，資料區段可能是空的，但 \<rs:data> 必須有標記。 如果沒有任何資料，您就可以直接撰寫標記速記 \<rs:data/> 。 任何前面加上 "rs" 的標記，表示它位於 urn：架構-microsoft-com：資料列集所定義的命名空間中。  
  
## <a name="see-also"></a>另請參閱  
 [以 XML 格式保存記錄](./persisting-records-in-xml-format.md)