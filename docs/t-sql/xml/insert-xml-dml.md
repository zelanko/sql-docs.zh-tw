---
title: insert (XML DML) | Microsoft Docs
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
- inserting nodes
- insert keyword [XML DML]
- insert XML DML statement
ms.assetid: 0c95c2b3-5cc2-4c38-9e25-86493096c442
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 95cf1eaa68e429d18456d7f0f9490b700efad3db
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68051294"
---
# <a name="insert-xml-dml"></a>insert (XML DML)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  將一個或多個節點 (由 *Expression1* 識別) 插入為其他節點 (由 *Expression2* 識別) 的子節點或同層級節點。  
  
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
 識別一或多個要插入的節點。 這可以是固定的 XML 執行個體、修改方法套用所在之相同 XML 結構描述集合的具類型 XML 資料類型執行個體的參考、使用獨立 **sql:column()** /**sql:variable()** 函數之不具類型的 XML 資料類型執行個體，或是 XQuery 運算式。 運算式可產生節點、文字節點，或經過排序的節點序列。 它不能解析成根 (/) 節點。 如果運算式會產生一個值或值的序列，這些值會以單一文字節點插入，並以空格隔開序列中的每個值。 如果您指定多個節點做為常數，這些節點會以括號括住，並以逗點隔開。 您不能插入異質性序列，例如含有元素、屬性或值的序列。 如果 *Expression1* 解析成空的序列，則不會進行插入，也不會傳回錯誤。  
  
 into  
 將 *Expression1* 所識別的節點插入為 *Expression2* 所識別之節點的直接下階 (子節點)。 如果 *Expression2* 中的節點已經有一或多個子節點，則必須使用 **as first** 或 **as last** 來指定您要加入新節點的位置。 例如，分別在子節點清單的開頭或結尾。 插入屬性時，會忽略 **as first** 和 **as last** 關鍵字。  
  
 after  
 將 *Expression1* 所識別的節點直接插入為 *Expression2* 所識別之節點後面的同層級節點。 **after** 關鍵字不能用來插入屬性。 例如，它不能用來插入屬性建構函式，或是從 XQuery 傳回屬性。  
  
 before  
 將 *Expression1* 所識別的節點直接插入為 *Expression2* 所識別之節點前面的同層級節點。 插入屬性時，不能使用 **before** 關鍵字。 例如，它不能用來插入屬性建構函式，或是從 XQuery 傳回屬性。  
  
 *Expression2*  
 識別節點。 *Expression1* 所識別的節點會以相對於 *Expression2* 所識別的節點來插入。 這可以是會傳回目前所參考文件中節點之參考的 XQuery 運算式。 如果傳回不止一個節點，則插入會失敗。 如果 *Expression2* 傳回空的序列，則不會進行插入，也不會傳回錯誤。 如果 *Expression2* 在靜態上並非單一，則會傳回靜態錯誤。 *Expression2* 不可以是處理指示、註解或屬性。 請注意，*Expression2* 必須是文件中現有節點的參考，而不是建構的節點。  
  
## <a name="examples"></a>範例  
  
### <a name="a-inserting-element-nodes-into-the-document"></a>A. 將元素節點插入文件中  
 下列範例說明如何將元素插入文件中。 首先，將 XML 文件指派給 **xml** 類型的變數。 然後，此範例透過數個 **insert** XML DML 陳述式，來說明如何將元素節點插入文件中。 在每一個插入之後，SELECT 陳述式會顯示結果。  
  
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
 在下列範例中，會先將文件指派給 **xml** 類型的變數。 然後，會將連續的兩個元素 (代表產品功能) 指派給 **xml** 類型的第二個變數。 然後將這一連串的元素插入第一個變數中。  
  
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
 下列範例說明如何將屬性插入文件。 首先，將文件指派給 **xml** 類型的變數。 然後，使用一連串 **insert** XML DML 陳述式，將屬性插入文件中。 在每一個屬性插入之後，SELECT 陳述式會顯示結果。  
  
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
 在此查詢中，先將 XML 文件指派給 **xml** 類型的變數。 然後，使用 XML DML 將註解節點插入到第一個 <`step`> 元素的後面。  
  
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
 在下列查詢中，先將 XML 文件指派給 **xml** 類型的變數。 然後，使用 XML DML 關鍵字，在文件開頭處插入處理指示。  
  
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
 當您所插入文字中包含對 XML 無效的字元 (例如 < 或 >)，您可以使用 CDATA 區段來插入資料，如下列查詢所示。 此查詢會指定 CDATA 區段，但區段會加入為文字節點，且任何無效字元都會轉換成實體。 例如，'<' 會另存為 &lt;。  
  
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
 在此查詢中，先將 XML 文件指派給 **xml** 類型的變數。 然後，使用 XML DML，將文字節點插入為 <`Root`> 元素的第一個子節點。 會使用文字建構函式來指定此文字。  
  
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
 下列範例會套用 XML DML，更新儲存在 **xml** 類型資料行中的 XML 執行個體：  
  
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
 在下列範例中，將 IF 條件指定為 **insert** XML DML 陳述式中 Expression1 的一部份。 如果條件為 True，則會將屬性新增至 <`WorkCenter`> 元素中。  
  
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
  
 下列範例很類似，只不過當條件為 True 時，**insert** XML DML 陳述式會將元素插入文件中。 也就是說，如果 <`WorkCenter`> 元素小於或等於兩個 <`step`> 子元素。  
  
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
 此範例會將元素和屬性插入到儲存在具類型 **xml** 資料行的製造指示 XML 中。  
  
 在此範例中，您先在 AdventureWorks 資料庫中建立一個包含具類型的 **xml** 資料行的資料表 (T)。 接著便從 ProductModel 資料表的 Instructions 資料行，將製造指示 XML 執行個體複製成 T 資料表，然後套用插入至 T 資料表中的 XML。  
  
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
declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
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
declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";             
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
 [XML 資料修改語言 &#40;XML DML&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
