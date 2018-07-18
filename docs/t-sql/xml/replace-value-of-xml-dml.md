---
title: replace value of (XML DML) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- XML DML [SQL Server]
- update keyword
- replacement values [XML DML]
- updating node values
- replace value of XML DML statement
ms.assetid: c310f6df-7adf-493b-b56b-8e3143b13ae7
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a7d8c32ecd68c5a19e1846fcf3c5249bb369d47b
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36258930"
---
# <a name="replace-value-of-xml-dml"></a>replace value of (XML DML)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  更新文件中的節點值。  
  
## <a name="syntax"></a>語法  
  
```  
  
replace value of Expression1   
with Expression2  
```  
  
## <a name="arguments"></a>引數  
 *Expression1*  
 識別要更新的值節點。 它必須只識別一個節點。 也就是，*Expression1* 必須是靜態單一的。 如果輸入 XML，節點類型必須是簡單類型。 如果選取多個節點，就會引發錯誤。 如果 *Expression1* 傳回空的序列，將不會發生值取代，而且也不會傳回錯誤。 *Expression1* 必須傳回單一元素且具有簡單類型的內容 (清單或不可部分完成類型)、文字節點或屬性節點。 *Expression1* 不能是聯集類型、複雜類型、處理指示、文件節點或註解節點。 如果它是，將傳回錯誤。  
  
 *Expression2*  
 識別節點的新值。 這可以是傳回簡單類型節點的運算式，因為將會隱含地使用 **data()**。 如果該值是值清單，**update** 陳述式會以該清單取代舊值。 在修改具類型的 XML 執行個體時，*Expression2* 必須是 *Expression*1 的相同類型或子類型。 否則，就會傳回錯誤。 在修改不具類型的 XML 執行個體時，*Expression2* 必須為不可部分完成的運算式。 否則，就會傳回錯誤。  
  
## <a name="examples"></a>範例  
 下列 **replace value of** XML DML 陳述式的範例說明如何更新 XML 文件中的節點。  
  
### <a name="a-replacing-values-in-an-xml-instance"></a>A. 取代 XML 執行個體的值  
 在下列範例中，首先會將文件執行個體指派至 **xml** 類型的變數。 接著，**replace value of** XML DML 陳述式會更新文件中的值。  
  
```  
DECLARE @myDoc xml;  
SET @myDoc = '<Root>  
<Location LocationID="10"   
            LaborHours="1.1"  
            MachineHours=".2" >Manufacturing steps are described here.  
<step>Manufacturing step 1 at this work center</step>  
<step>Manufacturing step 2 at this work center</step>  
</Location>  
</Root>';  
SELECT @myDoc;  
  
-- update text in the first manufacturing step  
SET @myDoc.modify('  
  replace value of (/Root/Location/step[1]/text())[1]  
  with     "new text describing the manu step"  
');  
SELECT @myDoc;  
-- update attribute value  
SET @myDoc.modify('  
  replace value of (/Root/Location/@LaborHours)[1]  
  with     "100.0"  
');  
SELECT @myDoc;  
```  
  
 請注意更新的目標必須在路徑運算式中明確指定最多一個節點，只要在運算式的結尾加入 "[1]" 即可。  
  
### <a name="b-using-the-if-expression-to-determine-replacement-value"></a>B. 使用 if 運算式決定取代值  
 您可以在 **replace value of XML DML** 陳述式的 Expression2 中指定 **if** 運算式，如下列範例所示。 Expression1 識別第一個工作中心內要更新的 LaborHours 屬性。 Expression2 使用 **if** 運算式決定 LaborHours 屬性的新值。  
  
```  
DECLARE @myDoc xml  
SET @myDoc = '<Root>  
<Location LocationID="10"   
            LaborHours=".1"  
            MachineHours=".2" >Manu steps are described here.  
<step>Manufacturing step 1 at this work center</step>  
<step>Manufacturing step 2 at this work center</step>  
</Location>  
</Root>'  
--SELECT @myDoc  
  
SET @myDoc.modify('  
  replace value of (/Root/Location[1]/@LaborHours)[1]  
  with (  
       if (count(/Root/Location[1]/step) > 3) then  
         "3.0"  
       else  
          "1.0"  
      )  
')  
SELECT @myDoc  
```  
  
### <a name="c-updating-xml-stored-in-an-untyped-xml-column"></a>C. 更新儲存在不具類型的 XML 資料行之 XML  
 下列範例會更新儲存在資料行中的 XML：  
  
```  
drop table T  
go  
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
-- verify the current <ProductDescription> element  
SELECT x.query(' /Root/ProductDescription')  
FROM T  
-- update the ProductName attribute value  
UPDATE T  
SET x.modify('  
  replace value of (/Root/ProductDescription/@ProductName)[1]  
  with "New Road Bike" ')  
-- verify the update  
SELECT x.query(' /Root/ProductDescription')  
FROM T  
```  
  
### <a name="d-updating-xml-stored-in-a-typed-xml-column"></a>D. 更新儲存在具類型的 XML 資料行之 XML  
 此範例會取代具類型的 xml 資料行中所儲存的製造指示文件中的值。  
  
 在此範例中，您先在 AdventureWorks 資料庫中建立一個包含具類型的 xml 資料行的資料表 (T)。 接著便從 ProductModel 資料表的 Instructions 資料行，將製造指示 XML 執行個體複製成 T 資料表，然後套用插入至 T 資料表中的 XML。  
  
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
--insert a new location - <Location 1000/>.   
update T  
set Instructions.modify('  
  declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
insert <MI:Location LocationID="1000"  LaborHours="1000"  LotSize="1000" >  
           <MI:step>Do something using <MI:tool>hammer</MI:tool></MI:step>  
         </MI:Location>  
  as first  
  into   (/MI:root)[1]  
')  
go  
select Instructions  
from T  
go  
-- Now replace manu. tool in location 1000  
update T  
set Instructions.modify('  
  declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  replace value of (/MI:root/MI:Location/MI:step/MI:tool)[1]   
  with   "screwdriver"  
')  
go  
select Instructions  
from T  
-- Now replace value of lot size  
update T  
set Instructions.modify('  
  declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  replace value of (/MI:root/MI:Location/@LotSize)[1]   
  with   500 cast as xs:decimal ?  
')  
go  
select Instructions  
from T  
```  
  
 請注意取代 LotSize 值時 **cast** 的用法。 當該值必須是特定類型時就需要使用它。 在此範例中，如果值為 500，就不一定需要明確轉換。  
  
## <a name="see-also"></a>另請參閱  
 [比較具類型的 XML 與不具類型的 XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [建立 XML 資料的執行個體](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 資料類型方法](../../t-sql/xml/xml-data-type-methods.md)   
 [XML 資料修改語言 &#40;XML DML&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
