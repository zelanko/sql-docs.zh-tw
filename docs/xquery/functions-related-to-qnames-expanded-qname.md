---
title: 展開-QName (XQuery) |Microsoft Docs
description: '瞭解如何使用擴充的 QName ( # A1 函式來傳回 QName 的命名空間 URI 和本機名稱部分。'
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
- expanded-QName function
- fn:expanded-QName function
ms.assetid: b8377042-95cc-467b-9ada-fe43cebf4bc3
author: rothja
ms.author: jroth
ms.openlocfilehash: d1a59104b8becec2edd8b4b15c28e13e19011a4b
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036821"
---
# <a name="functions-related-to-qnames---expanded-qname"></a>與 QNames 相關的函式 - expanded-QName
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  傳回 xs： QName 類型的值，其中包含在 *$paramURI* 中指定的命名空間 URI，以及 *$paramLocal*中指定的本機名稱。 如果 *$paramURI* 為空字串或空的序列，則表示沒有任何命名空間。  
  
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
 下列適用于 **擴充的 QName ( # B1 ** 函數：  
  
-   如果指定的 *$paramLocal* 值不是 Xs： NCName 類型的正確詞法格式，則會傳回空的序列，並表示動態錯誤。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 不支援從 xs:QName 類型轉換成任何其他類型。 因此， **擴充的 QName ( # B1 ** 函數無法用於 XML 結構中。 例如，當您建構節點時，例如 `<e> expanded-QName(...) </e>`，該值必須為不具類型。 您將需要將 `expanded-QName()` 傳回的 xs:QName 類型值轉換成 xdt:untypedAtomic。 不過，並不支援此轉換。 本主題稍後將在範例中提供解決方案。  
  
-   您無法修改或比較現有的 QName 類型值。 例如，將專案的 `/root[1]/e[1] eq expanded-QName("http://nsURI" "myNS")` 值（<`e`>）與 **展開-QName ( # B1 ** 函數所傳回的 qname 進行比較。  
  
## <a name="examples"></a>範例  
 本主題針對 XML 實例提供 XQuery 範例，這些實例是儲存在資料庫的各種 **XML** 類型資料行中 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 。  
  
### <a name="a-replacing-a-qname-type-node-value"></a>A. 取代 QName 類型節點值  
 此範例說明您可以如何修改 QName 類型的元素節點值。 本範例將執行下列動作：  
  
-   建立 XML 結構描述集合，以定義 QName 類型的元素。  
  
-   使用 xml 架構集合，建立具有 **xml** 型別資料行的資料表。  
  
-   在資料表中儲存 XML 執行個體。  
  
-   使用 xml 資料類型的 **modify ( # B1 ** 方法來修改實例中 QName type 元素的值。 **展開的 qname ( # B1**函數用來產生新的 qname 類型值。  
  
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
<Root xmlns="QNameXSD" xmlns:ns="https://myURI">  
      <ElemQN>ns:someName</ElemQN>  
</Root>')  
go  
-- Verify the insertion  
SELECT * from T  
go  
-- Result  
<Root xmlns="QNameXSD" xmlns:ns="https://myURI">  
  <ElemQN>ns:someName</ElemQN>  
</Root>   
```  
  
 在下列查詢中， `ElemQN` 會使用 xml 資料類型的 **modify ( # B1 ** 方法和 xml DML 的 replace 值來取代 <> 元素值，如下所示。  
  
```  
-- the value.  
UPDATE T   
SET XmlCol.modify('  
  declare default element namespace "QNameXSD";   
  replace value of /Root[1]/ElemQN   
  with expanded-QName("https://myURI", "myLocalName") ')  
go  
-- Verify the result  
SELECT * from T  
go  
```  
  
 以下是結果。 請注意， `ElemQN`> QName 類型 <的專案現在有新的值：  
  
```  
<Root xmlns="QNameXSD" xmlns:ns="urn">  
  <ElemQN xmlns:p1="https://myURI">p1:myLocalName</ElemQN>  
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
 **展開的 QName**函數不能用在 XML 結構中。 下列範例將說明這點。 若要解決這個限制，該範例會先插入一個節點，然後修改該節點。  
  
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
insert into T values ('<root xmlns:a="https://someURI">a:b</root>')  
 go  
-- Verify  
SELECT *   
FROM T  
```  
  
 下列嘗試會新增另一個 <`root`> 元素，但會失敗，因為 XML 結構中不支援擴充的 QName ( # A1 函數。  
  
```  
update T SET xmlCol.modify('  
insert <root>{expanded-QName("http://ns","someLocalName")}</root> as last into / ')  
go  
```  
  
 解決方法是先使用 <> 專案的值插入實例 `root` ，然後加以修改。 在此範例中，當插入 <> 元素時，會使用 nil 初始值 `root` 。 此範例中的 XML 架構集合允許 <> 元素的 nil 值 `root` 。  
  
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
  
 `<root xmlns:a="https://someURI">a:b</root>`  
  
 `<root xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:p1="http://ns">p1:someLocalName</root>`  
  
 您可以比較 QName 值，如下列查詢所示。 查詢只會傳回 `root` 其值符合 **展開-qname ( # B1 ** 函數所傳回之 QName 類型值的 <> 元素。  
  
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
 有一項限制： **展開的 QName ( # B1 ** 函數接受空的序列做為第二個引數，而且在第二個引數不正確時，會傳回空的，而不會引發執行階段錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [QNames &#40;XQuery&#41;的相關函數 ]()  
  
