---
title: 範例：指定 XMLTEXT 指示詞 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XMLTEXT directive
ms.assetid: e78008ec-51e8-4fd1-b86f-1058a781de17
author: rothja
ms.author: jroth
ms.openlocfilehash: 541e214399a0f91c63c5cf053f5a99dafe9fb837
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85013340"
---
# <a name="example-specifying-the-xmltext-directive"></a>範例：指定 XMLTEXT 指示詞
  此範例說明如何在使用 EXPLICIT 模式的 `SELECT` 陳述式中，使用 `XMLTEXT` 指示詞將溢位資料行中的資料定址。  
  
 假設有 `Person` 資料表。 此資料表有一個 `Overflow` 資料行，可用來儲存 XML 文件的未消耗部分。  
  
```  
USE tempdb;  
GO  
CREATE TABLE Person(PersonID varchar(5), PersonName varchar(20), Overflow nvarchar(200));  
GO  
INSERT INTO Person VALUES   
    ('P1','Joe',N'<SomeTag attr1="data">content</SomeTag>')  
   ,('P2','Joe',N'<SomeTag attr2="data"/>')  
   ,('P3','Joe',N'<SomeTag attr3="data" PersonID="P">content</SomeTag>');  
```  
  
 此查詢從 `Person` 資料表擷取資料行。 對於 `Overflow` 資料行，並未指定 *AttributeName*，但「指示詞」  會將 `XMLTEXT` 設為提供通用資料表資料行名稱的一部分。  
  
```  
SELECT 1 as Tag, NULL as parent,  
       PersonID as [Parent!1!PersonID],  
       PersonName as [Parent!1!PersonName],  
       Overflow as [Parent!1!!XMLTEST] -- No AttributeName; XMLTEXT directive  
FROM Person  
FOR XML EXPLICIT;  
```  
  
 在產生的 XML 文件中：  
  
-   因為 *資料行未指定*AttributeName`Overflow`，但指定 `xmltext` 指示詞，所以 <`overflow`> 元素中的屬性會附加到封閉式 <`Parent`> 元素的屬性清單。  
  
-   因為 <`PersonID`> 元素中的 `xmltext` 屬性與在相同元素層級上擷取的 `PersonID` 屬性衝突，所以即使 `xmltext` 為 NULL，還是會忽略 <`PersonID`> 元素中的屬性。 一般而言，屬性會覆寫溢位中相同名稱的屬性。  
  
 以下是結果：  
  
 `<Parent PersonID="P1" PersonName="Joe" attr1="data">content</Parent>`  
  
 `<Parent PersonID="P2" PersonName="Joe" attr2="data"></Parent>`  
  
 `<Parent PersonID="P3" PersonName="Joe" attr3="data">content</Parent>`  
  
 如果溢位資料有子元素而且指定相同的查詢，則 `Overflow` 資料行中的子元素將會新增為封閉式 <`Parent`> 元素的子元素。  
  
 例如，變更 `Person` 資料表中的資料，讓 `Overflow` 資料行現在擁有子元素。  
  
```  
USE tempdb;  
GO  
TRUNCATE TABLE Person;  
GO  
INSERT INTO Person VALUES   
    ('P1','Joe',N'<SomeTag attr1="data">content</SomeTag>')  
   ,('P2','Joe',N'<SomeTag attr2="data"/>')  
    ,('P3','Joe',N'<SomeTag attr3="data" PersonID="P"><name>PersonName</name></SomeTag>');  
```  
  
 如果執行相同的查詢，則 <`xmltext`> 元素中的子元素將會新增為封閉式 <`Parent`> 元素的子元素。  
  
