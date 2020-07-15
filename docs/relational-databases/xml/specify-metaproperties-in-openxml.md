---
title: 在 OPENXML 中指定中繼屬性 | Microsoft Docs
description: 了解如何在 OPENXML 陳述式中指定中繼屬性來擷取 XML 節點的資訊。
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- overflow in XML document [SQL Server]
- metaproperties [XML in SQL Server]
- unconsumed data
- extracting information of XML nodes [SQL Server]
- OPENXML statement, metaproperties
ms.assetid: 29bfd1c6-3f9a-43c4-924a-53d438e442f4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd34411b00bfa89c5c69b0d71073ee1c0d4d2280
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85728124"
---
# <a name="specify-metaproperties-in-openxml"></a>在 OPENXML 中指定中繼屬性
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  XML 文件的中繼屬性 (Metaproperty) 之屬性 (Attribute)，是描述 XML 項目 (例如元素、屬性或任何其他 DOM 節點) 屬性 (Property) 的屬性 (Attribute)。 這些屬性實際上不存在於 XML 文件文字中。 不過，OPENXML 會提供這些中繼屬性給所有的 XML 項目。 這些中繼屬性可讓您擷取 XML 節點的資訊，例如本機定位和命名空間資訊。 此資訊可提供您所呈現文字以外更詳細的資料。  
  
 您可以使用 *ColPattern* 參數，將這些中繼屬性對應至 OPENXML 陳述式的資料列集資料行。 這些資料行將會包括其所對應的中繼屬性值。 如需 OPENXML 語法的詳細資訊，請參閱 [OPENXML &#40;Transact-SQL&#41;](../../t-sql/functions/openxml-transact-sql.md)。  
  
 若要存取中繼屬性的屬性，需提供 SQL Server 特定的命名空間。 這個命名空間 **urn:schemas-microsoft-com:xml-metaprop** 可讓使用者存取中繼屬性的屬性。 若 OPENXML 查詢的結果是以邊緣資料表格式傳回，每一個中繼屬性的屬性在邊緣資料表中各有一個資料行 ( **xmltext** 中繼屬性除外)。  
  
 有些中繼屬性的屬性是使用來進行處理。 例如， **xmltext** 中繼屬性的屬性是用來處理溢位。 溢位處理指的是文件中未消耗/未處理的資料。 由 OPENXML 產生之資料列集的其中一個資料行可識別為溢位資料行。 作法是使用 **ColPattern** 參數，將它對應到 *xmltext* 中繼屬性。 然後資料行就會接收溢位資料。 *flags* 參數會判斷資料行是否包含所有資料，或只包含未耗用的資料。  
  
 以下資料表將列出每個剖析 XML 元素具有的中繼屬性。 這些中繼屬性的屬性可使用命名空間 **urn:schemas-microsoft-com:xml-metaprop**加以存取。 由使用者利用這些中繼屬性直接在 XML 文件中設定的任何值，將予以忽略。  
  
> [!NOTE]  
>  您無法在任何 XPath 瀏覽中參考這些中繼屬性。  
  
|中繼屬性的屬性|描述|  
|----------------------------|-----------------|  
|**\@mp:id**|提供 DOM 節點的全文件識別碼 (由系統產生)。 只要文件未經過重新分析，此識別碼就會參照相同的 XML 節點。<br /><br /> XML 識別碼為 **0** ，表示元素為根元素。 其父系 XML 識別碼為 NULL。|  
|**\@mp:localname**|儲存節點名稱的本機部份。 它會和前置詞及命名空間 URI 一起用來命名元素或屬性節點。|  
|**\@mp:namespaceuri**|提供目前元素的命名空間 URI。 若此屬性值為 NULL，則沒有命名空間|  
|**\@mp:prefix**|儲存現行元素名稱的命名空間前置詞。<br /><br /> 若無前置詞 (NULL) 但提供了 URI，表示指定的命名空間是預設命名空間。 若未提供 URI，則不附加任何命名空間。|  
|**\@mp:prev**|儲存相對於節點的前一個同層級。 這提供了文件中元素排序的相關資訊。<br /><br /> **\@mp:prev** 含有具相同父元素的前一個同層級元素的 XML 識別碼。 若元素位在同層級元素清單的前端，則 **\@mp:prev** 為 NULL。|  
|**\@mp:xmltext**|用來進行處理。 它是元素及其屬性 (還有子元素) 的文字序列化，會用在 OPENXML 的溢位處理。|  
  
 下表顯示所提供的其他父屬性，可讓您擷取關於階層的資訊。  
  
|父系中繼屬性的屬性|描述|  
|-----------------------------------|-----------------|  
|**\@mp:parentid**|對應至 **../\@mp:id**|  
|**\@mp:parentlocalname**|對應至 **../\@mp:localname**|  
|**\@mp:parentnamespacerui**|對應至 **../\@mp:namespaceuri**|  
|**\@mp:parentprefix**|對應至 **../\@mp:prefix**|  
  
## <a name="examples"></a>範例  
 下列範例說明如何使用 OPENXML 來建立不同的資料列集檢視。  
  
### <a name="a-mapping-the-openxml-rowset-columns-to-the-metaproperties"></a>A. 將 OPENXML 資料列集資料行對應至中繼屬性  
 此範例使用 OPENXML 來建立範例 XML 文件的資料列集檢視。 並特別說明如何利用 *ColPattern* 參數，將各種中繼屬性的屬性，對應到 OPENXML 陳述式的資料列集資料行。  
  
 OPENXML 陳述式說明下列各項：  
  
-   **id** 資料行會對應到 **\@mp:id** 中繼屬性 (metaproperty) 屬性 (attribute)，表示該資料行包含元素的唯一 XML 識別碼 (由系統產生)。  
  
-   **parent** 資料行會對應到 **\@mp:parentid** ，表示該資料行包含元素父系的 XML 識別碼。  
  
-   **parentLocalName** 資料行會對應到 **\@mp:parentlocalname** ，表示該資料行包含父系的區域名稱。  
  
 然後，SELECT 陳述式會傳回 OPENXML 所提供的資料列集：  
  
```  
DECLARE @idoc int  
DECLARE @doc nvarchar(1000)  
-- Sample XML document  
SET @doc = N'<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was very satisfied</Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue white red">  
          <Urgency>Important</Urgency>  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@idoc, '/root/Customer/Order', 9)  
      WITH (id int '@mp:id',   
            oid char(5),   
            date datetime,   
            amount real,   
            parentIDNo int '@mp:parentid',   
            parentLocalName varchar(40) '@mp:parentlocalname')  
EXEC sp_xml_removedocument @idoc  
```  
  
 以下是結果：  
  
```  
id   oid         date                amount    parentIDNo  parentLocalName    
--- ------- ---------------------- ---------- ------------ ---------------  
6    O1    1996-01-20 00:00:00.000     3.5         2        Customer  
10   O2    1997-04-30 00:00:00.000     13.4        2        Customer  
19   O3    1999-07-14 00:00:00.000     100.0       15       Customer  
25   O4    1996-01-20 00:00:00.000     10000.0     15       Customer  
```  
  
### <a name="b-retrieving-the-whole-xml-document"></a>B. 擷取整份 XML 文件  
 在此範例中，會使用 OPENXML 建立範本 XML 文件的單一資料行資料列集檢視。 此資料行 **Col1**會對應到 **xmltext** 中繼屬性，而成為溢位資料行。 所以，此資料行將接收未耗用的資料。 在此案例中，就是指整份文件。  
  
 然後 SELECT 陳述式會傳回完整的資料列集。  
  
```  
DECLARE @idoc int  
DECLARE @doc nvarchar(1000)  
SET @doc = N'<?xml version="1.0"?>  
<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was very   
             satisfied</Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue   
             white red">  
     <MyTag>Testing to see if all the subelements are returned</MyTag>  
          <Urgency>Important</Urgency>  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@idoc, '/')  
   WITH (Col1 ntext '@mp:xmltext')  
```  
  
 若要擷取整份文件，但不要 XML 宣告，則可將查詢指定為如下所示：  
  
```  
SELECT *  
FROM OPENXML (@idoc, '/root')  
   WITH (Col1 ntext '@mp:xmltext')  
EXEC sp_xml_removedocument @idoc  
```  
  
 查詢將傳回含有 root 名稱的根元素，以及根元素所包含的資料。  
  
### <a name="c-specifying-the-xmltext-metaproperty-to-retrieve-the-unconsumed-data-in-a-column"></a>C. 指定 xmltext 中繼屬性來擷取資料行中未耗用的資料  
 此範例使用 OPENXML 來建立範例 XML 文件的資料列集檢視。 範例中將說明如何將 **xmltext** 中繼屬性的屬性對應到 OPENXML 中的資料列集資料行，以擷取未消耗的 XML 資料。  
  
 **comment** 資料行藉由對應到 **\@mp:xmltext** 中繼屬性，而被識別為溢位資料行。 *flags* 參數是設為 **9** (XML_ATTRIBUTE 和 XML_NOCOPY)。 這表示 **屬性中心** 對應，並表示只有未耗用的資料才要複製到溢位資料行。  
  
 然後 SELECT 陳述式將傳回由 OPENXML 所提供的資料列集。  
  
 在此範例中， **\@mp:parentlocalname** 中繼屬性是針對 OPENXML 所產生資料列集的資料行 **ParentLocalName** 來設定的。 因此，此資料行含有父元素的本機名稱。  
  
 資料列集內還指定了另外兩個資料行： **parent** 及 **comment**。 **parent** 資料行會對應到 **\@mp:parentid** ，表示該資料行包含元素之父元素的 XML 識別碼。 comment 資料行藉由對應到 **\@mp:xmltext** 中繼屬性，而被識別為溢位資料行。  
  
```  
DECLARE @idoc int  
DECLARE @doc nvarchar(1000)  
-- sample XML document  
SET @doc = N'<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was very satisfied</Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue white red">  
          <Urgency>Important</Urgency>  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>  
'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@idoc, '/root/Customer/Order', 9)  
      WITH (oid char(5),   
            date datetime,  
            comment ntext '@mp:xmltext')  
EXEC sp_xml_removedocument @idoc  
```  
  
 以下是結果。 由於已耗用 oid 資料行及 date 資料行，因此它們沒有出現在溢位資料行中。  
  
```  
oid   date                        comment                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            
----- --------------------------- ----------------------------------------  
O1    1996-01-20 00:00:00.000     <Order amount="3.5"/>  
O2    1997-04-30 00:00:00.000     <Order amount="13.4">Customer was very   
                                   satisfied</Order>  
O3    1999-07-14 00:00:00.000     <Order amount="100" note="Wrap it blue   
                                   white red"><Urgency>   
                                   Important</Urgency></Order>  
O4    1996-01-20 00:00:00.000     <Order amount="10000"/>  
```  
  
## <a name="see-also"></a>另請參閱  
 [OPENXML &#40;Transact-SQL&#41;](../../t-sql/functions/openxml-transact-sql.md)   
 [OPENXML &#40;SQL Server&#41;](../../relational-databases/xml/openxml-sql-server.md)  
  
  
