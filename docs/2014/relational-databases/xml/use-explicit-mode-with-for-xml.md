---
title: 搭配 FOR XML 使用 EXPLICIT 模式 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- EXPLICIT FOR XML mode
- FOR XML clause, EXPLICIT mode
- FOR XML EXPLICIT mode
ms.assetid: 8b26e8ce-5465-4e7a-b237-98d0f4578ab1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8976b77bf0823c9735e6e6e67fc3159bcb54ecdf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63231281"
---
# <a name="use-explicit-mode-with-for-xml"></a>搭配 FOR XML 使用 EXPLICIT 模式
  如[使用 FOR XML 來建立 xml](../xml/for-xml-sql-server.md)主題中所述，RAW 和 AUTO 模式不會對從查詢結果產生之 XML 的圖形提供很大的控制。 但是，EXPLICIT 模式在由查詢結果產生想要的 XML 方面，可提供的彈性最大。  
  
 EXPLICIT 模式詢必須以特定方式寫入，如此一來有關所需 XML 的額外資訊 (例如 XML 中將會構成的巢狀結構 )，就可以明確指定在查詢內。 根據您要求使用的 XML，撰寫 EXPLICIT 模式查詢會相當繁雜。 您可能會發現對撰寫 EXPLICIT 模式查詢而言， [使用 PATH 模式](../xml/use-path-mode-with-for-xml.md) 搭配巢狀結構是較為簡單的替代方法。  
  
 因為您會將想要的 XML 描述為 EXPLICIT 模式中查詢的一部份，所以您必須確定產生的 XML 有效而且格式正確。  
  
## <a name="rowset-processing-in-explicit-mode"></a>EXPLICIT 模式中的資料列集處理  
 EXPLICIT 模式會將執行查詢所產生的資料列集轉換為 XML 文件。 資料列集必須具有特定格式，EXPLICIT 模式才能產生 XML 文件。 您必須撰寫 SELECT 查詢，以特定格式產生資料列集 ( **通用資料表**)，如此處理邏輯之後才能產生您想要的 XML。  
  
 首先，查詢必須產生以下兩個中繼資料資料行：  
  
-   第一個資料行必須提供目前元素的標記編號、整數類型，而且該資料行名稱必須為 **Tag**。 您的查詢必須要為資料列集將要建構的每個元素，提供唯一的標記編號。  
  
-   第二個資料行必須提供父元素的標記編號，而且此資料行名稱必須為 **Parent**。 如此一來，「標記」與「父系」資料行就可以提供階層資訊。  
  
 這些中繼資料資料行值連同資料行名稱中的資訊，都會用來產生您想要的 XML。 請注意，您的查詢必須以特定的方式提供資料行名稱。 此外，也請注意， **Parent** 資料行中的 0 或 NULL 表示該對應元素沒有父系。 該元素會作為最上層元素增加到 XML。  
  
 若要了解查詢產生的通用資料表是如何處理以產生 XML 結果，假設您已經撰寫可以處理此通用資料表的查詢：  
  
 ![範例通用資料表](../../database-engine/media/xmlutable.gif "範例通用資料表")  
  
 記下有關此通用資料表的下列各項：  
  
-   前兩個資料行是 **Tag** 和 **Parent** ，而且都是中繼資料行。 這些值可以決定階層。  
  
-   資料行名稱是以特定方式指定，如本主題稍後所述。  
  
-   在由此通用資料表產生 XML 時，此資料表中的資料會垂直分割成資料行群組。 分組是根據 **Tag** 值及資料行名稱來決定。 建構 XML 時，處理邏輯會為每個資料列選取一個資料行群組並建構一個元素。 以下適用於此範例：  
  
    -   對於第一個資料列中的 **Tag** 資料行值 1，其名稱包含相同標記編號的資料行 **Customer!1!cid** 及 **Customer!1!name** 會形成一個群組。 這些資料行是用來處理資料列，而且您可能已注意到產生的元素是 <`Customer id=... name=...`>。 資料行名稱格式會在本主題稍後描述。  
  
    -   對於 **Tag** 資料行值 2 的資料列，資料行 **Order!2!id** 及 **Order!2!date** 會形成一個群組，之後會用來建構元素 <`Order id=... date=... /`>。  
  
    -   對於 **Tag** 資料行值 3 的資料列，資料行 **OrderDetail!3!id!id** 及 **OrderDetail!3!pid!idref** 會形成一個群組。 每一個資料列都會由這些資料行產生一個元素 <`OrderDetail id=... pid=...`>。  
  
