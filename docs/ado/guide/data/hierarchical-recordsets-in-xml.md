---
title: "在 XML 中的階層式資料錄集 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: hierarchical Recordsets [ADO], in XML
ms.assetid: 5d4b11c4-c94f-4910-b99b-5b9abc50d791
caps.latest.revision: "4"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9916333a203309d81228c86c019277c9d5515313
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="hierarchical-recordsets-in-xml"></a>在 XML 中的階層式資料錄集
ADO 允許為 XML 持續性的階層式資料錄集物件。 使用階層式資料錄集物件，在父資料錄集欄位的值會是另一個資料錄集。 這類欄位會表示為 XML 資料流，而不是屬性中的子項目。  
  
## <a name="remarks"></a>備註  
 下列範例將示範此情況下：  
  
```  
Rs.Open "SHAPE {select stor_id, stor_name, state from stores} APPEND ({select stor_id, ord_num, ord_date, qty from sales} AS rsSales RELATE stor_id TO stor_id)", "Provider=MSDataShape;DSN=pubs;Integrated Security=SSPI;"  
```  
  
 以下是 XML 格式的保存資料錄集：  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"     xmlns:dt="uuid:C2F41010-65B3-11d1-A29F-00AA00C14882"     xmlns:rs="urn:schemas-microsoft-com:rowset"   
    xmlns:z="#RowsetSchema">   
  <s:Schema id="RowsetSchema">   
    <s:ElementType name="row" content="eltOnly" rs:updatable="true">   
      <s:AttributeType name="stor_id" rs:number="1"   
        rs:writeunknown="true">   
        <s:datatype dt:type="string" dt:maxLength="4"   
          rs:fixedlength="true" rs:maybenull="false"/>   
      </s:AttributeType>   
      <s:AttributeType name="stor_name" rs:number="2" rs:nullable="true"   
        rs:writeunknown="true">   
          <s:datatype dt:type="string" dt:maxLength="40"/>   
      </s:AttributeType>   
      <s:AttributeType name="state" rs:number="3" rs:nullable="true"   
        rs:writeunknown="true">   
        <s:datatype dt:type="string" dt:maxLength="2"   
          rs:fixedlength="true"/>   
      </s:AttributeType>   
      <s:ElementType name="rsSales" content="eltOnly"   
        rs:updatable="true" rs:relation="010000000100000000000000">   
        <s:AttributeType name="stor_id" rs:number="1"   
          rs:writeunknown="true">   
          <s:datatype dt:type="string" dt:maxLength="4"   
            rs:fixedlength="true" rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:AttributeType name="ord_num" rs:number="2"   
          rs:writeunknown="true">   
          <s:datatype dt:type="string" dt:maxLength="20"   
            rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:AttributeType name="ord_date" rs:number="3"   
          rs:writeunknown="true">   
            <s:datatype dt:type="dateTime" dt:maxLength="16"   
              rs:scale="3" rs:precision="23" rs:fixedlength="true"   
              rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:AttributeType name="qty" rs:number="4" rs:writeunknown="true">   
          <s:datatype dt:type="i2" dt:maxLength="2" rs:precision="5"   
            rs:fixedlength="true" rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:extends type="rs:rowbase"/>   
      </s:ElementType>   
      <s:extends type="rs:rowbase"/>   
    </s:ElementType>   
  </s:Schema>   
  <rs:data>   
    <z:row stor_id="6380" stor_name="Eric the Read Books" state="WA">   
      <rsSales stor_id="6380" ord_num="6871"   
        ord_date="1994-09-14T00:00:00" qty="5"/>   
      <rsSales stor_id="6380" ord_num="722a"   
        ord_date="1994-09-13T00:00:00" qty="3"/>   
    </z:row>   
    <z:row stor_id="7066" stor_name="Barnum's" state="CA">   
      <rsSales stor_id="7066" ord_num="A2976"   
        ord_date="1993-05-24T00:00:00" qty="50"/>   
      <rsSales stor_id="7066" ord_num="QA7442.3"   
        ord_date="1994-09-13T00:00:00" qty="75"/>   
    </z:row>   
    <z:row stor_id="7067" stor_name="News & Brews" state="CA">   
      <rsSales stor_id="7067" ord_num="D4482"   
        ord_date="1994-09-14T00:00:00" qty="10"/>   
      <rsSales stor_id="7067" ord_num="P2121"   
        ord_date="1992-06-15T00:00:00" qty="40"/>   
      <rsSales stor_id="7067" ord_num="P2121"   
        ord_date="1992-06-15T00:00:00" qty="20"/>   
      <rsSales stor_id="7067" ord_num="P2121"   
        ord_date="1992-06-15T00:00:00" qty="20"/>   
    </z:row>   
  </rs:data>   
</xml>   
```  
  
 保存以這種方式時，在父資料錄集資料行的確切順序不明顯。 父系中的任何欄位可能包含子資料錄集。 持續性提供者保存出第一個程式屬性的所有純量資料行，並且再保存為子項目的父資料列的 出所有子資料錄集 」 的資料行 」。 父欄位的序數位置可以藉由查看結構描述定義的資料錄集取得資料錄集。 每個欄位都包含該欄位的序數號碼的資料錄集結構描述命名空間中定義的 OLE DB 屬性 rs： 數字。  
  
 中的子資料錄集的所有欄位的名稱會串連的父資料錄集，其中包含此子系中的欄位名稱。 這是為了確保在父和子資料錄集這兩個包含的欄位，取得兩個不同資料表，但是權責名為的情況下沒有名稱衝突。  
  
 當將階層式資料錄集儲存成 XML 時，您應該注意下列限制在 ADO 中：  
  
-   階層式資料錄集具有擱置更新無法保存為 XML。  
  
-   無法保存以參數化的形狀命令所建立的階層式資料錄集 （以 XML 或 ADTG 格式）。  
  
-   ADO 目前會儲存為二進位大型物件 (BLOB) 的父系和子資料錄集之間的關聯性。 XML 標記來描述此關聯性具有尚未定義資料列集結構描述命名空間中。  
  
-   儲存階層式資料錄集時，所有的子資料錄集會一起儲存它。 如果目前資料錄集是另一個資料錄集的子系，則其父代不會儲存。 所有子系會儲存目前資料錄集的子樹狀結構的資料錄集。  
  
 當階層式資料錄集重新開啟從其 XML 保存的格式，您必須注意下列限制：  
  
-   如果子記錄包含沒有對應的父記錄會的記錄，這些資料列不會寫出的階層式資料錄集的 XML 表示中。 因此，這些資料列將會遺失資料錄集重新開啟從持續性的位置時。  
  
-   如果子記錄中有一個以上的父記錄的參考，然後在重新開啟資料錄集時，子資料錄集可能包含重複的記錄。 不過，這些重複項目才會顯示如果使用者直接使用基礎的子資料列集。 如果章用於巡覽資料錄集 （亦即透過 ADO 來瀏覽的唯一方式） 的子系，請重複的項目不會顯示。  
  
## <a name="see-also"></a>請參閱  
 [以 XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)
