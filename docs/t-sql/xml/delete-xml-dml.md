---
title: delete (XML DML) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- XML DML [SQL Server]
- delete keyword
- delete statement [XML DML]
- deleting nodes
ms.assetid: b22c93a4-b84d-4356-af4c-6013322a4b71
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1e06e1679a8a416bbcdba8d1a2930ccd50f4ce74
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85765647"
---
# <a name="delete-xml-dml"></a>delete (XML DML)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  從 XML 執行個體刪除節點。  
  
## <a name="syntax"></a>語法  
  
```  
  
delete Expression  
```  
  
## <a name="arguments"></a>引數  
 *運算式*  
 是一種 XQuery 運算式，可識別要刪除的節點。 會刪除運算式所選取的所有節點，以及選取節點內所包含的所有節點或值。 如 [insert (XML DML)](../../t-sql/xml/insert-xml-dml.md) 中所述，必須是文件中現有節點的參考。 它不能是建構節點。 運算式不可以是根 (/) 節點。 如果運算式傳回空白時序，就不會發生刪除，也不會傳回錯誤。  
  
## <a name="examples"></a>範例  
  
### <a name="a-deleting-nodes-from-a-document-stored-in-an-untyped-xml-variable"></a>A. 從不具類型的 xml 變數所儲存的文件刪除節點  
 下列範例說明如何從文件刪除各個節點。 首先，將 XML 執行個體指派給 **xml** 類型的變數。 接著，後續的 delete XML DML 陳述式會從文件刪除各個節點。  
  
```  
DECLARE @myDoc xml  
SET @myDoc = '<?Instructions for=TheWC.exe ?>   
<Root>  
 <!-- instructions for the 1st work center -->  
<Location LocationID="10"   
            LaborHours="1.1"  
            MachineHours=".2" >Some text 1  
<step>Manufacturing step 1 at this work center</step>  
<step>Manufacturing step 2 at this work center</step>  
</Location>  
</Root>'  
SELECT @myDoc  
  
-- delete an attribute  
SET @myDoc.modify('  
  delete /Root/Location/@MachineHours  
')  
SELECT @myDoc  
  
-- delete an element  
SET @myDoc.modify('  
  delete /Root/Location/step[2]  
')  
SELECT @myDoc  
  
-- delete text node (in <Location>  
SET @myDoc.modify('  
  delete /Root/Location/text()  
')  
SELECT @myDoc  
  
-- delete all processing instructions  
SET @myDoc.modify('  
  delete //processing-instruction()  
')  
SELECT @myDoc  
```  
  
### <a name="b-deleting-nodes-from-a-document-stored-in-an-untyped-xml-column"></a>B. 從不具類型的 xml 資料行所儲存的文件刪除節點  
 在下列範例中，**delete** XML DML 陳述式會從資料行所儲存的文件，移除 <`Features`> 的第二個子元素。  
  
```  
CREATE TABLE T (i int, x xml)  
go  
INSERT INTO T VALUES(1,'<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>  
</ProductDescription>  
</Root>')  
go  
-- verify the contents before delete  
SELECT x.query(' //ProductDescription/Features')  
FROM T  
-- delete the second feature  
UPDATE T  
SET x.modify('delete /Root/ProductDescription/Features/*[2]')  
-- verify the deletion  
SELECT x.query(' //ProductDescription/Features')  
FROM T  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   [modify() 方法 (xml 資料類型)](../../t-sql/xml/modify-method-xml-data-type.md) 是用以指定 **delete** XML DML 關鍵字。  
  
-   [query() 方法 (xml 資料類型)](../../t-sql/xml/query-method-xml-data-type.md) 是用以查詢文件。  
  
### <a name="c-deleting-nodes-from-a-typed-xml-column"></a>C. 從具類型的 xml 資料行刪除節點  
 此範例會從具類型的 **xml** 資料行中所儲存的製造指示 XML 文件刪除節點。  
  
 在此範例中，您先在 AdventureWorks 資料庫中建立一個包含具類型的 **xml** 資料行的資料表 (T)。 接著便從 ProductModel 資料表的 Instructions 資料行將製造指示 XML 執行個體複製為 T 資料表，並從該文件刪除一或多個節點。  
  
```  
use AdventureWorks  
go  
drop table T  
go  
create table T(ProductModelID int primary key,   
Instructions xml (Production.ManuInstructionsSchemaCollection))  
go  
insert  T   
select ProductModelID, Instructions  
from Production.ProductModel  
where ProductModelID=7  
go  
select Instructions  
from T  
--1) insert <Location 1000/>. Note: <Root> must be singleton in the query  
update T  
set Instructions.modify('  
  declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  insert <MI:Location LocationID="1000"  LaborHours="1000" >  
           These are manu steps at location 1000.   
           <MI:step>New step1 instructions</MI:step>  
           Instructions for step 2 are here  
           <MI:step>New step 2 instructions</MI:step>  
         </MI:Location>  
  as first  
  into   (/MI:root)[1]  
')  
go  
select Instructions  
from T  
  
-- delete an attribute  
update T  
set Instructions.modify('  
  declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  delete(/MI:root/MI:Location[@LocationID=1000]/@LaborHours)   
')  
go  
select Instructions  
from T  
-- delete text in <location>  
update T  
set Instructions.modify('  
  declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  delete(/MI:root/MI:Location[@LocationID=1000]/text())   
')  
go  
select Instructions  
from T  
-- delete 2nd manu step at location 1000  
update T  
set Instructions.modify('  
  declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  delete(/MI:root/MI:Location[@LocationID=1000]/MI:step[2])   
')  
go  
select Instructions  
from T  
-- cleanup  
drop table T  
go  
```  
  
## <a name="see-also"></a>另請參閱  
 [比較具類型的 XML 與不具類型的 XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [建立 XML 資料的執行個體](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 資料類型方法](../../t-sql/xml/xml-data-type-methods.md)   
 [XML 資料修改語言 &#40;XML DML&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
