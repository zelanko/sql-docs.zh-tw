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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 76cd14b8ee1c5a55e0312993090bfaf098c7e219
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702132"
---
# <a name="data-section"></a>資料區段
[資料] 區段會定義以及任何暫止的更新、 插入或刪除資料列集的資料。 [資料] 區段可以包含零個或多個資料列。 它只能包含結構描述所定義的資料列所在的一個資料列集的資料。 此外，如先前所述，就可以省略資料行沒有任何資料。 如果屬性或子元素會在 [資料] 區段，該建構尚未定義在結構描述區段中，它會以無訊息方式忽略。  
  
## <a name="string"></a>String  
 在文字資料中保留的 XML 字元必須以適當的字元實體取代。 比方說，公司名稱 」 Joe 的車庫"，單引號必須取代的實體。 實際的資料列，如下所示：  
  
```  
<z:row CompanyName="Joe's Garage"/>  
```  
  
 下列字元是保留在 XML 中，必須被取代的字元實體: {'，"，&，\<，>}。  
  
## <a name="binary"></a>二進位  
 二進位資料會將編碼 （也就是一個位元組並對應至兩個字元，每半位元組的一個字元）。  
  
## <a name="datetime"></a>Datetime  
 XML 資料的資料類型所不直接支援 variant 的 VT_DATE 格式。 使用資料和時間元件的日期的正確格式為 yyyy-mm-Yyyy-mm-ddthh。  
  
 如需有關 XML 所指定的日期格式的詳細資訊，請參閱[W3C XML 資料的規格](https://go.microsoft.com/fwlink/?LinkId=5692)。  
  
 當 XML 資料的規格會定義兩個對等資料類型 (例如 i4 = = int)，ADO 會寫出好記的名稱，但在讀取。  
  
## <a name="managing-pending-changes"></a>管理暫止的變更  
 資料錄集可以開啟在即時或批次更新模式。 當開啟用戶端資料指標的批次更新模式中時，資料錄集所做的變更會處於擱置狀態 UpdateBatch 方法呼叫之前。 儲存資料錄集時，會也會保存 暫止的變更。 在 XML 中，它們都由使用 「 更新 」 定義的項目在 urn: schemas-microsoft-microsoft-com:rowset。 此外，如果可以更新資料列集，可更新屬性必須設定為定義中的資料列，則為 true。 比方說，若要定義 [Shippers] 表格包含暫止的變更，會定義資料列的外觀類似於下列。  
  
```  
<s:ElementType name="row" content="eltOnly" updatable="true">  
  <s:attribute type="ShipperID"/>  
  <s:attribute type="CompanyName"/>  
  <s:attribute type="Phone"/>  
  <s:extends type="rs:rowbase"/>  
</s:ElementType>  
```  
  
 這會告訴介面的資料持續性提供者，讓 ADO 可以建構可更新的資料錄集物件。  
  
 下列的範例資料會顯示在保存的檔案中外觀插入、 變更和刪除。  
  
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
  
 更新一律會包含整個原始後面接著已變更的資料列資料的資料列資料。 已變更的資料列可能包含的所有資料行或實際上已變更這些資料行。 在上述範例中，託運商 2 的資料列不會變更，並只 Phone 資料行已變更的託運商 3 的值，因此包含在已變更的資料列的唯一資料行。 插入的資料列的貨運公司 12、 13 和 14 是批次放在一起的下一個 rs： 插入標記。 請注意，已刪除的資料列也批次處理，雖然這不會顯示在上述範例中也一樣。  
  
## <a name="see-also"></a>另請參閱  
 [以 XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)
