---
title: "資料區段 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: data section [ADO]
ms.assetid: 43dc42a8-7057-48e6-93d6-880d5c5c51a4
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fae3df37c9a83bdf97a7ae2a53bc76777b318546
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="data-section"></a>資料區段
資料區段定義以及任何暫止的更新、 插入或刪除資料列集的資料。 資料區段可以包含零或多個資料列。 它只能包含一個資料列集結構描述所定義的資料列所在的資料。 此外，如之前所述，就可以省略資料行沒有任何資料。 如果屬性或子元素用於資料區段中，而且尚未在結構描述 」 一節中定義該建構，則會以無訊息模式忽略。  
  
## <a name="string"></a>字串  
 必須使用適當字元實體取代文字資料中保留的 XML 字元。 比方說，在 公司名稱"Joe 的機庫"單引號必須由實體取代。 實際的資料列，如下所示：  
  
```  
<z:row CompanyName="Joe's Garage"/>  
```  
  
 下列字元是保留在 XML 中，必須將取代字元實體: {'，"，&，\<，>}。  
  
## <a name="binary"></a>二進位  
 二進位資料是 bin.hex 編碼 （也就是一個位元組且對應至兩個字元、 每半字節的一個字元）。  
  
## <a name="datetime"></a>DateTime  
 由 XML 資料的資料類型不直接支援 variant VT_DATE 格式。 如需資料和時間元件包含日期正確的格式是 yyyy-mm-Yyyy-mm-ddthh。  
  
 如需 XML 所指定的日期格式的詳細資訊，請參閱[W3C XML 資料的規格](https://go.microsoft.com/fwlink/?LinkId=5692)。  
  
 當 XML 資料的規格會定義兩個對等資料類型 (例如 i4 = = int)，ADO 會寫出的易記名稱，但在讀取。  
  
## <a name="managing-pending-changes"></a>管理暫止的變更  
 資料錄集可以開啟在 即時運算或批次更新模式。 在與用戶端資料指標的批次更新模式中開啟它們，當資料錄集所做的變更會處於暫止狀態直到 UpdateBatch 方法會呼叫。 暫止的變更也會保存在儲存資料錄集時。 在 XML 中，這些原則由定義在 urn： 結構描述中的 「 更新 」 項目使用-microsoft-com:rowset。 此外，如果可以更新資料列集，可更新的屬性必須設為 true 的資料列定義中。 例如，定義貨運公司資料表包含暫止的變更時，資料列定義會尋找類似下列。  
  
```  
<s:ElementType name="row" content="eltOnly" updatable="true">  
  <s:attribute type="ShipperID"/>  
  <s:attribute type="CompanyName"/>  
  <s:attribute type="Phone"/>  
  <s:extends type="rs:rowbase"/>  
</s:ElementType>  
```  
  
 這會告訴介面的資料持續性提供者，讓 ADO 可以建構可更新的資料錄集物件。  
  
 下列範例資料顯示插入、 變更和刪除的外觀中保存檔。  
  
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
  
 更新一律包含後面接著已變更的資料列資料的整個原始資料列資料。 已變更的資料列可能包含的所有資料行或已實際變更這些資料行。 在上述範例中，託運商 2 的資料列不會變更，且 Phone 資料行已變更的託運商 3 的值，所以包含在已變更的資料列的唯一資料行。 貨運公司 12、 13 和 14 的插入資料列是批次在一起的下一個 rs： 插入標記。 請注意，刪除的資料列也批次處理，雖然這不會顯示在上述範例中。  
  
## <a name="see-also"></a>請參閱＜  
 [以 XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)
