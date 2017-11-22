---
title: "擴充 QName (XQuery) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- expanded-QName function
- fn:expanded-QName function
ms.assetid: b8377042-95cc-467b-9ada-fe43cebf4bc3
caps.latest.revision: "19"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4a688ffc9299e8f00b0b4d8cccd0e33538cbe63d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="functions-related-to-qnames---expanded-qname"></a>函式與 QNames 相關的-Expanded-qname
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  傳回 URI 中指定的命名空間的 xs: qname 類型值*$paramURI*中指定的本機名稱和*$paramLocal*。 如果*$paramURI*是空字串或空的序列，它代表沒有命名空間。  
  
## <a name="syntax"></a>語法  
  
```  
fn:expanded-QName($paramURI as xs:string?, $paramLocal as xs:string?) as xs:QName?  
```  
  
## <a name="arguments"></a>引數  
 *$paramURI*  
 是 QName 的命名空間 URI。  
  
 *$paramLocal*  
 為 QName 的本機名稱部份。  
  
## <a name="remarks"></a>備註  
 下列適用於**expanded-qname （)**函式：  
  
-   如果*$paramLocal*指定值不是 xs: ncname 類型的正確語彙格式，會傳回空的序列，並代表動態錯誤。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 不支援從 xs:QName 類型轉換成任何其他類型。 因為這個緣故， **expanded-qname （)**函式不能用於 XML 建構中。 例如，當您建構節點時，例如 `<e> expanded-QName(…) </e>`，該值必須為不具類型。 您將需要將 `expanded-QName()` 傳回的 xs:QName 類型值轉換成 xdt:untypedAtomic。 不過，並不支援此轉換。 本主題稍後將在範例中提供解決方案。  
  
-   您無法修改或比較現有的 QName 類型值。 例如，`/root[1]/e[1] eq expanded-QName("http://nsURI" "myNS")`比較元素的值 <`e`>，所傳回的 qname **expanded-qname （)**函式。  
  
## <a name="examples"></a>範例  
 本主題提供 XQuery 範例，針對 XML 執行個體儲存在各種**xml**類型資料行中的[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]資料庫。  
  
### <a name="a-replacing-a-qname-type-node-value"></a>A. 取代 QName 類型節點值  
 此範例說明您可以如何修改 QName 類型的元素節點值。 本範例將執行下列動作：  
  
-   建立 XML 結構描述集合，以定義 QName 類型的元素。  
  
-   建立具有資料表**xml**使用 XML 結構描述集合的型別資料行。  
  
-   在資料表中儲存 XML 執行個體。  
  
-   使用**modify （)**方法來修改執行個體中的 QName 類型元素值的 xml 資料類型。 **Expanded-qname （)**函式用來產生新的 QName 類型值。  
  
```  
-- If XML schema collection (if exists)  
-- drop xml schema collection SC  
-- go  
-- Create XML schema collection  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
    xmlns:xs="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="QNameXSD"   
      xmlns:xqo="QNameXSD" elementFormDefault="qualified">  
      <element name="Root" type="xqo:rootType" />  
      <complexType name="rootType">  
            <sequence minOccurs="1" maxOccurs="1">  
                        <element name="ElemQN" type="xs:QName" />  
            </sequence>  
      </complexType>  
</schema>'  
go  
-- Create table.  
CREATE TABLE T( XmlCol xml(SC) )  
-- Insert sample XML instnace  
INSERT INTO T VALUES ('  
<Root xmlns="QNameXSD" xmlns:ns="http://myURI">  
      <ElemQN>ns:someName</ElemQN>  
</Root>')  
go  
-- Verify the insertion  
SELECT * from T  
go  
-- Result  
<Root xmlns="QNameXSD" xmlns:ns="http://myURI">  
  <ElemQN>ns:someName</ElemQN>  
</Root>   
```  
  
 在下列查詢中，<`ElemQN`> 元素的值會取代使用**modify （)** xml 資料類型和 XML DML 所示的取代值的方法。  
  
```  
-- the value.  
UPDATE T   
SET XmlCol.modify('  
  declare default element namespace "QNameXSD";   
  replace value of /Root[1]/ElemQN   
  with expanded-QName("http://myURI", "myLocalName") ')  
go  
-- Verify the result  
SELECT * from T  
go  
```  
  
 以下是結果。 請注意 QName 類型的 <`ElemQN`> 元素現在有一個新值：  
  
```  
<Root xmlns="QNameXSD" xmlns:ns="urn">  
  <ElemQN xmlns:p1="http://myURI">p1:myLocalName</ElemQN>  
</Root>  
```  
  
 下表陳述式會移除範例中所使用的物件。  
  
```  
-- Cleanup  
DROP TABLE T  
go  
drop xml schema collection SC  
go  
```  
  
### <a name="b-dealing-with-the-limitations-when-using-the-expanded-qname-function"></a>B. 使用 expanded-QName() 函數時處理其限制  
 **Expanded-qname**函式不能用於 XML 建構中。 下列範例將說明這點。 若要解決這個限制，該範例會先插入一個節點，然後修改該節點。  
  
```  
-- if exists drop the table T  
--drop table T  
-- go  
-- Create XML schema collection  
-- DROP XML SCHEMA COLLECTION SC  
-- go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" type="QName" nillable="true"/>  
</schema>'  
go  
 -- Create table T with a typed xml column (using the XML schema collection)  
CREATE TABLE T (xmlCol XML(SC))  
go  
-- Insert an XML instance.  
insert into T values ('<root xmlns:a="http://someURI">a:b</root>')  
 go  
-- Verify  
SELECT *   
FROM T  
```  
  
 下列程式碼嘗試加入另一個 <`root`> 元素卻失敗，因為 XML 建構不支援 expanded-QName() 函數。  
  
```  
update T SET xmlCol.modify('  
insert <root>{expanded-QName("http://ns","someLocalName")}</root> as last into / ')  
go  
```  
  
 解決此問題的方法是先為 <`root`> 元素插入一個含值的執行個體，然後修改它。 在此範例中，當插入 <`root`> 元素時，使用了 nil 初始值。 在此範例中的 XML 結構描述集合允許 <`root`> 元素的 nil 值。  
  
```  
update T SET xmlCol.modify('  
insert <root xsi:nil="true"/> as last into / ')  
go  
-- now replace the nil value with another QName.  
update T SET xmlCol.modify('  
replace value of /root[last()] with expanded-QName("http://ns","someLocalName") ')  
go  
 -- verify   
SELECT * FROM T  
go  
-- result  
<root>b</root>  
```  
  
 `<root xmlns:a="http://someURI">a:b</root>`  
  
 `<root xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:p1="http://ns">p1:someLocalName</root>`  
  
 您可以比較 QName 值，如下列查詢所示。 查詢只會傳回 <`root`> 類型的傳回值的元素值符合的 QName **expanded-qname （)**函式。  
  
```  
SELECT xmlCol.query('  
    for $i in /root  
    return  
       if ($i eq expanded-QName("http://ns","someLocalName") ) then  
          $i  
       else  
          ()')  
FROM T  
```  
  
### <a name="implementation-limitations"></a>實作限制  
 會有一個限制： **expanded-qname （)**函式接受空的序列，做為第二個引數，並會傳回空白的而不是第二個引數不正確時引發執行階段錯誤。  
  
## <a name="see-also"></a>請參閱＜  
 [與 QNames &#40; 函式XQuery &#41;](http://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
