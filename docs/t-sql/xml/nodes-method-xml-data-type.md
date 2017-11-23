---
title: "nodes （) 方法 (xml 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- nodes() method
- nodes method
ms.assetid: 7267fe1b-2e34-4213-8bbf-1c953822446c
caps.latest.revision: "39"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: e083c0b7376b1cac9433e19eee8fc25c93ea09b4
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="nodes-method-xml-data-type"></a>nodes() 方法 (xml 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **Nodes （)**方法很有用，當您想要切割**xml**成關聯式資料的資料類型執行個體。 它可以讓您識別會對應至新資料列的節點。  
  
 每個**xml**資料類型執行個體具有隱含提供的內容節點。 針對儲存在資料行或變數中的 XML 執行個體，這是指文件節點。 文件節點是隱含的節點上方的每個**xml**資料類型執行個體。  
  
 結果**nodes （)**方法是包含的原始 XML 執行個體的邏輯副本的資料列集。 在這些邏輯副本中，每個資料列執行個體的內容節點，都會設成可用查詢運算式來識別的節點之一，讓後續的查詢能夠比對這些內容節點來進行導覽。  
  
 您可以從資料列集中擷取多個值。 例如，您可以套用**value （)**方法所傳回的資料列集來**nodes （)**和原始 XML 執行個體中擷取多個值。 請注意， **value （)**方法套用至 XML 執行個體時傳回只有一個值。  
  
## <a name="syntax"></a>語法  
  
```  
  
nodes (XQuery) as Table(Column)  
```  
  
## <a name="arguments"></a>引數  
 *XQuery*  
 是字串常值，一個 XQuery 運算式。 如果查詢運算式建構了節點，所建構的這些節點會公開在結果資料列集中。 如果查詢運算式的結果是空的序列，資料列集也會是空的。 如果查詢運算式以靜態方式產生了序列 (其中包含不可部分完成的值) 而不是產生節點，則會引發靜態錯誤。  
  
 *資料表*(*資料行*)  
 是結果資料列集的資料表名稱和資料行名稱。  
  
## <a name="remarks"></a>備註  
 舉例來說，假設您有下列資料表：  
  
```  
T (ProductModelID int, Instructions xml)  
```  
  
 資料表中儲存了下列製造指示文件。 這裡只顯示部份片段。 請注意，文件中有三個製造位置。  
  
```  
<root>  
  <Location LocationID="10"...>  
     <step>...</step>  
     <step>...</step>  
      ...  
  </Location>  
  <Location LocationID="20" ...>  
       ...  
  </Location>  
  <Location LocationID="30" ...>  
       ...  
  </Location>  
</root>  
```  
  
 A`nodes()`查詢運算式的方法引動過程`/root/Location`會傳回三個資料列與資料列集，每個包含的邏輯複本的原始 XML 文件，與內容項目設定為其中一個`<Location>`節點：  
  
```  
Product  
ModelID      Instructions  
----------------------------------  
1       <root>  
             <Location LocationID="20" ... />  
             <Location LocationID="30" .../></root>  
1      <root><Location LocationID="10" ... />  
  
             <Location LocationID="30" .../></root>  
1      <root><Location LocationID="10" ... />  
             <Location LocationID="20" ... />  
             </root>  
```  
  
 您可以使用，以再查詢這個資料列集**xml**資料類型方法。 下列查詢會針對所產生的每個資料列，擷取其中內容項目的子樹：  
  
```  
SELECT T2.Loc.query('.')  
FROM   T  
CROSS APPLY Instructions.nodes('/root/Location') as T2(Loc)   
```  
  
 以下是結果：  
  
