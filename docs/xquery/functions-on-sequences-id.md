---
title: id 函數 (XQuery) |微軟文件
description: 瞭解如何使用 XQuery id 函數按文件順序使用提供的 xs:IDREF 值傳回 XML 實例中的元素序列。
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
ms.openlocfilehash: 45b7f9f7ee9fa301b10c29fafb663c3a307509d7
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388519"
---
# <a name="functions-on-sequences---id"></a>序列的相關函式 - id
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回具有 xs:ID 值的元素節點序列,該值與 *$arg*中提供的一個或多個 xs:IDREF 值的值匹配。  
  
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
 本主題針對儲存在[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]資料庫中各種**xml**類型列中的 XML 實例提供了 XQuery 範例。  
  
### <a name="a-retrieving-elements-based-on-the-idref-attribute-value"></a>A. 根據 IDREF 屬性值擷取元素  
 下面的範例使用fn:id檢索基於`employee`IDREF管理器屬性<>元素。 在此範例中，經理屬性是 IDREF 類型屬性，而且 eid 屬性是 ID 類型屬性。  
  
 對於特定的管理員屬性值 **,id()** 函數查`employee`找 ID 類型屬性值與輸入 IDREF 值匹配<>元素。 換句話說,對於特定員工 **,id()** 函數返回員工經理。  
  
 在範例中執行了下列動作：  
  
-   建立 XML 結構描述集合。  
  
-   使用 XML 架構集合創建類型化**xml**變數。  
  
-   查詢檢索具有由<>`employee`元素**的經理**IDREF 屬性引用的 ID 屬性值的元素。  
  
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
 在下面的示例中,<>`Customer`元素的 OrderList 屬性是 IDREFS 類型屬性。 它列出特定客戶的 id 順序。 對於每個訂單 ID,<>`Order`提供 訂單值的<`Customer`下有一個<>元素子項。  
  
 查詢運算式 `data(CustOrders:Customers/Customer[1]/@OrderList)[1]` 會從第一個客戶的 IDRES 清單擷取第一個值。 然後,此值將傳遞給**id()** 函數。 然後,函數查找orderID`Order`屬性值與**id()** 函數匹配的輸入>元素<。  
  
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
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]不支援**id()** 的兩參數版本。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]要求**id()** 的參數類型是 xs:IDREF*的子類型。  
  
## <a name="see-also"></a>另請參閱  
 [序列的相關函數](https://msdn.microsoft.com/library/672d2795-53ab-49c2-bf24-bc81a47ecd3f)  
  
  
