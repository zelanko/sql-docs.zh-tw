---
title: 資料區段 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data section [ADO]
ms.assetid: 43dc42a8-7057-48e6-93d6-880d5c5c51a4
author: rothja
ms.author: jroth
ms.openlocfilehash: 2d6b03137e920be036d1dd47cb4612076247fa3f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761094"
---
# <a name="data-section"></a>資料區段
Data 區段會定義資料列集的資料，以及任何暫止的更新、插入或刪除。 Data 區段可以包含零個或多個資料列。 它只能包含一個資料列集的資料，其中的資料列是由架構所定義。 此外，如先前所述，可以省略沒有任何資料的資料行。 如果在 data 區段中使用屬性或子項目，而且架構區段中尚未定義該結構，則會以無訊息方式略過。  
  
## <a name="string"></a>String  
 文字資料中的保留 XML 字元必須以適當的字元實體取代。 例如，在公司名稱「Joe 的車庫」中，單引號必須由實體取代。 實際的資料列如下所示：  
  
```  
<z:row CompanyName="Joe's Garage"/>  
```  
  
 下列字元會保留在 XML 中，而且必須取代成字元實體： {'，"，&， \< ，>}。  
  
## <a name="binary"></a>Binary  
 二進位資料為 bin。以十六進位編碼（也就是一個位元組對應到兩個字元，每個半位元組一個字元）。  
  
## <a name="datetime"></a>Datetime  
 XML 資料類型不直接支援 variant VT_DATE 格式。 具有資料和時間元件之日期的正確格式為 yyyy-mm-dd ddThh： mm： ss。  
  
 如需 XML 所指定之日期格式的詳細資訊，請參閱[W3C XML 資料規格](https://go.microsoft.com/fwlink/?LinkId=5692)。  
  
 當 XML 資料規格定義兩個相等的資料類型（例如，i4 = = int）時，ADO 會寫出易記名稱，但同時讀取兩者。  
  
## <a name="managing-pending-changes"></a>管理暫止的變更  
 記錄集可以在 [立即] 或 [批次更新] 模式中開啟。 當它們在具有用戶端資料指標的批次更新模式中開啟時，對記錄集所做的所有變更都會處於暫止狀態，直到呼叫 UpdateBatch 方法為止。 儲存記錄集時，也會保存暫止的變更。 在 XML 中，它們是使用 urn：架構-microsoft-com：資料列集中定義的 "update" 元素來表示。 此外，如果資料列集可以更新，在資料列的定義中，可更新的屬性必須設定為 true。 例如，若要定義 [貨主] 資料表包含暫止的變更，資料列定義看起來會像下面這樣。  
  
```  
<s:ElementType name="row" content="eltOnly" updatable="true">  
  <s:attribute type="ShipperID"/>  
  <s:attribute type="CompanyName"/>  
  <s:attribute type="Phone"/>  
  <s:extends type="rs:rowbase"/>  
</s:ElementType>  
```  
  
 這會告知持續性提供者呈現資料，讓 ADO 可以建立可更新的記錄集物件。  
  
 下列範例資料顯示在保存的檔案中，插入、變更和刪除的外觀。  
  
```  
<rs:data>  
  <z:row ShipperID="2" CompanyName="United Package"   
    Phone="(503) 555-3199"/>  
<rs:update>  
  <rs:original>  
    <z:row ShipperID="3" CompanyName="Federal Shipping"   
      Phone="(503) 555-9931"/>  
  </rs:original>  
  <z:row Phone="(503) 552-7134"/>  
</rs:update>  
<rs:insert>  
  <z:row ShipperID="12" CompanyName="Lightning Shipping"   
    Phone="(505) 111-2222"/>  
  <z:row ShipperID="13" CompanyName="Thunder Overnight"   
    Phone="(505) 111-2222"/>  
  <z:row ShipperID="14" CompanyName="Blue Angel Air Delivery"   
    Phone="(505) 111-2222"/>  
</rs:insert>  
<rs:delete>  
  <z:row ShipperID="1" CompanyName="Speedy Express" Phone="(503) 555-9831"/>  
</rs:delete>  
</rs:data>  
```  
  
 更新一律包含整個原始資料列資料，後面接著變更的資料列資料。 已變更的資料列可能會包含所有資料行，或只包含實際變更的資料行。 在上述範例中，[貨主 2] 的資料列不會變更，而且只有 [電話] 資料行已變更 [貨主 3] 的值，因此，只有變更的資料列中才會包含唯一的資料行。 針對貨主12、13和14所插入的資料列會在一個 rs： insert 標記下一起批次處理。 請注意，已刪除的資料列也可以批次處理在一起，不過上述範例中不會顯示這種情況。  
  
## <a name="see-also"></a>另請參閱  
 [以 XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)