```  
ProductModelID  Instructions  
----------------------------------  
1        <Location LocationID="10" ... />  
1        <Location LocationID="20" ... />  
1        <Location LocationID="30" .../>  
```  
  
 請注意，所傳回的資料列集保留了類型資訊。 您可以套用**xml**資料類型方法，例如**query （)**， **value （)**， **exist （)**，和**nodes （)**結果的**nodes （)**方法。 不過，您無法套用**modify （)**方法來修改 XML 執行個體。  
  
 此外，也不能將資料列集中的內容節點具體化。 意即，您不能將它用在 SELECT 陳述式中。 但是您可以將它用在 IS NULL 及 COUNT(*) 中。  
  
 使用案例**nodes （)**方法是使用一樣[OPENXML &#40;TRANSACT-SQL &#41;](../../t-sql/functions/openxml-transact-sql.md). 它會提供 XML 的資料列集檢視。 不過，您沒有使用資料指標，當您使用**nodes （)**包含 XML 文件的幾個資料列的資料表上的方法。  
  
 請注意，所傳回的資料列集**nodes （)**方法是未命名的資料列集。 因此，您必須用別名來明確地加以命名。  
  
 **Nodes （)**函式不能直接套用到使用者定義函數的結果。 若要使用**nodes （)**函式與純量使用者定義函數的結果，您可以在使用者定義函數的結果指派給變數，或使用衍生的資料表將資料行別名指派給使用者定義函式傳回值，然後使用 CROSS APPLY 從別名選取。  
  
 下列範例顯示使用 `CROSS APPLY` 從使用者自訂函數的結果中選取的一個方式。  
  
```  
USE AdventureWorks;  
GO  
  
CREATE FUNCTION XTest()  
RETURNS xml  
AS  
BEGIN  
RETURN '<document/>';  
END;  
GO  
  
SELECT A2.B.query('.')  
FROM  
(SELECT dbo.XTest()) AS A1(X)   
CROSS APPLY X.nodes('.') A2(B);  
GO  
  
DROP FUNCTION XTest;  
GO  
```  
  
## <a name="examples"></a>範例  
  
### <a name="using-nodes-method-against-a-variable-of-xml-type"></a>針對 xml 類型的變數來使用 nodes() 方法  
 在下列範例中，有一個 XML 文件，其中含有一個 <`Root`> 最上層元素及三個 <`row`> 子元素。 此查詢使用 `nodes()` 方法設定個別的內容節點，每個 <`row`> 元素各設定一個內容節點。 `nodes()` 方法會傳回含有三個資料列的資料列集。 每個資料列都有一個原始 XML 的邏輯副本，其中每個內容節點都在原始文件中識別不同的 <`row`> 元素。  
  
 接著，查詢會從每個資料列傳回內容節點：  
  
```  
DECLARE @x xml   
SET @x='<Root>  
    <row id="1"><name>Larry</name><oflw>some text</oflw></row>  
    <row id="2"><name>moe</name></row>  
    <row id="3" />  
</Root>'  
SELECT T.c.query('.') AS result  
FROM   @x.nodes('/Root/row') T(c)  
GO  
```  
  
 以下為結果。 在此範例中，查詢方法會傳回內容項目及其內容：  
  
```  
<row id="1"><name>Larry</name><oflw>some text</oflw></row>  
<row id="2"><name>moe</name></row>  
<row id="3"/>  
```  
  
 將父系存取子套用在內容節點上，會為所有的三個資料列傳回 <`Root`> 元素：  
  
```  
SELECT T.c.query('..') AS result  
FROM   @x.nodes('/Root/row') T(c)  
go  
```  
  
 以下是結果：  
  
```  
<Root>  
    <row id="1"><name>Larry</name><oflw>some text</oflw></row>  
    <row id="2"><name>moe</name></row>  
    <row id="3" />  
</Root>  
<Root>  
    <row id="1"><name>Larry</name><oflw>some text</oflw></row>  
    <row id="2"><name>moe</name></row>  
    <row id="3" />  
</Root>  
<Root>  
    <row id="1"><name>Larry</name><oflw>some text</oflw></row>  
    <row id="2"><name>moe</name></row>  
    <row id="3" />  
</Root>  
```  
  
### <a name="specifying-the-nodes-method-against-a-column-of-xml-type"></a>針對 xml 類型的資料行來指定 nodes() 方法  
 自行車製造指示會使用在此範例中，並且儲存在指示**xml**類型資料行的**ProductModel**資料表。  
  
 在下列範例中，`nodes()`方法針對指定`Instructions`資料行**xml**輸入`ProductModel`資料表。  
  
 `nodes()` 方法藉由指定 `/MI:root/MI:Location` 路徑，將 <`Location`> 元素設為內容節點。 結果資料列集包含原始文件的邏輯副本 (文件中的每個 <`Location`> 節點各有一個副本)，且其內容節點設為 <`Location`> 元素。 因此，`nodes()` 函數會提供一組 <`Location`> 內容節點。  
  
 用於此資料列集的 `query()` 方法會要求 `self::node`，所以會傳回每個資料列的 `<Location>` 元素。  
  
 在此範例中，查詢在特定產品型號的製造指示文件中，將每個 <`Location`> 元素都設成內容節點。 您可以使用這些內容節點來擷取值，如下所示：  
  