-   請注意，在產生 XML 階層時，會依序處理資料列。 決定 XML 階層的方式如下所示：  
  
    -   第一個資料列指定 **Tag** 值 1 及 **Parent** 值 NULL。 因此，對應的元素 (<`Customer`> 元素) 是新增為 XML 中的最上層元素。  
  
        ```  
        <Customer cid="C1" name="Janine">  
        ```  
  
    -   第二個資料列指定 **Tag** 值 2 及 **Parent** 值 1。 因此，<`Order`> 元素會加入為 <`Customer`> 元素的子系。  
  
        ```  
        <Customer cid="C1" name="Janine">  
           <Order id="O1" date="1/20/1996">  
        ```  
  
    -   後面兩個資料列指定 **Tag** 值 3 及 **Parent** 值 2。 因此，<`OrderDetail`> 這兩個元素會加入為 <`Order`> 元素的子系。  
  
        ```  
        <Customer cid="C1" name="Janine">  
           <Order id="O1" date="1/20/1996">  
              <OrderDetail id="OD1" pid="P1"/>  
              <OrderDetail id="OD2" pid="P2"/>  
        ```  
  
    -   最後一個資料列將 2 指定為 **Tag** 編號，並將 1 指定為 **Parent** 標記編號。 因此，會將另一個 <`Order`> 元素子系新增到 <`Customer`> 父元素。  
  
        ```  
        <Customer cid="C1" name="Janine">  
           <Order id="O1" date="1/20/1996">  
              <OrderDetail id="OD1" pid="P1"/>  
              <OrderDetail id="OD2" pid="P2"/>  
           </Order>  
           <Order id="O2" date="3/29/1997">  
        </Customer>  
        ```  
  
 簡言之，**Tag** 及 **Parent** 中繼資料行中的值、資料行名稱提供的相關資訊，以及資料列的正確順序都可以在您使用 EXPLICIT 模式時，產生您想要的 XML。  
  
### <a name="universal-table-row-ordering"></a>通用資料表資料列順序  
 在建構 XML 時，會按照順序處理通用資料表中的資料列集。 因此，若要擷取與父系相關的正確子執行個體，就必須要將資料列集中的資料列排序，如此每個父節點後面就會緊跟著其所屬子系。  
  
## <a name="specifying-column-names-in-a-universal-table"></a>指定通用資料表的資料行名稱  
 撰寫 EXPLICIT 模式查詢時，必須使用此格式指定所產生資料列集中的資料行名稱。 它們可提供轉換資訊，包括使用指示詞指定的元素集屬性名稱和其他資訊在內。  
  
 此為一般格式：  
  