```  
SELECT 1 as Tag, NULL as parent,  
       PersonID as [Parent!1!PersonID],  
       PersonName as [Parent!1!PersonName],  
       Overflow as [Parent!1!!XMLTEXT] -- no AttributeName, XMLTEXT directive  
FROM Person  
FOR XML EXPLICIT;  
```  
  
 以下是結果：  
  
 `<Parent PersonID="P1" PersonName="Joe" attr1="data">content</Parent>`  
  
 `<Parent PersonID="P2" PersonName="Joe" attr2="data"></Parent>`  
  
 `<Parent PersonID="P3" PersonName="Joe" attr3="data">`  
  
 `<name>PersonName</name>`  
  
 `</Parent>`  
  
 如果以 *指示詞指定*AttributeName`xmltext`，則 <`overflow`> 元素的屬性將會新增為封閉式 <`Parent`> 元素的子元素屬性。 為*AttributeName*指定的名稱會成為子項目的名稱。  
  
 在此查詢中， *AttributeName*（<`overflow`>）會與指示詞一起指定 `xmltext` ：  
  
```  
SELECT 1 as Tag, NULL as parent,  
       PersonID as [Parent!1!PersonID],  
       PersonName as [Parent!1!PersonName],  
       Overflow as [Parent!1!overflow!XMLTEXT] -- Overflow is AttributeName  
                      -- XMLTEXT is a directive  
FROM Person  
FOR XML EXPLICIT  
```  
  
 以下是結果：  
  
 `<Parent PersonID="P1" PersonName="Joe">`  
  
 `<overflow attr1="data">content</overflow>`  
  
 `</Parent>`  
  
 `<Parent PersonID="P2" PersonName="Joe">`  
  
 `<overflow attr2="data" />`  
  
 `</Parent>`  
  
 `<Parent PersonID="P3" PersonName="Joe">`  
  
 `<overflow attr3="data" PersonID="P">`  
  
 `<name>PersonName</name>`  
  
 `</overflow>`  
  
 `</Parent>`  
  
 在此查詢元素中， *屬性指定為* directive `PersonName` 。 `PersonName` 的這個結果將會新增為封閉式 <`Parent`> 元素的子元素。 <`xmltext`> 的屬性仍然會附加到封閉式 <`Parent`> 元素。 <`overflow`> 元素的內容 (子元素) 將會附加到封閉式 <`Parent`> 元素的其他子元素前面。  
  
```  
SELECT 1      AS Tag, NULL as parent,  
       PersonID   AS [Parent!1!PersonID],  
       PersonName AS [Parent!1!PersonName!element], -- element directive  
       Overflow   AS [Parent!1!!XMLTEXT]  
FROM Person  
FOR XML EXPLICIT;  
```  
  
 以下是結果：  
  
 `<Parent PersonID="P1" attr1="data">content<PersonName>Joe</PersonName>`  
  
 `</Parent>`  
  
 `<Parent PersonID="P2" attr2="data">`  
  
 `<PersonName>Joe</PersonName>`  
  
 `</Parent>`  
  
 `<Parent PersonID="P3" attr3="data">`  
  
 `<name>PersonName</name>`  
  
 `<PersonName>Joe</PersonName>`  
  
 `</Parent>`  
  
 如果 `XMLTEXT` 資料行資料包含根元素的屬性，這些屬性不會顯示於 XML 資料結構描述中，而且 MSXML 剖析器並不會驗證產生的 XML 文件片段。 例如：  
  
```  
SELECT 1 AS Tag,  
       0 ASParent,  
       N'<overflow a="1"/>' AS 'overflow!1!!xmltext'  
FOR XML EXPLICIT, xmldata;  
```  
  
 以下是結果。 請注意，在傳回的結構描述中，結構描述已經遺漏溢位屬性 `a` ：  
  
 `<Schema name="Schema2"`  
  
 `xmlns="urn:schemas-microsoft-com:xml-data"`  
  
 `xmlns:dt="urn:schemas-microsoft-com:datatypes">`  
  
 `<ElementType name="overflow" content="mixed" model="open">`  
  
 `</ElementType>`  
  
 `</Schema>`  
  
 `<overflow xmlns="x-schema:#Schema2" a="1">`  
  
 `</overflow>`  
  
## <a name="see-also"></a>另請參閱  
 [搭配 FOR XML 使用 EXPLICIT 模式](use-explicit-mode-with-for-xml.md)  
  
  