-   在每個尋找位置識別碼 <`Location`>  
  
-   擷取製造步驟 (<`step`> 子元素) 中每個 <`Location`>  
  
 此查詢會傳回內容項目，其中在 `'.'` 方法中指定了 `self::node()` 的 `query()` 縮寫語法。  
  
 請注意下列事項：  
  
-   `nodes()` 方法會套用至 Instructions 資料行，並傳回資料列集 `T (C)`。 此資料列集包含原始製造指示文件的邏輯副本，並以 `/root/Location` 做為內容項目。  
  
-   CROSS APPLY 會將 `nodes()` 套用在 `Instructions` 資料表中的每個資料列，並且只傳回會產生結果集的資料列。  
  
    ```  
    SELECT C.query('.') as result  
    FROM Production.ProductModel  
    CROSS APPLY Instructions.nodes('  
    declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
    /MI:root/MI:Location') as T(C)  
    WHERE ProductModelID=7  
    ```  
  
     以下是部份結果：  
  
    ```  
    <MI:Location LocationID="10"  ...>  
       <MI:step ... />  
          ...  
    </MI:Location>  
    <MI:Location LocationID="20"  ... >  
        <MI:step ... />  
          ...  
    </MI:Location>  
    ...  
    ```  
  
### <a name="applying-nodes-to-the-rowset-returned-by-another-nodes-method"></a>將 nodes() 套用到由另一個 nodes() 方法傳回的資料列集  
 下列程式碼會在 XML 文件中查詢 `Instructions` 資料表之 `ProductModel` 資料行中的製造指示。 該查詢會傳回一個資料列集，其中包含產品型號識別碼、製造位置，以及製造步驟。  
  
 請注意下列事項：  
  
-   `nodes()` 方法會套用至 `Instructions` 資料行，並傳回 `T1 (Locations)` 資料列集。 此資料列集包含原始製造說明文件的邏輯副本，並以 `/root/Location` 元素做為項目內容。  
  
-   `nodes()` 會套用至 `T1 (Locations)` 資料列集，並傳回 `T2 (steps)` 資料列集。 此資料列集包含原始製造說明文件的邏輯副本，並以 `/root/Location/step` 元素做為項目內容。  
  
```  
SELECT ProductModelID, Locations.value('./@LocationID','int') as LocID,  
steps.query('.') as Step         
FROM Production.ProductModel         
CROSS APPLY Instructions.nodes('         
declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";         
/MI:root/MI:Location') as T1(Locations)         
CROSS APPLY T1.Locations.nodes('         
declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";         
./MI:step ') as T2(steps)         
WHERE ProductModelID=7         
GO         
```  
  
 以下是結果：  
  
```  
ProductModelID LocID Step         
----------------------------         
7      10   <step ... />         
7      10   <step ... />         
...         
7      20   <step ... />         
7      20   <step ... />         
7      20   <step ... />         
...         
```  
  
 此查詢會宣告二次 `MI` 前置詞。 您也可以改用 `WITH XMLNAMESPACES` 來宣告一次前置詞，並且在查詢中使用該前置詞：  
  
```  
WITH XMLNAMESPACES (  
   'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions'  AS MI)  
  
SELECT ProductModelID, Locations.value('./@LocationID','int') as LocID,  
steps.query('.') as Step         
FROM Production.ProductModel         
CROSS APPLY Instructions.nodes('         
/MI:root/MI:Location') as T1(Locations)         
CROSS APPLY T1.Locations.nodes('         
./MI:step ') as T2(steps)         
WHERE ProductModelID=7         
GO    
```  
  
## <a name="see-also"></a>請參閱＜  
 [使用 WITH XMLNAMESPACES 將命名空間加入至查詢](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [建立 XML 資料的執行個體](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 資料類型方法](../../t-sql/xml/xml-data-type-methods.md)  
  
  
