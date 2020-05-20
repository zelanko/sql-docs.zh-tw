---
title: XML 中的階層式記錄集 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchical Recordsets [ADO], in XML
ms.assetid: 5d4b11c4-c94f-4910-b99b-5b9abc50d791
author: rothja
ms.author: jroth
ms.openlocfilehash: 24a5303f4ecd43293508f117b795d389a7608285
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762739"
---
# <a name="hierarchical-recordsets-in-xml"></a>XML 中的階層式資料錄集
ADO 允許將階層式記錄集物件保存到 XML。 使用階層式記錄集物件時，父記錄集中的欄位值是另一個記錄集。 這類欄位會表示為 XML 資料流程中的子項目，而不是屬性。  
  
## <a name="remarks"></a>備註  
 下列範例示範這種情況：  
  
```  
Rs.Open "SHAPE {select stor_id, stor_name, state from stores} APPEND ({select stor_id, ord_num, ord_date, qty from sales} AS rsSales RELATE stor_id TO stor_id)", "Provider=MSDataShape;DSN=pubs;Integrated Security=SSPI;"  
```  
  
 下列是持續性記錄集的 XML 格式：  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"     xmlns:dt="uuid:C2F41010-65B3-11d1-A29F-00AA00C14882"     xmlns:rs="urn:schemas-microsoft-com:rowset"   
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
  
 以這種方式保存父記錄集中的資料行時，它的確切順序並不明顯。 父系中的任何欄位都可能包含子記錄集。 持續性提供者會先將所有純量資料行當做屬性來保存，然後將所有子記錄集「資料行」保存為父資料列的子項目。 您可以藉由查看記錄集的架構定義，取得父記錄集中之欄位的序數位置。 每個欄位都有一個 OLE DB 屬性 rs： number，其定義于記錄集架構命名空間中，其中包含該欄位的序數。  
  
 子記錄集中所有欄位的名稱都會與包含這個子系之父記錄集內的功能變數名稱進行串連。 這是為了確保在父和子記錄集都包含從兩個不同的資料表取得的欄位，但名為 singularly 的情況下，沒有名稱衝突。  
  
 將階層式記錄集儲存至 XML 時，您應該注意 ADO 中的下列限制：  
  
-   具有暫止更新的階層式記錄集無法保存至 XML。  
  
-   使用參數化圖形命令所建立的階層式記錄集不能保存（XML 或 ADTG 格式）。  
  
-   ADO 目前會將父系和子記錄集之間的關聯性儲存為二進位大型物件（BLOB）。 用來描述此關聯性的 XML 標記尚未定義于資料列集架構命名空間中。  
  
-   儲存階層式記錄集時，會連同所有子記錄集一起儲存。 如果目前的記錄集是另一個記錄集的子系，則不會儲存其父系。 會儲存構成目前記錄集之子樹的所有子記錄集。  
  
 當階層式記錄集從其 XML 保存格式重新開啟時，您必須注意下列限制：  
  
-   如果子記錄包含沒有對應父記錄的記錄，則不會在階層式記錄集的 XML 表示中寫出這些資料列。 因此，當記錄集從其保存的位置重新開啟時，這些資料列將會遺失。  
  
-   如果子記錄有多個父記錄的參考，則在重新開啟記錄集時，子記錄集可能會包含重複的記錄。 不過，只有在使用者直接處理基礎子資料列集時，才會顯示這些重複專案。 如果使用章節來導覽子記錄集（這是流覽 ADO 的唯一方法），則不會顯示這些重複專案。  
  
## <a name="see-also"></a>另請參閱  
 [以 XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)