```  
  
ElementName!TagNumber!AttributeName!Directive  
```  
  
 以下是格式的部份描述。  
  
 *ElementName*  
 是產生的元素一般識別碼。 例如，若將 **Customers** 指定為 *ElementName*，就會產生 \<Customers> 項目。  
  
 *TagNumber*  
 是指派給元素的唯一標記值。 此值搭配兩個中繼資料資料行 **Tag** 及 **Parent**，就可以決定結果 XML 中元素的巢狀結構。  
  
 *AttributeName*  
 提供要在指定的 *ElementName*中建構的屬性名稱。 如果未指定「指示詞」**，就會使用這個行為。  
  
 如果指定「指示詞」** 而且它是 **xml**、**cdata** 或 **element**，就會使用此值建構 *ElementName* 的元素子系，而且會加入資料行值。  
  
 如果指定「指示詞」**，*AttributeName* 可以為空白。 例如，ElementName!TagNumber!!Directive。 在此情況下， *ElementName*會直接包含資料行值。  
  
 *指示詞*  
 指示*詞是選擇性的，* 您可以用它來提供 XML 結構的其他資訊。 指示*詞有兩*個用途。  
  
 其中一項用途是將值編碼為 ID、IDREF 及 IDREFS。 您可以指定 **ID**、**IDREF** 及 **IDREFS** 關鍵字作為「指示詞」**。 這些指示詞會覆寫屬性類型。 您可以藉此建立內部文件連結。  
  
 此外，您可以使用「指示詞」** 指出要如何將字串資料對應到 XML。 
  **hide**、**element、elementxsinil**、**xml**、**xmltext** 及 **cdata** 關鍵字可以作為「指示詞」**。 
  **hide** 指示詞會隱藏節點。 只是為了進行排序而擷取值，但不希望產生 XML 時，這就很有用。  
  
 
  **element** 指示詞會產生內含元素而不是屬性。 內含的資料會被編碼為實體。 例如， **<** 字元會變成&lt;。 對於 NULL 資料行值，不會產生任何元素。 如果希望 Null 資料行值會產生一個元素，您可以指定 **elementxsinil** 指示詞。 這將會產生具有屬性 xsi:nil=TRUE 的元素。  
  
 除了不會進行實體編碼之外， **xml** 指示詞和 **element** 指示詞一樣。 請注意， **element** 指示詞可以與 **ID**、 **IDREF**或 **IDREFS**合併，而 **xml** 指示詞不能與任何其他指示詞一起使用，除了 **hide**之外。  
  
 
  **cdata** 指示詞包含利用 CDATA 區段包裝的資料。 內容並未進行實體編碼。 原始資料類型必須是文字類型，例如 **varchar**、 **nvarchar**、 **text**或 **ntext**。 此指示詞只適用於 **hide**。 使用此指示詞時，絕不能指定 *AttributeName* 。  
  
 在大部份情況下，您可以合併這兩個群組織間的指示詞，但不可以合併指示詞本身。  
  
 如果未指定「指示詞」** 及 *AttributeName* (例如 **Customer!1**)，就會隱含 **element** 指示詞 (例如 **Customer!1!!element**)，而 *ElementName* 中會包含資料行資料。  
  
 如果指定 **xmltext** 指示詞，資料行內容會包裝在單一標記中，與文件的其他部分整合。 此指示詞用來取得 OPENXML 儲存在資料行的溢位 (未消耗) XML 資料很有用。 如需詳細資訊，請參閱 [OPENXML &#40;SQL Server&#41;](../xml/openxml-sql-server.md)。  
  
 如果指定 *AttributeName*，就會以指定的名稱取代標記名稱。 否則，將內容放在不進行實體編碼的內含項目開頭，就會在內含元素目前的屬性清單後面附加上該屬性。 具有此指示詞的資料行必須屬於文字類型，例如 **varchar**、 **nvarchar**、 **char**、 **nchar**、 **text**或 **ntext**。 此指示詞只適用於 **hide**。 此指示詞可用來取得儲存在資料行的溢位資料。 若內容不是完整形成的 XML，則行為是未定義的。  
  
## <a name="in-this-section"></a>本節內容  
 下列範例說明 EXPLICIT 模式的用法。  
  
-   [範例：擷取員工資訊](../xml/example-retrieving-employee-information.md)  
  
-   [範例：指定 ELEMENT 指示詞](../xml/example-specifying-the-element-directive.md)  
  
-   [範例：指定 ELEMENTXSINIL 指示詞](../xml/example-specifying-the-elementxsinil-directive.md)  
  
-   [範例：使用 EXPLICIT 模式建構同層級](../xml/example-constructing-siblings-with-explicit-mode.md)  
  
-   [範例：指定 ID 和 IDREF 指示詞](../xml/example-specifying-the-id-and-idref-directives.md)  
  
-   [範例：指定 ID 和 IDREFS 指示詞](../xml/example-specifying-the-id-and-idrefs-directives.md)  
  
-   [範例：指定 HIDE 指示詞](../xml/example-specifying-the-hide-directive.md)  
  
-   [範例：指定 ELEMENT 指示詞及實體編碼](../xml/example-specifying-the-element-directive-and-entity-encoding.md)  
  
-   [範例：指定 CDATA 指示詞](../xml/example-specifying-the-cdata-directive.md)  
  
-   [範例：指定 XMLTEXT 指示詞](../xml/example-specifying-the-xmltext-directive.md)  
  
## <a name="see-also"></a>另請參閱  
 [搭配 FOR XML 使用 RAW 模式](../xml/use-raw-mode-with-for-xml.md)   
 [搭配 FOR XML 使用 AUTO 模式](../xml/use-auto-mode-with-for-xml.md)   
 [搭配 FOR XML 使用 PATH 模式](../xml/use-path-mode-with-for-xml.md)   
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [FOR XML &#40;SQL Server&#41;](../xml/for-xml-sql-server.md)  
  
  
