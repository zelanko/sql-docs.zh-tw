---
title: id 函數 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:id function
- id function
ms.assetid: de99fc60-d0ad-4117-a17d-02bdde6512b4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 80bb427800f57ddaa07e5e53f21b03df9e8317d3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62933685"
---
# <a name="functions-on-sequences---id"></a>序列的相關函式 - id
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  傳回含有 xs: id 值的一或多個 xs: idref 值中提供的值相符的元素節點序列 *$arg*。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:id($arg as xs:IDREF*) as element()*  
```  
  
## <a name="arguments"></a>引數  
 *$arg*  
 一個或多個 xs:IDREF 值。  
  
## <a name="remarks"></a>備註  
 函數的結果是依照文件順序之 XML 執行個體中的元素序列，其中 xs:ID 值等於適用 xs:IDREF 的清單中之一或多個 xs:IDREF。  
  
 如果 xs:IDREF 值與任何元素不相符，函數會傳回空白時序。  
  
## <a name="examples"></a>範例  
 本主題提供 XQuery 範例，針對 XML 執行個體儲存於各種**xml**類型資料行中的[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]資料庫。  
  
### <a name="a-retrieving-elements-based-on-the-idref-attribute-value"></a>A. 根據 IDREF 屬性值擷取元素  
 下列範例會使用 fn: id 來擷取 <`employee`> 項目，根據 IDREF 經理屬性。 在此範例中，經理屬性是 IDREF 類型屬性，而且 eid 屬性是 ID 類型屬性。  
  
 對於特定的經理屬性值， **id （)** 函數會尋找 <`employee`> 元素，其 ID 類型屬性值符合輸入的 IDEF 值。 換句話說，針對特定的員工而言**id （)** 函式會傳回員工主管。  
  
 在範例中執行了下列動作：  
  
-   建立 XML 結構描述集合。  
  
-   具型別**xml**變數由使用 XML 結構描述集合。  
  
-   此查詢會擷取含有 ID 屬性值所參考的項目**經理**IDREF 屬性的 <`employee`> 項目。  
  
```  
-- If exists, drop the XML schema collection (SC).  
-- drop xml schema collection SC  
-- go  
  
create xml schema collection SC as  
'<schema xmlns="http://www.w3.org/2001/XMLSchema" xmlns:e="emp" targetNamespace="emp">  
            <element name="employees" type="e:EmployeesType"/>  
            <complexType name="EmployeesType">  
                 <sequence>  
                      <element name="employee" type="e:EmployeeType" minOccurs="0" maxOccurs="unbounded" />  
                 </sequence>  
            </complexType>    
  
            <complexType name="EmployeeType">  
                        <attribute name="eid" type="ID" />  
                        <attribute name="name" type="string" />  
                        <attribute name="manager" type="IDREF" />  
            </complexType>         
</schema>'  
go  
```  
  
```  
declare @x xml(SC)  
set @x='<e:employees xmlns:e="emp">  
<employee eid="e1" name="Joe" manager="e10" />  
<employee eid="e2" name="Bob" manager="e10" />  
<employee eid="e10" name="Dave" manager="e10" />  
</e:employees>'  
  
select @x.value(' declare namespace e="emp";   
 (fn:id(e:employees/employee[@name="Joe"]/@manager)/@name)[1]', 'varchar(50)')   
Go  
```  
  
 該查詢所傳回的值為 "Dave"。 這表示 Dave 是 Joe 的經理。  
  
### <a name="b-retrieving-elements-based-on-the-orderlist-idrefs-attribute-value"></a>B. 根據 OrderList IDREFS 屬性值擷取元素  
 在下列範例中的 OrderList 屬性 <`Customer`> 項目為 IDREFS 類型屬性。 它列出特定客戶的 id 順序。 對於每個訂單 id、 <`Order`> 項目底下的子系 <`Customer`> 提供順序值。  
  
 查詢運算式 `data(CustOrders:Customers/Customer[1]/@OrderList)[1]` 會從第一個客戶的 IDRES 清單擷取第一個值。 此值接著會傳遞給**id （)** 函式。 函數接著會尋找 <`Order`> 元素的 OrderID 屬性值符合的輸入**id （)** 函式。  
  
```  
drop xml schema collection SC  
go  
create xml schema collection SC as  
'<schema xmlns="http://www.w3.org/2001/XMLSchema" xmlns:Customers="Customers" targetNamespace="Customers">  
            <element name="Customers" type="Customers:CustomersType"/>  
            <complexType name="CustomersType">  
                        <sequence>  
                            <element name="Customer" type="Customers:CustomerType" minOccurs="0" maxOccurs="unbounded" />  
                        </sequence>  
            </complexType>  
             <complexType name="OrderType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="OrderValue" type="integer" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="OrderID" type="ID" />  
            </complexType>  
  
            <complexType name="CustomerType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="spouse" type="string" minOccurs="0" maxOccurs="unbounded"/>  
                                <element name="Order" type="Customers:OrderType" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="CustomerID" type="string" />  
                <attribute name="OrderList" type="IDREFS" />  
            </complexType>  
 </schema>'  
go  
declare @x xml(SC)  
set @x='<CustOrders:Customers xmlns:CustOrders="Customers">  
                <Customer CustomerID="C1" OrderList="OrderA OrderB"  >  
                              <spouse>Jenny</spouse>  
                                <Order OrderID="OrderA"><OrderValue>11</OrderValue></Order>  
                                <Order OrderID="OrderB"><OrderValue>22</OrderValue></Order>  
  
                </Customer>  
                <Customer CustomerID="C2" OrderList="OrderC OrderD" >  
                                <spouse>John</spouse>  
                                <Order OrderID="OrderC"><OrderValue>33</OrderValue></Order>  
                                <Order OrderID="OrderD"><OrderValue>44</OrderValue></Order>  
  
                        </Customer>  
                <Customer CustomerID="C3"  OrderList="OrderE OrderF" >  
                                <spouse>Jane</spouse>  
                                <Order OrderID="OrderE"><OrderValue>55</OrderValue></Order>  
                                <Order OrderID="OrderF"><OrderValue>55</OrderValue></Order>  
                </Customer>  
                <Customer CustomerID="C4"  OrderList="OrderG"  >  
                                <spouse>Tim</spouse>  
                                <Order OrderID="OrderG"><OrderValue>66</OrderValue></Order>  
                        </Customer>  
                <Customer CustomerID="C5"  >  
                </Customer>  
                <Customer CustomerID="C6" >  
                </Customer>  
                <Customer CustomerID="C7"  >  
                </Customer>  
</CustOrders:Customers>'  
select @x.query('declare namespace CustOrders="Customers";  
  id(data(CustOrders:Customers/Customer[1]/@OrderList)[1])')  
  
-- result  
<Order OrderID="OrderA">  
  <OrderValue>11</OrderValue>  
</Order>  
```  
  
### <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 不支援的兩個引數版本**id （)** 。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 需要的引數類型**id （)** 是 xs: idref * 的子型別。  
  
## <a name="see-also"></a>另請參閱  
 [在序列上的函式](https://msdn.microsoft.com/library/672d2795-53ab-49c2-bf24-bc81a47ecd3f)  
  
  
