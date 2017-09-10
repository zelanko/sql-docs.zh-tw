---
title: "insert (XML DML) |Microsoft 文件"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- XML DML [SQL Server]
- inserting nodes
- insert keyword [XML DML]
- insert XML DML statement
ms.assetid: 0c95c2b3-5cc2-4c38-9e25-86493096c442
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9f995a0dcd0b91c0835c4121a7a2072c2a586f35
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="insert-xml-dml"></a>insert (XML DML)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  將一或多個所識別的節點插入*Expression1*做為子節點或所識別的節點的同層級*Expression2*。  
  
## <a name="syntax"></a>語法  
  
```  
  
insert   
      Expression1 (  
                 {as first | as last} into | after | before  
                                    Expression2  
                )  
```  
  
## <a name="arguments"></a>引數  
 *Expression1*  
 識別一或多個要插入的節點。 這可以是常數的 XML 執行個體。相同的 XML 結構描述集合所在的修改方法套用的具類型 XML 資料類型執行個體的參考不具類型的 XML 資料類型執行個體使用獨立**: column （)**/**: variable （)**函式; 或是 XQuery 運算式。 運算式可產生節點、文字節點，或經過排序的節點序列。 它不能解析成根 (/) 節點。 如果運算式會產生一個值或值的序列，這些值會以單一文字節點插入，並以空格隔開序列中的每個值。 如果您指定多個節點做為常數，這些節點會以括號括住，並以逗點隔開。 您不能插入異質性序列，例如含有元素、屬性或值的序列。 如果*Expression1*解析到空白時序，不會進行插入，並不會傳回錯誤。  
  
 into  
 所識別節點*Expression1*以所識別的節點的直接下階 （子節點） 的方式插入*Expression2*。 如果在節點*Expression2*已經有一個或多個子節點，您必須使用**為第一個**或**為最後一個**指定要加入新節點。 例如，分別在子節點清單的開頭或結尾。 **為第一個**和**為上次**關鍵字會被忽略，插入屬性時。  
  
 after  
 所識別節點*Expression1*所識別的節點之後插入成為直接同層級*Expression2*。 **之後**關鍵字不能用來插入屬性。 例如，它不能用來插入屬性建構函式，或是從 XQuery 傳回屬性。  
  
 before  
 所識別節點*Expression1*成為直接同層級所識別的節點之前插入*Expression2*。 **之前**插入屬性時，就無法使用關鍵字。 例如，它不能用來插入屬性建構函式，或是從 XQuery 傳回屬性。  
  
 *Expression2*  
 識別節點。 中所識別的節點*Expression1*相對於所識別的節點會插入*Expression2*。 這可以是會傳回目前所參考文件中節點之參考的 XQuery 運算式。 如果傳回不止一個節點，則插入會失敗。 如果*Expression2*傳回空的序列，插入不會發生而且不會傳回錯誤。 如果*Expression2*在靜態上並非單一，就會傳回靜態錯誤。 *Expression2*不能是處理指示、 註解或屬性。 請注意， *Expression2*必須是文件中現有的節點並不是建構的節點的參考。  
  
## <a name="examples"></a>範例  
  
### <a name="a-inserting-element-nodes-into-the-document"></a>A. 將元素節點插入文件中  
 下列範例說明如何將元素插入文件中。 首先，將 XML 文件指派給變數的**xml**型別。 然後，透過數個**插入**XML DML 陳述式，此範例說明如何將元素節點插入文件中。 在每一個插入之後，SELECT 陳述式會顯示結果。  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;         
SET @myDoc = '<Root>         
    <ProductDescription ProductID="1" ProductName="Road Bike">         
        <Features>         
        </Features>         
    </ProductDescription>         
</Root>'  ;       
SELECT @myDoc;     
-- insert first feature child (no need to specify as first or as last)         
SET @myDoc.modify('         
insert <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>   
into (/Root/ProductDescription/Features)[1]') ;  
SELECT @myDoc ;        
-- insert second feature. We want this to be the first in sequence so use 'as first'         
set @myDoc.modify('         
insert <Warranty>1 year parts and labor</Warranty>          
as first         
into (/Root/ProductDescription/Features)[1]         
')  ;       
SELECT @myDoc  ;       
-- insert third feature child. This one is the last child of <Features> so use 'as last'         
SELECT @myDoc         
SET @myDoc.modify('         
insert <Material>Aluminium</Material>          
as last         
into (/Root/ProductDescription/Features)[1]         
')         
SELECT @myDoc ;        
-- Add fourth feature - this time as a sibling (and not a child)         
-- 'after' keyword is used (instead of as first or as last child)         
SELECT @myDoc  ;       
set @myDoc.modify('         
insert <BikeFrame>Strong long lasting</BikeFrame>   
after (/Root/ProductDescription/Features/Material)[1]         
')  ;       
SELECT @myDoc;  
GO  
```  
  
 請注意，此範例中各個路徑運算式都指定 "[1]" 做為依據靜態類型的必要條件。 這可確保都是單一目標節點。  
  
### <a name="b-inserting-multiple-elements-into-the-document"></a>B. 將多個元素插入文件中  
 在下列範例中，文件第一次指派給變數的**xml**型別。 然後，代表產品功能的兩個元素的順序指派給第二個變數的**xml**型別。 然後將這一連串的元素插入第一個變數中。  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc = N'<Root>             
<ProductDescription ProductID="1" ProductName="Road Bike">             
    <Features> </Features>             
</ProductDescription>             
</Root>';  
DECLARE @newFeatures xml;  
SET @newFeatures = N'<Warranty>1 year parts and labor</Warranty>            
<Maintenance>3 year parts and labor extended maintenance is available</Maintenance>';           
-- insert new features from specified variable            
SET @myDoc.modify('             
insert sql:variable("@newFeatures")             
into (/Root/ProductDescription/Features)[1] ')             
SELECT @myDoc;  
GO  
```  
  
### <a name="c-inserting-attributes-into-a-document"></a>C. 將屬性插入文件中  
 下列範例說明如何將屬性插入文件中。首先，將文件指派給**xml**類型變數。 然後，一系列的**插入**XML DML 陳述式用來將屬性插入文件。 在每一個屬性插入之後，SELECT 陳述式會顯示結果。  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml ;            
SET @myDoc =   
'<Root>             
    <Location LocationID="10" >             
        <step>Manufacturing step 1 at this work center</step>             
        <step>Manufacturing step 2 at this work center</step>             
    </Location>             
</Root>' ;  
SELECT @myDoc  ;          
-- insert LaborHours attribute             
SET @myDoc.modify('             
insert attribute LaborHours {".5" }             
into (/Root/Location[@LocationID=10])[1] ') ;           
SELECT @myDoc  ;          
-- insert MachineHours attribute but its value is retrived from a sql variable @Hrs             
DECLARE @Hrs float ;            
SET @Hrs =.2   ;          
SET @myDoc.modify('             
insert attribute MachineHours {sql:variable("@Hrs") }             
into   (/Root/Location[@LocationID=10])[1] ');            
SELECT @myDoc;             
-- insert sequence of attribute nodes (note the use of ',' and ()              
-- around the attributes.             
SET @myDoc.modify('             
insert (              
           attribute SetupHours {".5" },             
           attribute SomeOtherAtt {".2"}             
        )             
into (/Root/Location[@LocationID=10])[1] ');             
SELECT @myDoc;  
GO  
```  
  
### <a name="d-inserting-a-comment-node"></a>D. 插入註解節點  
 在此查詢中，XML 文件第一次指派給變數的**xml**型別。 然後，使用 XML DML 將註解節點插入到第一個 <`step`> 元素的後面。  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;             
SET @myDoc =   
'<Root>             
    <Location LocationID="10" >             
        <step>Manufacturing step 1 at this work center</step>             
        <step>Manufacturing step 2 at this work center</step>             
    </Location>             
</Root>' ;           
SELECT @myDoc;             
SET @myDoc.modify('             
insert <!-- some comment -->             
after (/Root/Location[@LocationID=10]/step[1])[1] ');            
SELECT @myDoc;  
GO  
```  
  
### <a name="e-inserting-a-processing-instruction"></a>E. 插入處理指示  
 在下列查詢中，XML 文件第一次指派給變數的**xml**型別。 然後，使用 XML DML 關鍵字，在文件開頭處插入處理指示。  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc =   
'<Root>   
    <Location LocationID="10" >   
        <step>Manufacturing step 1 at this work center</step>   
        <step>Manufacturing step 2 at this work center</step>   
    </Location>   
</Root>' ;  
SELECT @myDoc ;  
SET @myDoc.modify('   
insert <?Program = "Instructions.exe" ?>   
before (/Root)[1] ') ;  
SELECT @myDoc ;  
GO  
```  
  
### <a name="f-inserting-data-using-a-cdata-section"></a>F. 使用 CDATA 區段來插入資料  
 當您插入的文字中包含對 XML 無效的字元 (例如 < 或 >)，您可以使用 CDATA 區段來插入資料，如下列查詢所示。 此查詢會指定 CDATA 區段，但區段會加入為文字節點，且任何無效字元都會轉換成實體。 例如，' <' 會另存為&lt;。  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;             
SET @myDoc =   
'<Root>             
    <ProductDescription ProductID="1" ProductName="Road Bike">             
        <Features> </Features>             
    </ProductDescription>             
</Root>' ;            
SELECT @myDoc ;            
SET @myDoc.modify('             
insert <![CDATA[ <notxml> as text </notxml> or cdata ]]>   
into  (/Root/ProductDescription/Features)[1] ') ;   
SELECT @myDoc ;  
GO  
```  
  
 此查詢會將文字節點插入 <`Features`> 元素中：  
  
```  
<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features> <notxml> as text </notxml> or cdata </Features>  
</ProductDescription>  
</Root>       
```  
  
### <a name="g-inserting-text-node"></a>G. 插入文字節點  
 在此查詢中，XML 文件第一次指派給變數的**xml**型別。 然後，使用 XML DML，將文字節點插入為 <`Root`> 元素的第一個子節點。 會使用文字建構函式來指定此文字。  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc = '<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features>  
  
</Features>  
</ProductDescription>  
</Root>'  
SELECT @myDoc;  
set @myDoc.modify('  
 insert text{"Product Catalog Description"}   
 as first into (/Root)[1]  
');  
SELECT @myDoc;  
```  
  
### <a name="h-inserting-a-new-element-into-an-untyped-xml-column"></a>H. 將新元素插入不具類型的 xml 資料行  
 下列範例會套用 XML DML，更新儲存在 XML 執行個體**xml**類型資料行：  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE T (i int, x xml);  
go  
INSERT INTO T VALUES(1,'<Root>  
    <ProductDescription ProductID="1" ProductName="Road Bike">  
        <Features>  
            <Warranty>1 year parts and labor</Warranty>  
            <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
        </Features>  
    </ProductDescription>  
</Root>');  
go  
-- insert a new element  
UPDATE T  
SET x.modify('insert <Material>Aluminium</Material> as first  
  into   (/Root/ProductDescription/Features)[1]  
');  
GO  
```  
  
 同樣地，插入 <`Material`> 元素節點時，路徑運算式必須傳回單一目標。 這是在運算式結尾加入 [1] 來明確指定的。  
  
```  
-- check the update  
SELECT x.query(' //ProductDescription/Features')  
FROM T;  
GO  
```  
  
### <a name="i-inserting-based-on-an-if-condition-statement"></a>I. 依據 if 條件陳述式插入  
 在下列範例中，將 IF 條件指定為中 Expression1 的一部份**插入**XML DML 陳述式。 如果條件為 True，則會將屬性加入 <`WorkCenter`> 元素中。  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc =   
'<Root>  
    <Location LocationID="10" LaborHours="1.2" >  
        <step>Manufacturing step 1 at this work center</step>  
    <step>Manufacturing step 2 at this work center</step>  
    </Location>  
</Root>';  
SELECT @myDoc  
SET @myDoc.modify('  
insert  
if (/Root/Location[@LocationID=10])  
then attribute MachineHours {".5"}  
else ()  
    as first into   (/Root/Location[@LocationID=10])[1] ');  
SELECT @myDoc;  
GO  
```  
  
 下列範例是類似，不同之處在於**插入**XML DML 陳述式將元素插入文件中如果條件為 True。 也就是說，如果 <`WorkCenter`> 元素小於或等於兩個 <`step`> 子元素。  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc =   
'<Root>  
    <Location LocationID="10" LaborHours="1.2" >  
        <step>Manufacturing step 1 at this work center</step>  
        <step>Manufacturing step 2 at this work center</step>  
    </Location>  
</Root>';  
SELECT @myDoc;  
SET @myDoc.modify('  
insert  
if (count(/Root/Location/step) <= 2)  
then element step { "This is a new step" }  
else ()  
    as last into   (/Root/Location[@LocationID=10])[1] ');  
SELECT @myDoc;  
GO  
```  
  
 以下是結果：  
  
```  
<Root>  
 <WorkCenter WorkCenterID="10" LaborHours="1.2">  
  <step>Manufacturing step 1 at this work center</step>  
  <step>Manufacturing step 2 at this work center</step>  
  <step>This is a new step</step>  
 </WorkCenter>  
```  
  
### <a name="j-inserting-nodes-in-a-typed-xml-column"></a>J. 將節點插入具類型的 xml 資料行中  
 此範例中插入元素和屬性儲存在具類型的 XML 製造指示**xml**資料行。  
  
 在範例中，您先建立資料表 (T) 包含具類型**xml** AdventureWorks 資料庫中的資料行。 接著便從 ProductModel 資料表的 Instructions 資料行，將製造指示 XML 執行個體複製成 T 資料表，然後套用插入至 T 資料表中的 XML。  
  
```  
USE AdventureWorks;  
GO            
DROP TABLE T;  
GO             
CREATE TABLE T(ProductModelID int primary key,    
Instructions xml (Production.ManuInstructionsSchemaCollection));  
GO  
INSERT T              
    SELECT ProductModelID, Instructions             
    FROM Production.ProductModel             
    WHERE ProductModelID=7;  
GO             
SELECT Instructions             
FROM T;  
-- now insertion begins             
--1) insert a new manu. Location. The <Root> specified as              
-- expression 2 in the insert() must be singleton.      
UPDATE T   
set Instructions.modify('   
declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
insert <MI:Location LocationID="1000" >   
           <MI:step>New instructions go here</MI:step>   
         </MI:Location>   
as first   
into   (/MI:root)[1]   
') ;  
  
SELECT Instructions             
FROM T ;  
-- 2) insert attributes in the new <Location>             
UPDATE T             
SET Instructions.modify('             
declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";             
insert attribute LaborHours { "1000" }             
into (/MI:root/MI:Location[@LocationID=1000])[1] ');   
GO             
SELECT Instructions             
FROM T ;  
GO             
--cleanup             
DROP TABLE T ;  
GO             
```  
  
## <a name="see-also"></a>另請參閱  
 [比較具類型的 XML 與不具類型的 XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [建立 XML 資料的執行個體](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 資料類型方法](../../t-sql/xml/xml-data-type-methods.md)   
 [XML 資料修改語言 &#40;XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  

